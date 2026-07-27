# FTP Server Setup with vsftpd

## Overview

FTP (File Transfer Protocol) is used to transfer files between client and server over a network. vsftpd (Very Secure FTP Daemon) is a popular FTP server for Linux.

---

## Server Side Setup

### 1. Install vsftpd and FTP client

```bash
sudo yum update -y
sudo yum install -y vsftpd ftp
```

### 2. Create FTP User

```bash
# Create user
sudo useradd ftpuser

# Set password
echo "ftpuser:test" | sudo chpasswd

# Alternative: interactive password setting
sudo passwd ftpuser
```

### 3. Configure vsftpd

Edit the configuration file:

```bash
sudo vim /etc/vsftpd/vsftpd.conf
```

Add or modify these settings:

```conf
# Disable anonymous access
anonymous_enable=NO

# Enable local users
local_enable=YES

# Allow write operations
write_enable=YES

# Use local time
use_localtime=YES

# Jail users to their home directory
chroot_local_user=YES

# Enable chroot list (for exceptions)
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list

# Enable passive mode
pasv_enable=YES
pasv_min_port=30000
pasv_max_port=31000

# Allow writable chroot (required for newer vsftpd)
	allow_writeable_chroot=YES
```

### 4. Create chroot_list file

```bash
# Create empty chroot list file
sudo touch /etc/vsftpd/chroot_list

# Note: Users in this file are exceptions to chroot_local_user
# If chroot_local_user=YES, users in this list will NOT be jailed
# Usually leave this file empty to jail all users
```

### 5. Create Upload Directory

```bash
# Create upload folder in user's home
sudo mkdir -p /home/ftpuser/upload

# Set ownership
sudo chown -R ftpuser:ftpuser /home/ftpuser
```

### 6. Start and Enable vsftpd Service

```bash
# Enable service to start on boot
sudo systemctl enable vsftpd

# Start the service
sudo systemctl start vsftpd

# Check status
sudo systemctl status vsftpd

# Restart if needed
sudo systemctl restart vsftpd
```

### 7. Configure Firewall

```bash
# Allow FTP service
sudo firewall-cmd --permanent --add-service=ftp

# Allow passive mode ports
sudo firewall-cmd --permanent --add-port=30000-31000/tcp

# Reload firewall
sudo firewall-cmd --reload

# Verify
sudo firewall-cmd --list-services
sudo firewall-cmd --list-ports
```

---

## Client Side Setup

### 1. Install FTP Client

```bash
sudo yum update -y
sudo yum install -y ftp
```

### 2. Create Test File for Upload

```bash
# Create a test file
echo "This is a test file from client" > /tmp/client-file

# Or use vim
vim /tmp/client-file
```

### 3. Connect to FTP Server

```bash
# Connect to server
ftp <server-ip>

# Example
ftp 192.168.1.100
```

### 4. FTP Commands

```bash
# Login
ftp> user ftpuser
Password: test

# Check current directory
ftp> pwd

# List files
ftp> ls

# Change directory
ftp> cd upload

# Upload file
ftp> put /tmp/client-file

# Download file
ftp> get server-file

# Create directory
ftp> mkdir newfolder

# Delete file
ftp> delete filename

# Exit
ftp> bye
```

---

## File Transfer Examples

### Upload File from Client to Server

```bash
ftp <server-ip>
ftp> user ftpuser
ftp> cd upload
ftp> put /tmp/client-file
ftp> ls
ftp> bye
```

### Download File from Server to Client

```bash
# First, place file on server in user's home
# Server: /home/ftpuser/upload/server-file

ftp <server-ip>
ftp> user ftpuser
ftp> cd upload
ftp> get server-file
ftp> bye

# File will be downloaded to current directory on client
```

---

## Important Notes

### Chroot Jail Behavior

When `chroot_local_user=YES`:
- Users are jailed to their home directory (`/home/ftpuser`)
- They cannot access files outside their home
- Paths like `/tmp/server-file` are NOT accessible
- Files must be in `/home/ftpuser/` or subdirectories

### chroot_list File

- If `chroot_list_enable=YES` and `chroot_local_user=YES`:
  - Users in `/etc/vsftpd/chroot_list` are NOT jailed
  - Users not in the list ARE jailed
- If `chroot_list_enable=YES` and `chroot_local_user=NO`:
  - Users in `/etc/vsftpd/chroot_list` ARE jailed
  - Users not in the list are NOT jailed

### Common Mistakes

1. Forgetting `allow_writeable_chroot=YES` (causes 500 OOPS error)
2. Not opening firewall ports for passive mode
3. Trying to access `/tmp` when user is chrooted
4. Not setting correct ownership on upload directories

---

## Troubleshooting

### Check if vsftpd is running

```bash
sudo systemctl status vsftpd
sudo netstat -tulnp | grep vsftpd
```

### Check logs

```bash
sudo tail -f /var/log/vsftpd.log
sudo journalctl -u vsftpd -f
```

### Test connection locally

```bash
# On server machine
ftp localhost
```

### Verify firewall rules

```bash
sudo firewall-cmd --list-all
```

### Check SELinux (if enabled)

```bash
# Allow FTP home directories
sudo setsebool -P ftp_home_dir on

# Check SELinux status
getenforce
```

---

## Configuration Options Reference

| Option | Value | Description |
|--------|-------|-------------|
| `anonymous_enable` | NO | Disable anonymous login |
| `local_enable` | YES | Allow local users to login |
| `write_enable` | YES | Allow write operations |
| `chroot_local_user` | YES | Jail users to home directory |
| `pasv_enable` | YES | Enable passive mode |
| `pasv_min_port` | 30000 | Passive mode port range start |
| `pasv_max_port` | 31000 | Passive mode port range end |
| `allow_writeable_chroot` | YES | Allow writable chroot (required) |

---

## Quick Summary

**Server Setup:**
1. Install vsftpd
2. Create FTP user and set password
3. Edit `/etc/vsftpd/vsftpd.conf`
4. Create upload directory
5. Start vsftpd service
6. Open firewall ports

**Client Usage:**
1. Install ftp client
2. Connect using `ftp <server-ip>`
3. Login with username and password
4. Use `put` to upload files
5. Use `get` to download files
