# Linux Users, Groups & Permissions

## Users

### User Management Commands

```bash
# Add a new user
sudo useradd username
sudo useradd -m username          # Create home directory
sudo useradd -m -s /bin/bash username  # Specify shell
sudo adduser username             # Interactive user creation (Debian/Ubuntu)

# Add user with specific UID
sudo useradd -u 1500 username

# Set/change user password
sudo passwd username

# Delete a user
sudo userdel username
sudo userdel -r username          # Remove home directory too

# Modify user
sudo usermod -l newname oldname   # Change username
sudo usermod -d /new/home username  # Change home directory
sudo usermod -s /bin/zsh username # Change shell

# Lock/unlock user account
sudo usermod -L username          # Lock
sudo usermod -U username          # Unlock

# View user information
id username
whoami                            # Current user
who                               # Logged in users
w                                 # Who is logged in and what they're doing
```

### User Files

```bash
/etc/passwd     # User account information
/etc/shadow     # Encrypted passwords
/etc/group      # Group information
/etc/gshadow    # Secure group information
```

### /etc/passwd format
```
username:x:UID:GID:comment:home_directory:shell
```

---

## Groups

### Group Management Commands

```bash
# Create a new group
sudo groupadd groupname
sudo groupadd -g 1500 groupname   # With specific GID

# Delete a group
sudo groupdel groupname

# Modify group
sudo groupmod -n newname oldname  # Rename group

# Add user to group
sudo usermod -aG groupname username
sudo gpasswd -a username groupname

# Remove user from group
sudo gpasswd -d username groupname

# View groups
groups                            # Current user's groups
groups username                   # Specific user's groups
cat /etc/group                    # All groups
```

### Primary vs Secondary Groups

```bash
# Change user's primary group
sudo usermod -g groupname username

# Add user to secondary groups
sudo usermod -aG group1,group2 username
```

---

## File Permissions

### Permission Types

```
r = read    (4)
w = write   (2)
x = execute (1)
```

### Permission Format

```
-rwxrwxrwx
│││││││││└─ Others execute
││││││││└── Others write
│││││││└─── Others read
││││││└──── Group execute
│││││└───── Group write
││││└────── Group read
│││└─────── Owner execute
││└──────── Owner write
│└───────── Owner read
└────────── File type (- file, d directory, l link)
```

### chmod - Change Permissions

**Symbolic mode:**
```bash
chmod u+x file        # Add execute for user
chmod g-w file        # Remove write for group
chmod o+r file        # Add read for others
chmod a+x file        # Add execute for all
chmod u=rwx,g=rx,o=r file  # Set specific permissions

# u = user/owner
# g = group
# o = others
# a = all
```

**Numeric mode:**
```bash
chmod 755 file        # rwxr-xr-x
chmod 644 file        # rw-r--r--
chmod 777 file        # rwxrwxrwx
chmod 600 file        # rw-------
chmod 400 file        # r--------
chmod 444 file        # r--r--r-- (read-only for everyone)
chmod 744 file        # rwxr--r-- (owner full, others read-only)
chmod 664 file        # rw-rw-r-- (owner & group read-write)
chmod 660 file        # rw-rw---- (owner & group only)

# Calculate: owner(4+2+1) group(4+0+1) others(4+0+0) = 754
```

### Common chmod Examples

| Command | Meaning |
|---------|---------|
| `chmod 444 file.txt` | Read-only for everyone |
| `chmod 777 file.txt` | Full access for everyone |
| `chmod +x file.txt` | Add execute permission |
| `chmod -x file.txt` | Remove execute permission |
| `chmod u+x file.txt` | Add execute for owner |
| `chmod g-rw file.txt` | Remove read/write for group |
| `chmod 744 file.txt` | Owner full, others read-only |
| `chmod 664 file.txt` | Owner & group read-write |
| `chmod 660 file.txt` | Owner & group only |

**Recursive:**
```bash
chmod -R 755 directory
```

### chown - Change Ownership

```bash
# Change owner
sudo chown newowner file

# Change owner and group
sudo chown newowner:newgroup file

# Change only group
sudo chown :newgroup file

# Recursive
sudo chown -R user:group directory
```

