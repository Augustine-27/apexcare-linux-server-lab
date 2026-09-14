# Incident 005 — Slow Website Performance

## Incident Summary

**Issue:** Users reported that the ApexCare website was loading slowly.

**Reported Problem:**

> “The website is loading very slowly. It eventually opens, but pages take much longer than normal. Please investigate.”

## Investigation

A structured investigation was carried out to determine whether the reported performance issue was caused by high CPU usage, memory pressure, Nginx, network connectivity, hostname resolution, or the website itself.

### 1. System Resource Usage

System resource usage was checked using the Linux system monitoring tools.

The server showed:

* Very low system load
* Approximately 99.9% CPU idle
* No significant I/O wait
* Adequate available memory
* No swap usage
* No zombie processes

**Result:** No abnormal CPU, memory, or system resource usage was identified.

### 2. Nginx Service

The Nginx service was checked and confirmed to be active and running.

**Result:** Nginx was operational.

### 3. Website HTTP Response

The ApexCare website was tested using an HTTP request.

**Result:** The website returned an HTTP `200 OK` response.

### 4. Website Response Time

The total HTTP response time was measured from the Linux environment.

The website responded in approximately:

`0.008 seconds`

**Result:** The response time was very fast and did not indicate a server-side performance problem.

### 5. Network Connectivity

The ApexCare hostname was tested using `ping`.

The hostname resolved to `127.0.0.1` with:

* 0% packet loss
* Approximately 0.073 ms average response time

**Result:** No network connectivity problem was identified.

### 6. Nginx Logs

The Nginx access and error logs were reviewed for abnormal responses or errors.

The logs showed normal website requests, including successful `200` responses and normal browser cache-related `304` responses.

No significant server errors were identified.

### 7. Browser Test

The website was accessed directly through the browser.

**Result:** The website loaded normally and the reported slowness could not be reproduced.

## Findings

The investigation established that:

* CPU utilization was normal.
* Memory utilization was normal.
* No swap was being used.
* Nginx was active.
* The website returned HTTP `200 OK`.
* Website response time was approximately 8 milliseconds.
* Network connectivity showed 0% packet loss.
* Nginx logs did not indicate a significant server-side problem.
* The website loaded normally from the browser.

## Root Cause

No server-side root cause was identified.

The reported performance issue could not be reproduced during the investigation.

## Resolution

No server-side changes were required because the server and website were operating normally.

If users continue to experience slow performance, further investigation should be carried out from the client side, including:

* Client network connection
* Browser performance
* Client device resources
* Browser extensions
* DNS configuration
* Other client-specific factors

## Resolution Status

**Status:** No server-side fault identified / Issue not reproducible.

**Recommended Action:** Monitor for recurrence and investigate the client environment if the problem occurs again.
