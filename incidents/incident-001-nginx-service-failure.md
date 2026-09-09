# Incident 001 — Nginx Service Failure

## 1. Incident Summary

**Incident ID:** INC-001
**System:** ApexCare Solutions Linux Web Server
**Service:** Nginx
**Severity:** Medium
**Status:** Resolved

### Issue

The ApexCare Solutions website became unavailable because the Nginx web server service was stopped.

---

## 2. Symptoms

The website could not be accessed through:

`http://apexcare.local`

A connection test using `curl` returned:

`curl: (7) Failed to connect to apexcare.local port 80: Could not connect to server`

---

## 3. Investigation

### Step 1 — Checked Nginx service status

Command used:

`sudo systemctl status nginx`

Result:

`Active: inactive (dead)`

This confirmed that the Nginx service was not running.

### Step 2 — Tested the website from the server

Command used:

`curl http://apexcare.local`

Result:

Connection to port 80 failed.

This confirmed that the website was not reachable from the server itself.

### Step 3 — Checked port 80

Command used:

`sudo ss -tulnp | grep :80`

Result:

No output was returned.

This indicated that no process was listening on TCP port 80.

---

## 4. Root Cause

The Nginx service had been stopped.

Because Nginx was responsible for serving the ApexCare website over HTTP port 80, stopping the service caused the website to become unavailable.

---

## 5. Resolution

Nginx was started using:

`sudo systemctl start nginx`

The service status was then checked and showed:

`Active: active (running)`

---

## 6. Verification

### Port verification

Command:

`sudo ss -tulnp | grep :80`

Result:

Nginx was listening on port 80 through IPv4 and IPv6.

### Application verification

Command:

`curl http://apexcare.local`

Result:

The ApexCare website HTML was successfully returned.

### Browser verification

The website was also successfully accessed from the Windows browser using:

`http://apexcare.local`

---

## 7. Final Status

**Resolved**

The Nginx service was restored and the ApexCare website was confirmed to be operational.

---

## 8. Technical Support Skills Demonstrated

* Linux service management
* Nginx administration
* Network port troubleshooting
* HTTP troubleshooting
* Command-line diagnostics
* Root-cause analysis
* Service recovery
* Application verification
* Incident documentation

