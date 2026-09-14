# Incident 007 — High CPU Usage

## Incident Summary

**Issue:** Users reported that the ApexCare website had become slow and that the server appeared to be taking longer than normal to respond.

**Reported Problem:**

> “The ApexCare website has become slow and users are complaining that the server is taking too long to respond. Please investigate the server and identify what might be causing the high resource usage.”

## Investigation

A structured investigation was carried out to determine whether high CPU usage or another server-side resource problem was affecting website performance.

### 1. System CPU and Memory Usage

The system was monitored using the Linux `top` utility.

The server showed:

* Very low system load
* 100% CPU idle during the check
* No significant I/O wait
* Approximately 2.7 GiB of free memory
* No swap usage
* No zombie processes

**Result:** No abnormal CPU or memory usage was identified.

### 2. Process Investigation

Running processes were reviewed to determine whether any process was consuming excessive CPU resources.

The Nginx worker processes were using negligible CPU resources.

**Result:** No process was identified as consuming excessive CPU resources.

### 3. Nginx Service

The Nginx service was checked and confirmed to be active.

**Result:** Nginx was operational.

### 4. Nginx Error Logs

The Nginx error log was checked for server-side errors.

**Result:** No significant errors were recorded.

### 5. Nginx Journal

The Nginx system journal was reviewed for errors occurring during the investigation period.

**Result:** No Nginx error entries were identified.

### 6. Website Access Logs

The Nginx access log was reviewed after generating fresh website requests.

The logs showed successful homepage requests and normal browser cache responses.

A `404` response was observed for a favicon request, but no significant server errors such as `500`, `502`, `503`, or `504` were identified.

**Result:** Website requests were being processed normally.

### 7. Linux HTTP Response Time

The ApexCare website was tested from Linux and the HTTP request timing was measured.

The total response time was approximately:

`0.021 seconds`

**Result:** The server responded quickly.

### 8. Windows HTTP Response Time

The website was also tested from the Windows client.

The total response time was approximately:

`0.033 seconds`

**Result:** The client received a fast response from the website.

### 9. Windows Network Connectivity

The hostname was tested from Windows.

The hostname resolved to `127.0.0.1` and the connection showed:

* 0% packet loss
* Approximately 0 ms average response time

**Result:** No connectivity issue was identified.

### 10. Browser Test

The ApexCare website was accessed through the Windows browser.

**Result:** The website loaded normally.

## Findings

The investigation established that:

* CPU utilization was normal.
* System load was very low.
* Memory usage was normal.
* No swap was being used.
* No process was consuming excessive CPU.
* Nginx was active.
* Nginx error logs were clean.
* Nginx journal logs showed no relevant errors.
* Website requests were returning successful responses.
* Linux HTTP response time was approximately 21 milliseconds.
* Windows HTTP response time was approximately 33 milliseconds.
* Network connectivity showed 0% packet loss.
* The website loaded normally in the browser.

## Root Cause

No server-side root cause for high CPU usage or website performance degradation was identified.

The reported performance issue could not be reproduced during the investigation.

## Resolution

No server-side changes were required because the server was operating within normal resource and performance levels.

If users continue to experience slow performance, further investigation should be carried out from the client side and at the time the issue occurs.

Potential areas for further investigation include:

* Client network connection
* Client device resources
* Browser performance
* Browser extensions
* DNS configuration
* Other client-specific factors

## Resolution Status

**Status:** No server-side root cause identified / Issue not reproducible.

**Recommended Action:** Monitor server resources and website performance. If the issue recurs, capture system and application metrics during the incident and investigate the affected client's environment.
