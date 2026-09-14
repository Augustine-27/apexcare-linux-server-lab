# ApexCare Solutions — Linux Server & Technical Support Lab

A practical Linux and Technical Support portfolio project simulating the responsibilities of a Junior Linux / Technical Support Engineer supporting a small company's web infrastructure.

The project demonstrates hands-on experience with **Linux administration, Nginx, networking, system monitoring, log analysis, incident investigation, troubleshooting, service recovery, technical documentation, and Git/GitHub**.

---

## Project Overview

**ApexCare Solutions** is a fictional technology company used as the environment for this technical support lab.

The project was built to simulate a real-world support environment where a technical support engineer is responsible for:

* Managing a Linux server
* Deploying and maintaining a company website
* Managing Nginx
* Monitoring system resources and services
* Investigating network and connectivity issues
* Analyzing server logs
* Troubleshooting service failures
* Investigating reported incidents
* Restoring services
* Documenting technical findings
* Maintaining the project with Git and GitHub

The environment currently runs locally using **Ubuntu Linux on WSL2** and is designed to be extended later to a cloud/VPS environment.

---

## Project Scenario

ApexCare Solutions requires a reliable internal web server for its company website.

As the technical support engineer, the responsibilities in this lab include:

1. Preparing the Linux environment
2. Installing and managing Nginx
3. Creating and deploying the company website
4. Configuring an Nginx virtual host
5. Configuring local hostname resolution
6. Verifying network connectivity
7. Monitoring system and service health
8. Investigating website and server incidents
9. Analyzing Nginx logs
10. Recovering failed services
11. Documenting troubleshooting activities
12. Maintaining the project using Git and GitHub

---

## Objectives

The main objectives of this project are to develop practical experience in:

* Linux server administration
* File and directory management
* Linux permissions and ownership
* Users and groups
* Process management
* Systemd service management
* Nginx administration
* Website deployment
* HTTP troubleshooting
* TCP/IP networking
* Ports and sockets
* Hostname resolution
* System monitoring
* Log analysis
* Incident management
* Root-cause investigation
* Technical documentation
* Git version control
* GitHub repository management

---

## Environment

| Component             | Technology |
| --------------------- | ---------- |
| Host Operating System | Windows    |
| Linux Environment     | WSL2       |
| Linux Distribution    | Ubuntu     |
| Web Server            | Nginx      |
| Web Content           | HTML       |
| Service Manager       | systemd    |
| Network Protocol      | TCP/IP     |
| HTTP Port             | 80         |
| Version Control       | Git        |
| Repository Hosting    | GitHub     |

---

## Architecture

```text
Windows PC
    │
    ▼
WSL2
    │
    ▼
Ubuntu Linux
    │
    ├── Nginx
    │
    ├── Networking
    │
    ├── System Monitoring
    │
    ├── Nginx Logs
    │
    └── ApexCare Website
```

---

## Website Request Flow

The website request path is:

```text
Windows Browser
       │
       ▼
apexcare.local
       │
       ▼
127.0.0.1
       │
       ▼
WSL2 / Ubuntu
       │
       ▼
Nginx
       │
       ▼
TCP Port 80
       │
       ▼
Nginx Virtual Host
       │
       ▼
/var/www/apexcare
       │
       ▼
index.html
```

---

# Website

A simple HTML website was created to represent the fictional ApexCare Solutions company.

### Source

```text
website/index.html
```

### Website Content

The website contains information about:

* Technical Support
* Linux Server Administration
* Cloud Services
* Network Troubleshooting
* Company information
* Contact information

The deployed website is accessible locally through:

```text
http://apexcare.local
```

---

# Nginx Web Server

Nginx was installed and configured as the web server for ApexCare Solutions.

The website uses an Nginx virtual host configuration.

### Virtual Host

```text
/etc/nginx/sites-available/apexcare
```

### Configuration

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name apexcare.local;

    root /var/www/apexcare;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

