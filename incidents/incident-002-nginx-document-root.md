# Incident 002 — Nginx Incorrect Document Root

## 1. Incident Summary

**Incident ID:** INC-002
**System:** ApexCare Solutions Linux Web Server
**Service:** Nginx
**Severity:** Medium
**Status:** Resolved

### Issue

The ApexCare website returned a **404 Not Found** response after an incorrect document root was configured in the Nginx virtual host.

---

## 2. Symptoms

The Nginx service was running and port 80 was listening, but requests to:

`http://apexcare.local`

returned:

`404 Not Found`

---

## 3. Investigation

### Step 1 — Confirmed the Nginx configuration syntax

Command:

`sudo nginx -t`

Result:

`syntax is ok`
`test is successful`

This showed that the configuration was syntactically valid.

### Step 2 — Checked the configured website directory

The Nginx configuration had been intentionally changed from:

`root /var/www/apexcare;`

to:

`root /var/www/apexcare123;`

The directory was checked using:

`ls -ld /var/www/apexcare123`

Result:

`No such file or directory`

This confirmed that the configured document root did not exist.

### Step 3 — Checked the Nginx access log

Command:

`sudo tail -n 10 /var/log/nginx/access.log`

The access log showed:

`"GET / HTTP/1.1" 404`

This confirmed that Nginx received the HTTP request but returned a 404 response.

---

## 4. Root Cause

The Nginx virtual host was configured with an incorrect document root:

`/var/www/apexcare123`

The directory did not exist and therefore Nginx could not locate the website's requested resources.

---

## 5. Resolution

The Nginx configuration was corrected from:

`root /var/www/apexcare123;`

to:

`root /var/www/apexcare;`

The configuration was then tested using:

`sudo nginx -t`

The configuration test was successful.

Nginx was reloaded using:

`sudo systemctl reload nginx`

---

## 6. Verification

The website was tested using:

`curl http://apexcare.local`

The ApexCare website HTML was successfully returned.

The website was also confirmed to work from the Windows browser.

---

## 7. Key Technical Finding

A successful Nginx configuration test does not necessarily mean that the application will work correctly.

`nginx -t` confirmed that the configuration syntax was valid, but it did not detect that the configured document root directory did not exist.

Additional checks of the filesystem, access logs, and application response were therefore required.

---

## 8. Final Status

**Resolved**

The incorrect document root was corrected, Nginx was reloaded successfully, and the ApexCare website was restored.

---

## 9. Technical Support Skills Demonstrated

* Nginx virtual host troubleshooting
* Linux filesystem investigation
* HTTP status-code analysis
* Nginx log analysis
* Configuration validation
* Root-cause analysis
* Web server recovery
* Command-line troubleshooting
* Incident documentation
