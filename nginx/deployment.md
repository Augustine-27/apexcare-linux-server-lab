# ApexCare Solutions — Website Deployment

## 1. Overview

This document describes the deployment of the ApexCare Solutions website on an Ubuntu Linux server running inside WSL2.

The website is served using Nginx and is accessible locally through the hostname:

`http://apexcare.local`

The deployment demonstrates a basic real-world Linux web server deployment workflow.

---

## 2. Deployment Architecture

```text
Windows PC
    |
    v
WSL2
    |
    v
Ubuntu Linux
    |
    v
Nginx
    |
    v
Port 80
    |
    v
Nginx Virtual Host
    |
    v
/var/www/apexcare
    |
    v
index.html
```

## 3. Website Source

The website source file was created inside the project directory:

```text
website/index.html
```

The website contains:

* Company introduction
* Technical Support services
* Linux Server Administration
* Cloud Services
* Network Troubleshooting
* Contact information

---

## 4. Create the Web Root

Nginx requires a directory from which it can serve website files.

The web root was created using:

```bash
sudo mkdir -p /var/www/apexcare
```

### Command Explanation

**sudo**

Runs the command with administrator privileges.

**mkdir**

Means make directory. It creates a new directory.

**-p**

Means parents. It allows `mkdir` to create any required parent directories and prevents an error if the directory already exists.

**/var/www/apexcare**

This is the directory that will contain the deployed website.

---

## 5. Deploy the Website Files

The website's `index.html` file was copied into the Nginx web root:

```bash
sudo cp website/index.html /var/www/apexcare/
```

### Command Explanation

**cp**

Means copy.

The first path:

```text
website/index.html
```

is the source file.

The second path:

```text
/var/www/apexcare/
```

is the destination directory.

After copying, the deployed file was verified:

```bash
ls -l /var/www/apexcare/
```

### Expected Result

The directory should contain:

```text
index.html
```

---

## 6. Configure the Nginx Virtual Host

The Nginx virtual host configuration was created at:

```text
/etc/nginx/sites-available/apexcare
```

The configuration is:

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

---

## 7. Understanding the Configuration

### listen 80

Tells Nginx to listen for HTTP connections on TCP port 80.

Port 80 is the standard port for normal HTTP traffic.

### listen [::]:80

Allows Nginx to listen on port 80 using IPv6.

### server_name apexcare.local

Defines the hostname associated with this website.

When a request contains:

```text
Host: apexcare.local
```

Nginx can select this virtual host.

### root /var/www/apexcare

Defines the directory containing the website files.

For example:

```text
http://apexcare.local/
```

can result in Nginx looking for:

```text
/var/www/apexcare/index.html
```

### index index.html

Specifies the default file to serve when a directory is requested.

### location /

Defines how requests beginning with `/` should be handled.

### try_files $uri $uri/ =404

Nginx checks whether the requested resource exists.

If it exists, it is served.

If it does not exist, Nginx returns:

```text
404 Not Found
```

---

## 8. Enable the Virtual Host

Nginx keeps available configurations inside:

```text
/etc/nginx/sites-available/
```

Enabled configurations are normally placed in:

```text
/etc/nginx/sites-enabled/
```

The ApexCare configuration was enabled with:

```bash
sudo ln -s /etc/nginx/sites-available/apexcare /etc/nginx/sites-enabled/apexcare
```

### Command Explanation

**ln**

Means link. It creates a link between files or directories.

**-s**

Means symbolic. It creates a symbolic link.

A symbolic link allows the enabled configuration to reference the configuration stored in `sites-available`.

The configuration was verified with:

```bash
ls -l /etc/nginx/sites-enabled/
```

---

## 9. Validate the Nginx Configuration

Before reloading Nginx, the configuration was tested:

```bash
sudo nginx -t
```

### Command Explanation

**nginx**

Runs the Nginx command-line program.

**-t**

Means test.

It checks the Nginx configuration for syntax and configuration problems.

A successful result looks similar to:

```text
syntax is ok
test is successful
```

### Important Technical Point

A successful `nginx -t` does not guarantee that the website will work correctly.

For example, the configuration can have valid syntax but still contain:

* An incorrect document root
* A missing website file
* Incorrect permissions
* Incorrect hostname configuration
* Application-level problems

Therefore, configuration testing must be followed by actual application testing.

---

## 10. Reload Nginx

After confirming that the configuration was valid, Nginx was reloaded:

```bash
sudo systemctl reload nginx
```

### Command Explanation

**systemctl**

Controls and manages services through systemd.

**reload**

Tells a running service to reload its configuration without completely stopping the service.

