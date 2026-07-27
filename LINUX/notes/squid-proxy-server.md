---
title: "Squid Proxy Server"
date: 2026-04-09
tags: [study, linux, squid, proxy, networking]
subject: "Linux Server Administration"
source: "Class Notes"
status: in-progress
---

# Squid Proxy Server

## Key Concepts
- Squid is a caching proxy server that controls and filters outbound web traffic
- Default port is `3128`
- Config file is at `/etc/squid/squid.conf`
- ACL (Access Control List) rules define what to block or allow
- `http_access deny` blocks matching ACL, `http_access allow` permits it

## Notes

### Installation & Setup

```bash
# update repos
sudo yum update

# install squid
sudo yum install squid

# check status
sudo systemctl status squid

# start and enable squid
sudo systemctl start squid
sudo systemctl enable squid

# verify squid version and build options
squid -v

# validate the squid config for syntax errors
sudo squid -k parse

# open squid port in firewall
sudo firewall-cmd --add-port 3128/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-ports
```

> [!TIP]
> Always run `sudo squid -k parse` after editing `squid.conf` to catch config errors before restarting.

---

### Block Websites by Domain

> [!NOTE]
> These methods match the exact domain. `apple.com` will block `apple.com` but NOT `www.apple.com`.
> To block all subdomains, prefix with a dot: `.apple.com`

#### Method A — Inline domains in squid.conf

```bash
sudo vim /etc/squid/squid.conf
```

Add at the top of the file:

```
acl blocked_sites dstdomain apple.com amazon.in sunbeaminfo.in
http_access deny blocked_sites
```

```bash
sudo systemctl restart squid
```

#### Method B — External blocklist file

```bash
sudo vim /etc/squid/squid.conf
```

Add at the top:

```
acl blocked_sites dstdomain "/etc/squid/blocked_sites.txt"
http_access deny blocked_sites
```

Create and populate the blocklist file:

```bash
sudo vim /etc/squid/blocked_sites.txt
```

```
.microsoft.com
.youtube.com
.apple.com
.amazon.in
```

```bash
sudo systemctl restart squid
```

> [!TIP]
> Method B is easier to maintain. You can update `blocked_sites.txt` and reload squid without touching `squid.conf`.

---

### Block Files by Extension

```bash
sudo vim /etc/squid/squid.conf
```

Add at the top:

```
acl blocked_files urlpath_regex -i \.mp3$ \.mp4$ \.torrent$
http_access deny blocked_files
```

```bash
sudo systemctl restart squid
```

> [!NOTE]
> `urlpath_regex` matches against the URL path using regex. The `-i` flag makes it case-insensitive, so `.MP3` and `.mp3` are both blocked.

## Questions / Unclear Points
- [ ] What is the difference between `dstdomain` and `url_regex` ACL types?
- [ ] How do you configure a client machine to use squid as its proxy?
- [ ] How do you view squid access logs?

## Summary
Squid is installed via `yum` and listens on port 3128. ACL rules in `squid.conf` control what gets blocked — by domain (inline or via external file) or by file extension using regex. Always validate config with `squid -k parse` before restarting.

## Related
- [[Setting Up Apache HTTP Server]]
- [[HAProxy Setup]]
- [[Firewall Configuration]]

## References
- http://www.squid-cache.org/Doc/config/
- `man squid`
