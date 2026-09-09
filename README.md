# ApexCare Solutions — Linux Server & Technical Support Lab

## Project Overview

This project simulates the work of a Junior Linux / Technical Support Engineer supporting the infrastructure of a fictional company, **ApexCare Solutions**.

The project demonstrates Linux server administration, web server deployment, networking, monitoring, troubleshooting, incident management, and technical documentation.

The environment is built using **Ubuntu Linux running on WSL2**.

---

## Project Objectives

The main objectives of this project are to:

- Deploy and configure a Linux web server
- Install and administer Nginx
- Deploy a company website
- Configure an Nginx virtual host
- Configure local hostname resolution
- Monitor Linux services and system resources
- Troubleshoot service and application failures
- Investigate Nginx logs
- Perform root-cause analysis
- Document technical incidents
- Build practical Technical Support experience
- Prepare the project for GitHub and portfolio presentation

---

## Environment

| Component | Technology |
|---|---|
| Host Operating System | Windows |
| Linux Environment | WSL2 |
| Linux Distribution | Ubuntu |
| Web Server | Nginx |
| Website | HTML |
| Service Manager | systemd |
| Networking | TCP/IP |
| Monitoring | Linux command-line tools |

---

## Architecture

```text
Windows PC
    │
    ▼
WSL2
    │
    ▼
Ubuntu Linux Server
    ├── Nginx
    ├── Networking
    ├── System Monitoring
    └── ApexCare Website

## Website Request flow
Windows Browser
       │
       ▼
apexcare.local
       │
       ▼
127.0.0.1
       │
       ▼
Nginx
       │
       ▼
Port 80
       │
       ▼
/var/www/apexcare
       │
       ▼
index.html

# Website
The project includes a simple company website representing ApexCare Solutions.

Website source:

website/index.html

The website contains information about:

Technical Support
Linux Server Administration
Cloud Services
Network Troubleshooting
Company information
Contact information

# Nginx Configuration
Nginx was installed and configured as the web server for ApexCare Solutions.

The website uses an Nginx virtual host with the following configuration:

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
Important Configuration Components

listen 80

Nginx listens for HTTP traffic on TCP port 80.

server_name apexcare.local

Defines the hostname associated with the website.

root /var/www/apexcare

Defines the directory containing the website files.

index index.html

Specifies the default page to serve.

try_files $uri $uri/ =404

Checks whether the requested file or directory exists. If it does not exist, Nginx returns a 404 error.

# Website Deployment
The ApexCare Solutions website was deployed to the Ubuntu Linux server and configured to be served through Nginx.

# Deployment Process
website/index.html

# The nginx web root was created
sudo mkdir -p /var/www/apexcare
-p means parents. It allows mkdir to create the required parent directories if necessary and avoids an error if the directory already exists.
# The website was copied into the Nginx web root:
sudo cp website/index.html /var/www/apexcare/
cp means copy.

# The deployed file was verified:

ls -l /var/www/apexcare/

# The Nginx virtual host was created:

/etc/nginx/sites-available/apexcare

# The virtual host was enabled using a symbolic link:
The virtual host was enabled using a symbolic link:sudo ln -s /etc/nginx/sites-available/apexcare /etc/nginx/sites-enabled/apexcare
ln means link.

-s means symbolic, creating a symbolic link rather than a physical copy of the configuration file.
# The Nginx configuration was tested:

sudo nginx -t

-t means test. It checks the Nginx configuration for syntax and configuration errors without starting the service.
 
# Nginx was then reloaded:
sudo systemctl reload nginx

# Finally, the website was tested:
curl http://apexcare.local

# Local Hostname Configuration

** Because apexcare.local is a local development hostname, it was mapped to the local machine.

WSL Hosts File

# The following entry was added to the WSL /etc/hosts file:
127.0.0.1 apexcare.local

# Windows Hosts File

The same hostname was added to the Windows hosts file:

127.0.0.1 apexcare.local

# This allowed the Windows browser to resolve:

apexcare.local

to the local machine.

# The website was then accessible from the Windows browser at:

http://apexcare.local

Troubleshooting Demonstrations
Incident 001 — Nginx Service Failure

The Nginx service was intentionally stopped to simulate a website outage.

Symptoms

The website became unavailable:

http://apexcare.local

A curl request returned a connection failure.

# Investigation

Nginx service status was checked:

sudo systemctl status nginx

The service showed:

Active: inactive (dead)

Port 80 was also checked:

sudo ss -tulnp | grep :80

No listening process was found.

# Root Cause

Nginx had been stopped.

Resolution

Nginx was started:

sudo systemctl start nginx

The service and port were then verified.

The website successfully returned its HTML content.

# Documentation

Full incident report:

incidents/incident-001-nginx-service-failure.md
Incident 002 — Incorrect Nginx Document Root

The Nginx document root was intentionally changed to a directory that did not exist.

Symptoms

Nginx remained operational, but the website returned:

404 Not Found
Investigation

# The configured directory was checked:

ls -ld /var/www/apexcare123

The directory did not exist.

The Nginx access log was also checked:

sudo tail -n 10 /var/log/nginx/access.log

The log showed an HTTP 404 response.

# Root Cause

The Nginx virtual host pointed to the wrong document root:

/var/www/apexcare123

instead of:

/var/www/apexcare
Resolution

The document root was corrected.

The configuration was tested:

sudo nginx -t

Nginx was reloaded:

sudo systemctl reload nginx

The website was then verified using curl and the Windows browser.

Key Finding

A successful:

sudo nginx -t

does not guarantee that the website will work.

The configuration can be syntactically valid while still pointing to an incorrect or missing directory.

# Documentation

Full incident report:

incidents/incident-002-nginx-document-root.md
Technical Support Skills Demonstrated

This project demonstrates practical experience with:

Linux administration
Nginx administration
Web server deployment
Linux service management
HTTP troubleshooting
TCP/IP networking
Port troubleshooting
DNS/hostname resolution
Log analysis
Root-cause analysis
Incident management
Configuration management
Command-line troubleshooting
Technical documentation
Service recovery
Project Structure
apexcare-linux-server-lab/
│
├── README.md
│
├── documentation/
│
├── incidents/
│   ├── incident-001-nginx-service-failure.md
│   └── incident-002-nginx-document-root.md
│
├── linux/
│
├── monitoring/
│
├── networking/
│
├── nginx/
│
├── screenshots/
│
└── website/
    └── index.html
# Future Improvements

# The project will continue to be expanded with:

Linux system monitoring
CPU, memory and disk monitoring
Nginx log monitoring
Additional troubleshooting incidents
Network troubleshooting scenarios
Linux permissions and security
SSH administration
Firewall configuration
Automated monitoring
Backup and recovery procedures
Git version control
GitHub publication
Portfolio documentation
Cloud/VPS deployment
Project Status

Current Status: Active Development

Completed
✅ Ubuntu Linux environment
✅ Nginx installation
✅ Website creation
✅ Website deployment
✅ Nginx virtual host configuration
✅ Local hostname configuration
✅ Browser verification
✅ Incident 001 — Nginx service failure
✅ Incident 002 — Incorrect document root
✅ Incident documentation
Next
⬜ Linux system monitoring
⬜ Nginx log monitoring
⬜ Additional troubleshooting scenarios
⬜ Security configuration
⬜ Git/GitHub
⬜ Portfolio publication
⬜ Cloud/VPS deployment
