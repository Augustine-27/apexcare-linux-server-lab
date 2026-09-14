# Incident 004 — ApexCare Website Error

## Incident Summary

**Issue:** Customers reported that the ApexCare website was responding with an error when attempting to access the homepage.

**Reported Problem:**

> “The website is responding, but customers are getting an error when they try to access the homepage.”

## Investigation

A structured investigation was carried out to determine whether the issue was related to the Nginx service, website configuration, document root, logs, or the deployed website files.

### 1. Nginx Service Status

The Nginx service was checked and confirmed to be active and running.

**Result:** Nginx was operational.

### 2. HTTP Port

The server was checked to confirm that Nginx was listening on TCP port 80.

**Result:** Port 80 was listening and accepting HTTP connections.

### 3. Website Response

The ApexCare hostname was tested using an HTTP request.

**Result:** The website was accessible and returned an HTTP `200 OK` response after the configuration was corrected.

### 4. Access Log Investigation

The Nginx access log was reviewed to identify the HTTP responses generated during the incident.

A historical request to the homepage returned:

`404 Not Found`

The access log therefore confirmed that the homepage had previously been unavailable even though Nginx itself was running.

### 5. Error Log Investigation

The Nginx error log was checked for additional errors associated with the incident.

**Result:** No corresponding error was recorded in the Nginx error log.

### 6. Nginx Configuration Inspection

The active ApexCare Nginx configuration was inspected.

The expected document root was:

`/var/www/apexcare`

The configuration was compared with the backup configuration to identify any unexpected changes.

### 7. Website Files and Permissions

The ApexCare document root and website files were checked.

The website files were present and had appropriate read permissions for the Nginx web server.

### 8. Configuration Validation

Before applying the corrected configuration, the Nginx configuration was tested to confirm that the configuration syntax was valid.

**Result:** The Nginx configuration test was successful.

### 9. Configuration Reload

The corrected configuration was applied by reloading Nginx rather than restarting the service.

This allowed the configuration to be updated while minimizing service disruption.

### 10. Post-Change Testing

The website was tested again after the configuration was corrected and Nginx was reloaded.

**Result:** The ApexCare homepage loaded successfully and returned an HTTP `200 OK` response.

## Findings

The investigation established that:

* Nginx was running.
* TCP port 80 was available.
* The website files were present.
* The website files had appropriate permissions.
* A historical homepage request returned `404 Not Found`.
* The Nginx error log contained no corresponding error.
* The Nginx configuration required correction.
* The corrected configuration passed the Nginx syntax test.
* After reloading Nginx, the homepage returned successfully.

## Root Cause

A configuration change caused Nginx to serve the ApexCare homepage incorrectly, resulting in an HTTP `404 Not Found` response.

The configuration was identified through log analysis, configuration inspection, and comparison with the expected configuration.

## Resolution

The incorrect configuration was corrected and validated using the Nginx configuration test.

Nginx was then reloaded to apply the corrected configuration.

A subsequent HTTP request returned `200 OK`, confirming that the web server successfully processed the request and returned the requested homepage.

## Resolution Status

**Status:** Resolved.

**Root Cause:** Incorrect Nginx configuration affecting the website's document serving.

**Resolution:** Corrected the configuration, validated it, reloaded Nginx, and confirmed successful website access.