This is generally preferred over restarting the service when only configuration changes have been made.

---

## 11. Verify the Nginx Service

The Nginx service was checked using:

```bash
sudo systemctl status nginx
```

The expected state is:

```text
Active: active (running)
```

This confirms that the Nginx service is running.

---

## 12. Verify Port 80

Nginx listens for HTTP traffic on port 80.

The listening port was checked using:

```bash
sudo ss -tulnp | grep :80
```

### Command Explanation

**ss**

Means socket statistics. It displays information about network sockets.

**-t**

Shows TCP sockets.

**-u**

Shows UDP sockets.

**-l**

Shows listening sockets.

**-n**

Displays addresses and ports numerically instead of trying to resolve names.

**-p**

Shows the process using the socket.

**|**

This is called a pipe.

It sends the output from the command on the left to the command on the right.

**grep**

Searches/filter text.

**:80**

Filters the output for port 80.

The result should show Nginx listening on port 80.

---

## 13. Configure Local Hostname Resolution

The hostname:

```text
apexcare.local
```

needs to resolve to the local machine.

### WSL Hosts File

The following entry was added to:

```text
/etc/hosts
```

```text
127.0.0.1 apexcare.local
```

`127.0.0.1` is the IPv4 loopback address.

It refers back to the local machine.

The hostname was verified using:

```bash
getent hosts apexcare.local
```

### Expected Result

```text
127.0.0.1 apexcare.local
```

### Windows Hosts File

Because the website was also accessed from a Windows browser, the Windows hosts file was configured with:

```text
127.0.0.1 apexcare.local
```

The Windows hosts file is located at:

```text
C:\Windows\System32\drivers\etc\hosts
```

This allows Windows to resolve `apexcare.local` to the local machine.

---

## 14. Test the Website

The website was first tested from the Linux environment using:

```bash
curl http://apexcare.local
```

### Command Explanation

**curl**

A command-line tool used to make requests to web servers and retrieve responses.

The command sends an HTTP request to:

```text
http://apexcare.local
```

If the deployment is working, the HTML content of the ApexCare website is returned.

---

## 15. Browser Verification

The website was then tested from the Windows browser:

```text
http://apexcare.local
```

The ApexCare Solutions website loaded successfully.

This confirmed the complete local deployment path:

```text
Windows Browser
      |
      v
apexcare.local
      |
      v
127.0.0.1
      |
      v
WSL2 / Ubuntu
      |
      v
Nginx
      |
      v
Port 80
      |
      v
/var/www/apexcare/index.html
```

---

## 16. Deployment Verification Checklist

| Test                      | Expected Result                 | Status |
| ------------------------- | ------------------------------- | ------ |
| Website source exists     | `website/index.html` exists     | ✅      |
| Web root exists           | `/var/www/apexcare` exists      | ✅      |
| Website deployed          | `index.html` exists in web root | ✅      |
| Nginx virtual host exists | ApexCare configuration exists   | ✅      |
| Virtual host enabled      | Symbolic link exists            | ✅      |
| Nginx configuration       | Syntax test successful          | ✅      |
| Nginx service             | Active and running              | ✅      |
| Port 80                   | Nginx listening                 | ✅      |
| WSL hostname resolution   | `apexcare.local` resolves       | ✅      |
| Curl test                 | Website HTML returned           | ✅      |
| Browser test              | Website loads                   | ✅      |

---

## 17. Troubleshooting Considerations

If the website becomes unavailable, the following checks can be performed.

### Check Nginx

```bash
sudo systemctl status nginx
```

### Check Port 80

```bash
sudo ss -tulnp | grep :80
```

### Test the Website

```bash
curl http://apexcare.local
```

### Check Nginx Access Logs

```bash
sudo tail -n 10 /var/log/nginx/access.log
```

### Check Nginx Error Logs

```bash
sudo tail -n 10 /var/log/nginx/error.log
```

### Test Configuration

```bash
sudo nginx -t
```

These checks help determine whether the problem is related to:

* Service availability
* Network ports
* Nginx configuration
* Website files
* Hostname resolution
* HTTP responses
* Nginx logs

---

## 18. Deployment Result

The ApexCare Solutions website was successfully deployed on an Ubuntu Linux server running under WSL2.

Nginx was configured to serve the website through the virtual hostname:

```text
apexcare.local
```

The deployment was verified through:

* Nginx service status
* TCP port 80
* Hostname resolution
* `curl`
* Windows browser access

The deployment demonstrates a complete basic Linux web server deployment workflow from website creation through configuration, testing, and end-to-end verification.
