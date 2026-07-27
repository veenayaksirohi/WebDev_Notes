---
title: Setting Up HAProxy Load Balancer
date: 2026-04-09
tags:
  - study
  - linux
  - haproxy
  - load-balancer
  - networking
subject: Linux Server Administration
source: Class Notes
---

# Setting Up HAProxy Load Balancer

## Key Concepts
- HAProxy is a load balancer that distributes traffic across multiple backend servers
- `roundrobin` balance method sends requests to backends in rotation
- Frontend listens for incoming requests, backends serve the actual content
- Default HAProxy config is at `/etc/haproxy/haproxy.cfg`

## Lab Setup

| Role      | IP Address      |
|-----------|-----------------|
| Frontend  | 172.16.140.211  |
| Backend 1 | 172.16.140.218  |
| Backend 2 | 172.16.140.219  |

## Notes

### Step 1 — Configure Backend Machines (both backend1 & backend2)

```bash
# update repos
sudo yum update

# install apache and vim
sudo yum install httpd vim

# create a default page to identify each backend
sudo vim /var/www/html/index.html
```

Add this content to `index.html` (change for each backend):

```html
<h1>This is backend1</h1>
```

```bash
# start and enable httpd
sudo systemctl start httpd
sudo systemctl enable httpd

# open firewall for http and https
sudo firewall-cmd --add-service http --permanent
sudo firewall-cmd --add-service https --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-services
```

---

### Step 2 — Configure HAProxy on Frontend Machine

```bash
# update repos
sudo yum update

# install haproxy
sudo yum install haproxy

# check status
sudo systemctl status haproxy

# enable and start haproxy
sudo systemctl enable --now haproxy

# open the haproxy config file
sudo vim /etc/haproxy/haproxy.cfg
```

Update the backend section in `haproxy.cfg`:

```
backend app
    balance     roundrobin
    server  app1 172.16.140.218:80 check
    server  app2 172.16.140.219:80 check
```

```bash
# restart haproxy to apply config changes
sudo systemctl restart haproxy

# debug errors if any
sudo journalctl -xeu haproxy.service

# verify haproxy is load balancing
curl localhost:5000

# open port 5000 in firewall
sudo firewall-cmd --add-port 5000/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-ports
```

> [!TIP]
> Run `curl localhost:5000` multiple times. You should see the response alternate between `backend1` and `backend2` — that confirms roundrobin is working.

> [!NOTE]
> HAProxy listens on port 5000 by default in the example config. Check the `frontend` section in `haproxy.cfg` to confirm or change the port.

## Questions / Unclear Points
- [ ] How do you configure HAProxy for HTTPS (SSL termination)?
- [ ] What other balance methods are available besides roundrobin?
- [ ] How do you set health check intervals for backend servers?

## Summary
HAProxy sits on the frontend machine and distributes incoming requests across backend servers using roundrobin. Backends run `httpd` and serve content. The key config is in `/etc/haproxy/haproxy.cfg` under the `backend` block. Firewall rules must be opened on both frontend (port 5000) and backends (http service).

## Related
- [[Setting Up Apache HTTP Server]]
- [[Linux Networking Basics]]
- [[Firewall Configuration]]

## References
- https://www.haproxy.org/download/1.5/doc/configuration.txt
- `man haproxy`