### Key Configuration Components

**listen 80**

Nginx listens for HTTP traffic on TCP port 80.

**listen [::]:80**

Allows Nginx to listen for HTTP traffic using IPv6.

**server_name apexcare.local**

Defines the hostname associated with the ApexCare virtual host.

**root /var/www/apexcare**

Defines the directory containing the deployed website.

**index index.html**

Defines the default page served when the website root is requested.

**try_files $uri $uri/ =404**

Checks whether the requested resource exists and returns `404 Not Found` when it does not.

---

# Website Deployment

The website was deployed to the Nginx web root:

```text
/var/www/apexcare
```

The deployment process included:

1. Creating the web root
2. Copying the website files
3. Creating the Nginx virtual host
4. Enabling the virtual host
5. Testing the Nginx configuration
6. Reloading Nginx
7. Verifying the service
8. Verifying port 80
9. Testing hostname resolution
10. Testing the website with curl
11. Testing the website from a Windows browser

Detailed deployment documentation is available in:

```text
nginx/deployment.md
```

---

# Networking

The project includes practical networking troubleshooting and investigation.

Topics covered include:

* IPv4 addressing
* Loopback addressing
* Localhost
* TCP ports
* Listening sockets
* Default routes
* Connectivity testing
* Hostname resolution
* Local hosts files
* HTTP connectivity
* Windows-to-WSL connectivity

The ApexCare hostname:

```text
apexcare.local
```

was mapped to:

```text
127.0.0.1
```

This mapping was configured in both the WSL and Windows hosts files to allow the website to be accessed from the Windows browser.

---

# System Monitoring

Linux system resources were monitored using command-line tools.

The monitoring activities included:

* CPU utilization
* Memory utilization
* Swap usage
* System load
* Running processes
* Nginx worker processes
* Disk usage
* Service status
* Network listening ports
* Nginx logs

The project also included investigations where system performance was checked to determine whether reported website problems were caused by server resource exhaustion.

---

# Nginx Monitoring and Logs

Nginx service health was monitored using systemd and Linux command-line tools.

Important logs investigated include:

### Access Log

```text
/var/log/nginx/access.log
```

Used to investigate:

* HTTP requests
* Response status codes
* 200 responses
* 404 responses
* Client requests
* Request patterns

### Error Log

```text
/var/log/nginx/error.log
```

Used to investigate Nginx errors and configuration/runtime problems.

### Systemd Journal

Nginx service events were also investigated through the systemd journal.

```text
journalctl -u nginx
```

This helped identify service failures and configuration-related problems.

---

# Troubleshooting Methodology

The project follows a structured troubleshooting approach:

```text
Reported Problem
       │
       ▼
Confirm the Symptom
       │
       ▼
Check Service Health
       │
       ▼
Check Network / Port
       │
       ▼
Check Configuration
       │
       ▼
Check Website / Application
       │
       ▼
Check Logs
       │
       ▼
Identify Root Cause
       │
       ▼
Apply Resolution
       │
       ▼
Retest
       │
       ▼
Document Findings
```

This approach is intended to prevent assumptions and ensure that troubleshooting is based on evidence.

---

# Incident Management

Six troubleshooting incidents have been intentionally created and documented to simulate real Technical Support cases.

---

## Incident 001 — Nginx Service Failure

### Scenario

The ApexCare website became unavailable.

### Investigation

The Nginx service was checked and found to be inactive.

Port 80 was also checked and no listening Nginx process was found.

### Root Cause

Nginx had been stopped.

### Resolution

Nginx was started and the service and port were verified.

The website was then successfully accessed again.

### Documentation

```text
incidents/incident-001-nginx-service-failure.md
```

---

## Incident 002 — Incorrect Nginx Document Root

### Scenario

The website was responding but returned:

```text
404 Not Found
```

### Investigation

The Nginx configuration pointed to an incorrect document root:

