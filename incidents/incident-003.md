# Incident 003 — Website Connectivity Investigation

## Incident Summary

**Issue:** Customer reported that the ApexCare website could not be accessed from their computer.

**Reported Problem:**

> “I cannot access the ApexCare website from my computer. Other websites are working normally.”

## Investigation

A structured troubleshooting process was carried out to determine whether the issue was related to the server, Nginx, networking, hostname resolution, or the client environment.

### 1. Nginx Service

The Nginx service was checked and confirmed to be active and running.

**Result:** Nginx service was operational.

### 2. HTTP Port

The server's listening ports were checked. Nginx was confirmed to be listening on TCP port 80 through both IPv4 and IPv6.

**Result:** HTTP port 80 was operational.

### 3. Local Website Test

The website was accessed locally from the Linux server using `curl`.

**Result:** The ApexCare website returned the expected HTML content successfully.

### 4. Linux Hostname Resolution

The hostname `apexcare.local` was tested from the Linux environment.

**Result:**

`apexcare.local` resolved correctly to `127.0.0.1`.

### 5. Windows Client Test

The website was accessed from the Windows client using `curl`.

**Result:** The ApexCare website returned the expected HTML content successfully.

### 6. Windows Hostname Resolution

The hostname was tested from Windows using `ping`.

**Result:**

`apexcare.local` resolved to `127.0.0.1`.

Four packets were sent and four were received, resulting in **0% packet loss**.

### 7. Browser Test

The website was opened directly in the Windows browser.

**Result:** The ApexCare website loaded normally.

## Findings

All tested components were functioning normally:

* Nginx service — Operational
* TCP port 80 — Listening
* Website — Accessible
* Linux hostname resolution — Working
* Windows hostname resolution — Working
* Client connectivity — Working
* Windows HTTP request — Successful
* Browser access — Successful

The reported issue could not be reproduced during the investigation.

## Conclusion

After a thorough investigation of the server and system environment, 
no server-side root cause was identified for the reported website accessibility issue. 
The reported problem could not be reproduced during the investigation,
as the website was functioning normally from both the server and client environments.
If the issue continues to occur, the incident should be escalated to the appropriate technical support team 
for further investigation. If no server-side issue is identified, further investigation should be carried out from 
the client's environment, including the client device, browser, 
network connectivity, DNS configuration, and other client-specific factors.

## Resolution Status

**Status:** No server-side fault identified / Issue not reproducible.

**Recommended Action:** Monitor for recurrence and investigate the client environment if the issue occurs again.
