# Disk Partitioning and Mounting

## Key Commands Overview

| Command | Purpose |
|---------|---------|
| `lsblk` | List block devices (disks and partitions) |
| `fdisk -l` | List all disks and partition details |
| `df -h` | Show disk usage of mounted filesystems |
| `fdisk /dev/sdX` | Interactive partition editor |
| `mkfs.ext4` | Format partition with ext4 filesystem |
| `mount` | Mount a partition to a directory |
| `umount` | Unmount a partition |
| `findmnt` | Show mounted filesystems in tree view |

---

## Step 1: Check Existing Disks

```bash
# List block devices (clean tree view)
lsblk

# List all disks with partition details
sudo fdisk -l

# Show mounted filesystems and usage
df -h
```

---

## Step 2: Create Partitions with fdisk

```bash
# Open fdisk for a specific disk
sudo fdisk /dev/sdb
```

### fdisk Interactive Commands

| Key | Action |
|-----|--------|
| `m` | Show help menu |
| `p` | Print current partition table |
| `n` | Create new partition |
| `d` | Delete a partition |
| `t` | Change partition type |
| `w` | Write changes and exit |
| `q` | Quit without saving |

### Creating Two Partitions (Example)

```
# Inside fdisk prompt:

Command: n          # new partition
Partition type: p   # primary
Partition number: 1
First sector: (press Enter for default)
Last sector: +2G    # size of partition

Command: n          # new partition
Partition type: p   # primary
Partition number: 2
First sector: (press Enter for default)
Last sector: +2G    # size of partition

Command: p          # verify partition table
Command: w          # write and exit
```

### Verify Partitions Created

```bash
lsblk
sudo fdisk -l
ls /dev/sdb*        # should show sdb1, sdb2
```

---

## Step 3: Format Partitions

```bash
# Format partition 1 with ext4
sudo mkfs.ext4 /dev/sdb1

# Format partition 2 with ext4
sudo mkfs.ext4 /dev/sdb2
```

### Other Filesystem Types

```bash
sudo mkfs.ext3 /dev/sdb1    # ext3
sudo mkfs.xfs /dev/sdb1     # XFS
sudo mkfs.vfat /dev/sdb1    # FAT32
sudo mkfs.ntfs /dev/sdb1    # NTFS
```

---

## Step 4: Create Mount Points

```bash
# Create single directory
sudo mkdir /mnt/dir1

# Create multiple directories at once
sudo mkdir /mnt/{dir1,dir2}
```

---

## Step 5: Mount Partitions

```bash
# Mount partition to directory
sudo mount /dev/sdb1 /mnt/dir1
sudo mount /dev/sdb2 /mnt/dir2

# Verify mounts
df -h
lsblk
```

---

## Step 6: Persistent Mounting with /etc/fstab

Mounts done with `mount` are temporary and lost after reboot. To make them permanent, add entries to `/etc/fstab`.

```bash
sudo vim /etc/fstab
```

### /etc/fstab Format

```
<device>    <mount-point>    <filesystem>    <options>    <dump>    <pass>
```

### Example /etc/fstab Entries

```
/dev/sdb1   /mnt/dir1   ext4   defaults   0   0
/dev/sdb2   /mnt/dir2   ext4   defaults   0   0
```

### Using UUID (Recommended)

```bash
# Get UUID of partition
sudo blkid /dev/sdb1

# Use UUID in fstab (more reliable than device name)
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   /mnt/dir1   ext4   defaults   0   0
```

### fstab Options

| Option | Meaning |
|--------|---------|
| `defaults` | rw, suid, dev, exec, auto, nouser, async |
| `ro` | Read-only |
| `rw` | Read-write |
| `noauto` | Don't mount at boot |
| `user` | Allow regular users to mount |
| `nofail` | Don't fail boot if device missing |

### Apply fstab Changes

```bash
# Mount all entries in fstab
sudo mount -a

# Verify
df -h
```

---

## Unmounting

```bash
# Unmount a partition
sudo umount /mnt/dir1
sudo umount /dev/sdb1

# Verify
df -h
lsblk
```

---

## /etc/mtab vs /etc/fstab

| File | Purpose |
|------|---------|
| `/etc/fstab` | Static config — defines what to mount at boot. Edit this to make mounts permanent. |
| `/etc/mtab` | Dynamic — shows currently mounted filesystems. Updated automatically by the system, do not edit manually. |

---

## Useful Commands Reference

```bash
# List block devices
lsblk

# List block devices with filesystem info
lsblk -f

# Show disk usage
df -h

# Show all mounted filesystems in tree view
findmnt

# Find where a specific device is mounted
findmnt /dev/sdb1

# Find what is mounted at a specific path
findmnt /mnt/dir1

# Show partition details
sudo fdisk -l

# Show UUIDs of all partitions
sudo blkid

# Check filesystem for errors
sudo fsck /dev/sdb1

# Show mount points
mount | grep sdb
```

---

## Full Workflow Example

```bash
# 1. Check available disks
lsblk
sudo fdisk -l

# 2. Partition the disk
sudo fdisk /dev/sdb
# (create partitions interactively, then write with 'w')

# 3. Format partitions
sudo mkfs.ext4 /dev/sdb1
sudo mkfs.ext4 /dev/sdb2

# 4. Create mount points
sudo mkdir /mnt/{dir1,dir2}

# 5. Mount partitions
sudo mount /dev/sdb1 /mnt/dir1
sudo mount /dev/sdb2 /mnt/dir2

# 6. Verify
df -h
lsblk

# 7. Make permanent (add to /etc/fstab)
sudo vim /etc/fstab
# Add: /dev/sdb1  /mnt/dir1  ext4  defaults  0  0
# Add: /dev/sdb2  /mnt/dir2  ext4  defaults  0  0

# 8. Test fstab
sudo mount -a
df -h
```