```text
/var/www/apexcare123
```

The directory did not exist.

The Nginx access log confirmed the HTTP 404 response.

### Root Cause

The Nginx virtual host was configured with an incorrect document root.

### Resolution

The document root was corrected to:

```text
/var/www/apexcare
```

The configuration was tested, Nginx was reloaded, and the website was verified.

### Key Finding

A successful:

```text
nginx -t
```

does not necessarily mean that the application will work correctly.

A configuration can be syntactically valid while still containing an incorrect path or configuration value.

### Documentation

```text
incidents/incident-002-nginx-document-root.md
```

---

## Incident 003 — Website Connectivity Investigation

### Scenario

A user reported that the ApexCare website could not be accessed from their computer while other websites were working.

### Investigation

The following areas were checked:

* Nginx service
* Port 80
* Website response
* Hostname resolution
* Windows connectivity
* Ping response
* Browser access

The website successfully responded from Linux and Windows.

### Finding

The reported issue could not be reproduced during the investigation.

No server-side root cause was identified.

### Documentation

```text
incidents/incident-003.md
```

---

## Incident 004 — ApexCare Website Error

### Scenario

Users reported an error when accessing the ApexCare homepage.

### Investigation

The Nginx service, port 80, website files, configuration, and logs were investigated.

Historical access-log data showed a homepage request returning:

```text
404 Not Found
```

The Nginx configuration was also reviewed against the expected deployment configuration.

### Root Cause

A configuration change caused Nginx to serve the ApexCare homepage incorrectly, resulting in an HTTP 404 response.

### Resolution

The configuration was corrected, Nginx was reloaded, and the homepage returned successfully.

### Documentation

```text
incidents/incident-004.md
```

---

## Incident 005 — Slow Website Performance

### Scenario

Users reported that the website was loading slowly.

### Investigation

The investigation included:

* CPU utilization
* Memory utilization
* System load
* Swap usage
* Nginx service status
* HTTP response time
* Network connectivity
* Nginx logs
* Browser response

The server showed very low resource utilization.

The website returned an HTTP 200 response and responded within milliseconds during testing.

### Finding

No server-side performance problem could be identified or reproduced.

Further investigation would be required from the client side if the issue continued.

### Documentation

```text
incidents/incident-005.md
```

---

## Incident 006 — High CPU / Resource Usage Investigation

### Scenario

Users reported that the ApexCare website had become slow and suggested that high server resource usage might be responsible.

### Investigation

The following were investigated:

* CPU utilization
* Memory utilization
* System load
* Swap usage
* Running processes
* Nginx workers
* Nginx service status
* HTTP response times
* Network connectivity
* Nginx access logs
* Nginx error logs
* Systemd journal

System resources were found to be operating normally.

No process was consuming excessive CPU resources.

Website requests were returning successfully.

### Finding

No server-side root cause was identified.

The reported issue could not be reproduced during the investigation.

Further investigation should therefore focus on client-side factors such as:

* Client device
* Network connection
* Browser
* Local environment
* Other client-specific conditions

### Documentation

```text
incidents/incident-006.md
```

---

# Technical Support Skills Demonstrated

This project demonstrates practical experience with:

### Linux Administration

* Linux filesystem navigation
* File and directory management
* File permissions
* Ownership
* Users and groups
* Processes
* Services
* systemd
* Command-line troubleshooting

### Web Server Administration

* Nginx installation
* Nginx configuration
* Virtual hosts
* Web root configuration
* HTTP port configuration
* Website deployment
* Configuration validation
* Service reload and recovery

### Networking

* IPv4
* Loopback addresses
* TCP ports
* Listening sockets
* Routing
* Hostname resolution
* Hosts files
* HTTP connectivity
* Connectivity troubleshooting

### Monitoring

* CPU monitoring
* Memory monitoring
* Swap monitoring
* Process monitoring
* Service monitoring
* Port monitoring
* HTTP response-time testing
* Log monitoring

