---
title: Setting Up Apache HTTP Server
date: 2026-04-07
tags:
  - linux
  - apache
  - httpd
  - networking
subject: Linux Server Administration
source: Class Notes
---
	
# Setting Up Apache HTTP Server

## Key Concepts
- Apache HTTP Server runs as `httpd` on RHEL/Rocky Linux
- Default web root is `/var/www/html`
- Virtual hosting allows multiple websites on one server
- Firewall must be configured to allow HTTP (80) and HTTPS (443)

## Notes

### Install & Manage Apache

```bash
# update the yum repos
sudo yum update

# install apache
sudo yum install httpd

# check if apache is installed
sudo yum list installed | grep httpd

# check status
sudo systemctl status httpd

# start the server
sudo systemctl start httpd

# enable autostart on reboot
sudo systemctl enable httpd

# enable and start in one command
sudo systemctl enable --now httpd

# test if apache is serving requests
curl http://localhost
curl http://127.0.0.1
```

> [!NOTE]
> If you get `curl: (7) Failed to connect to localhost port 80: Connection refused`, the httpd service is not running. Start it with `sudo systemctl start httpd`.

---

### Configure Firewall

```bash
# open HTTP (port 80) and HTTPS (port 443)
sudo firewall-cmd --add-service http --permanent
sudo firewall-cmd --add-service https --permanent

# reload firewall to apply changes
sudo firewall-cmd --reload

# list open services
sudo firewall-cmd --list-services

# remove a service
sudo firewall-cmd --remove-service http --permanent
sudo firewall-cmd --remove-service https --permanent
sudo firewall-cmd --reload

# open specific ports instead of services
sudo firewall-cmd --add-port 80/tcp --permanent
sudo firewall-cmd --add-port 443/tcp --permanent
sudo firewall-cmd --reload

# list open ports
sudo firewall-cmd --list-ports
```

---

### Host a Website

```bash
# web root directory
cd /var/www/html

# create the default page
sudo vim index.html
```

---

### Install Console Browser (elinks)

```bash
# install EPEL repo first (extra packages for enterprise linux)
sudo yum install epel-release
sudo yum update

# install elinks
sudo yum install elinks

# open a URL in the console browser
elinks http://localhost
```

---

### Virtual Hosting

Host multiple websites on one Apache server using VirtualHost config files.

```bash
# create web root directories
sudo mkdir /var/www/website1
sudo mkdir /var/www/website2
sudo mkdir /var/www/website3

# create index pages
sudo vim /var/www/website1/index.html
sudo vim /var/www/website2/index.html
sudo vim /var/www/website3/index.html
```

Create a config file for each site in `/etc/httpd/conf.d/`:

```bash
sudo vim /etc/httpd/conf.d/website1.conf
```

```xml
<VirtualHost *:80>
  ServerName website1.local
  DocumentRoot /var/www/website1
</VirtualHost>
```

Repeat for `website2.conf` and `website3.conf`.

```bash
# restart apache to apply configs
sudo systemctl restart httpd

# debug errors if any
sudo journalctl -xeu httpd.service
```

Map domain names to localhost in `/etc/hosts`:

```bash
sudo vim /etc/hosts
```

```
127.0.0.1   website1.local
127.0.0.1   website2.local
127.0.0.1   website3.local
```

```bash
# verify each site
curl website1.local
curl website2.local
curl website3.local
```

> [!TIP]
> To access virtual hosts from your physical machine, add the VM's IP to your hosts file.
> - Linux/macOS: `sudo vim /etc/hosts`
> - Windows: `notepad C:\Windows\System32\Drivers\etc\hosts`
>
> Add: `<vm-ip-address>  website1.local`

---

### Quick Setup: Single Page Website

```bash
sudo yum update
sudo yum install httpd -y
sudo systemctl enable --now httpd
curl http://localhost
sudo vim /var/www/html/index.html
sudo firewall-cmd --add-service http --permanent
sudo firewall-cmd --add-service https --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-services
```

## Questions / Unclear Points
- [ ] What is the difference between `--add-service` and `--add-port` in firewall-cmd?
- [ ] How do SSL certificates work with virtual hosts?

## Summary
Apache (`httpd`) is installed via `yum`, managed with `systemctl`, and serves files from `/var/www/html`. Firewall rules must be opened for ports 80/443. Virtual hosting uses per-site config files in `/etc/httpd/conf.d/` with `VirtualHost` blocks, and local DNS is handled via `/etc/hosts`.

## Related
- [[Linux Networking Basics]]
- [[systemctl Commands]]
- [[Firewall Configuration]]

## References
- https://httpd.apache.org/docs/
- `man httpd`