### chgrp - Change Group

```bash
sudo chgrp groupname file
sudo chgrp -R groupname directory
```

---

## Special Permissions

### SUID (Set User ID) - 4

Allows file to be executed with owner's permissions.

```bash
chmod u+s file
chmod 4755 file

# Example: /usr/bin/passwd has SUID
-rwsr-xr-x
```

### SGID (Set Group ID) - 2

- On files: Execute with group's permissions
- On directories: New files inherit directory's group

```bash
chmod g+s file
chmod 2755 directory

# Display
-rwxr-sr-x
```

### Sticky Bit - 1

On directories: Only owner can delete their files (like /tmp).

```bash
chmod +t directory
chmod 1777 directory

# Display
drwxrwxrwt
```

### Combined Special Permissions

```bash
chmod 4755 file       # SUID + 755
chmod 2755 directory  # SGID + 755
chmod 1777 directory  # Sticky + 777
chmod 6755 file       # SUID + SGID + 755
```

---

## umask - Default Permissions

```bash
# View current umask
umask

# Set umask
umask 022             # Default: 755 for dirs, 644 for files
umask 077             # Restrictive: 700 for dirs, 600 for files

# How it works:
# Files: 666 - umask
# Directories: 777 - umask
```

---

## Access Control Lists (ACL)

Extended permissions beyond standard user/group/others.

```bash
# View ACL
getfacl file

# Set ACL
setfacl -m u:username:rwx file       # User permission
setfacl -m g:groupname:rx file       # Group permission
setfacl -m o::r file                 # Others permission

# Remove ACL
setfacl -x u:username file
setfacl -b file                      # Remove all ACLs

# Recursive
setfacl -R -m u:username:rwx directory

# Default ACL for directories
setfacl -d -m u:username:rwx directory
```

---

## sudo - Superuser Privileges

```bash
# Run command as root
sudo command

# Run command as another user
sudo -u username command

# Switch to root shell
sudo -i
sudo su

# Edit sudoers file (safe way)
sudo visudo
```

### /etc/sudoers format

```bash
# User privilege specification
username ALL=(ALL:ALL) ALL

# Allow user to run specific commands
username ALL=/usr/bin/apt, /usr/bin/systemctl

# Allow group
%groupname ALL=(ALL:ALL) ALL

# No password required
username ALL=(ALL) NOPASSWD: ALL
```

---

## Common Permission Scenarios

```bash
# Web server files
chmod 644 file.html               # Files readable by all
chmod 755 directory               # Directories executable by all

# Scripts
chmod 755 script.sh               # Executable by all
chmod 700 script.sh               # Executable by owner only

# Sensitive files
chmod 600 private_key             # Owner read/write only
chmod 400 config.conf             # Owner read only

# Shared directory
chmod 770 shared_dir              # Owner and group full access
sudo chgrp teamgroup shared_dir
chmod g+s shared_dir              # SGID for group inheritance

# Public upload directory
chmod 1777 upload_dir             # All can write, only owner can delete
```

### Example Workflow: Setting up a shared project directory

```bash
# Create a group for the team
sudo groupadd dev

# Add user to the group
sudo adduser ali
sudo usermod -aG dev ali

# Change group ownership of project files
sudo chgrp dev notes.txt

# Set permissions (owner & group read-write)
chmod 660 notes.txt

# For a directory with SGID (new files inherit group)
sudo chgrp dev /project
chmod 2770 /project
```

---

## Troubleshooting

```bash
# Find files by permission
find /path -perm 777
find /path -perm /u+s             # Find SUID files

# Find files by owner
find /path -user username
find /path -group groupname

# Check effective permissions
namei -l /path/to/file

# View who can access a file
ls -l file
getfacl file
```

---

## Best Practices

- Never use 777 permissions unless absolutely necessary
- Use groups for shared access instead of 777
- Regularly audit SUID/SGID files
- Use ACLs for complex permission requirements
- Keep sensitive files with 600 or 400 permissions
- Use sudo instead of logging in as root
- Document custom permission schemes
- Test permissions with a non-privileged user