### Troubleshooting

* Incident investigation
* Evidence-based troubleshooting
* Root-cause analysis
* Service recovery
* Configuration comparison
* Log analysis
* Connectivity testing
* Performance investigation
* Client-side vs server-side diagnosis

### Documentation

* Incident reports
* Deployment documentation
* Troubleshooting procedures
* Technical findings
* Resolution documentation

### Version Control

* Git repository management
* Git commits
* Branch management
* Remote repository configuration
* SSH authentication
* GitHub repository management

---

# Git and GitHub

The project is maintained using Git and published to GitHub.

Repository:

```text
github.com/Augustine-27/apexcare-linux-server-lab
```

The repository uses:

```text
main
```

as the primary branch.

GitHub authentication was configured using an SSH key.

The repository contains the project documentation, website source, deployment documentation, and incident investigations.

---

# Project Structure

```text
apexcare-linux-server-lab/
│
├── README.md
│
├── documentation/
│
├── incidents/
│   ├── incident-001-nginx-service-failure.md
│   ├── incident-002-nginx-document-root.md
│   ├── incident-003.md
│   ├── incident-004.md
│   ├── incident-005.md
│   └── incident-006.md
│
├── linux/
│
├── monitoring/
│
├── networking/
│
├── nginx/
│   └── deployment.md
│
├── screenshots/
│
└── website/
    └── index.html
```

The currently empty directories are reserved for additional documentation and supporting project materials as the lab continues to develop.

---

# Current Project Status

## Completed

* [x] Ubuntu Linux environment
* [x] WSL2 setup
* [x] Linux filesystem practice
* [x] Linux permissions and ownership practice
* [x] Users and groups
* [x] Process management
* [x] systemd service management
* [x] Nginx installation
* [x] Nginx configuration
* [x] Website creation
* [x] Website deployment
* [x] Nginx virtual host
* [x] Port 80 configuration
* [x] Local hostname configuration
* [x] Windows-to-WSL website access
* [x] Network connectivity testing
* [x] System resource monitoring
* [x] Nginx log analysis
* [x] HTTP troubleshooting
* [x] Incident investigations 001–006
* [x] Technical incident documentation
* [x] Git repository
* [x] GitHub repository
* [x] SSH authentication to GitHub
* [x] Project pushed to GitHub

---

# Future Improvements

The project will continue to evolve toward a more realistic production-support environment.

Planned improvements include:

* [ ] Create structured Linux documentation
* [ ] Create structured networking documentation
* [ ] Create structured monitoring documentation
* [ ] Add selected project screenshots
* [ ] Add SSH server administration
* [ ] Add firewall configuration
* [ ] Add security hardening
* [ ] Add backup and recovery procedures
* [ ] Add automated monitoring
* [ ] Add additional troubleshooting scenarios
* [ ] Deploy the application to a VPS/cloud server
* [ ] Configure a public domain
* [ ] Add HTTPS/TLS
* [ ] Introduce cloud infrastructure
* [ ] Add infrastructure automation
* [ ] Expand the project into a broader Technical Support portfolio

---

# Learning Goal

The long-term goal of this project is to develop practical skills that can be demonstrated when applying for:

* Technical Support Engineer
* IT Support Engineer
* Linux Support Engineer
* Junior Linux Administrator
* Cloud Support Engineer
* Junior Systems Administrator
* Technical Operations roles

The project is intentionally built as a hands-on environment rather than a collection of theoretical notes.

Each new feature, failure scenario, troubleshooting exercise, and documentation task is intended to represent a practical support responsibility.

---

# Project Status

**Status: Active Development**

The core Linux web-server environment is operational,
the ApexCare website is deployed, six troubleshooting incidents have been documented,
and the project is maintained in Git/GitHub.The next stage is to strengthen the project's documentation 
and portfolio presentation before expanding the environment toward cloud/VPS deployment.
