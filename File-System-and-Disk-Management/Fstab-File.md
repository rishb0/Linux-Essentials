# FSTAB FILE CONFIGURATION

**The `/etc/fstab` file defines how disk partitions, block devices, and remote filesystems should be mounted at system boot.**

---

## Basic Fstab Entry Structure

```
<device>  <mount_point>  <filesystem_type>  <options>  <dump>  <pass>
```

### Entry Components Explained:

1. **`<device>`**:
   - Identifies the filesystem to mount
   - Formats:
     - `/dev/sdXn`
     - `UUID=xxxxxxxx`
     - `LABEL=label_name`
     - Network path

2. **`<mount_point>`**:
   - Directory where device will be mounted
   - Examples:
     - `/`
     - `/home`
     - `/mnt/data`
     - `/media/external`

3. **`<filesystem_type>`**:
   - Filesystem type
   - Common types:
     - `ext4`
     - `xfs`
     - `btrfs`
     - `ntfs`
     - `vfat`
     - `nfs`
     - `cifs`

4. **`<options>`**:
   **Mounting Options:**
   - `defaults`: Standard options
   - `ro`: Read-only
   - `rw`: Read-write
   - `noauto`: Won't mount at boot
   - `user`: Non-root mount
   - `noexec`: Prevent binary execution
   - `noatime`: No access time updates
   - `sync`: Synchronous writes
   - `async`: Asynchronous writes

5. **`<dump>`**:
   - `dump` backup utility
   - `0`: No backup
   - `1`: Backup

6. **`<pass>`**:
   - Filesystem check order
   - `0`: Skip check
   - `1`: Root filesystem
   - `2`: Other filesystems

---

## Permanent Mounting Methods

### 1. Mounting by Device Name
```
/dev/sda1  /  ext4  defaults  0  1
```
- **Pros:** Simple, direct
- **Cons:** Device names can change, less reliable

### 2. Mounting by UUID
```
UUID=550e8400-e29b-41d4-a716-446655440000  /  ext4  defaults  0  1
```
- **Pros:** Persistent, unique identifier
- **Recommended Method**
- **Find UUID:**
  ```
  blkid
  ```

### 3. Mounting by Label
```
LABEL=root  /  ext4  defaults  0  1
```
- **Pros:** Human-readable
- **Set Label:**
  ```
  e2label /dev/sda1 root
  ```

---

## Filesystem Mounting Types

### 1. Local Filesystem Mounts
```
# Ext4 Filesystem
/dev/sda1  /  ext4  defaults  0  1

# XFS Filesystem
/dev/sda2  /data  xfs  defaults  0  2
```

### 2. Network Filesystem Mounts
```
# NFS Mount
192.168.1.100:/share  /mnt/network  nfs  defaults,soft,intr  0  0

# CIFS/Samba Mount
//server/share  /mnt/windows  cifs  username=user,password=pass  0  0
```

### 3. Special Filesystems
```
# Temporary RAM Filesystem
tmpfs  /tmp  tmpfs  defaults,size=2G  0  0

# Proc Filesystem
proc  /proc  proc  defaults  0  0

# Sys Filesystem
sysfs  /sys  sysfs  defaults  0  0
```

### 4. Bind Mounts
```
# Duplicate directory to another location
/home/user/data  /mnt/backup  none  bind  0  0
```

### 5. Auto Mounts
```
/media/cdrom  /mnt/cdrom  auto  noauto,user,exec  0  0
```

---

## Advanced Mounting Options

### Security Options
```
# Secure Mount
/dev/sda2  /home  ext4  nodev,nosuid,noexec  0  2
```
- `nodev`: Disable device files
- `nosuid`: Ignore setuid/setgid
- `noexec`: Prevent binary execution

### Performance Options
```
# Performance Tuning
/dev/sda3  /data  ext4  noatime,data=writeback  0  2
```
- `noatime`: Disable access time updates
- `data=writeback`: Improved write performance

---

## Special Mounting Scenarios

### Removable Media
```
/dev/sr0  /media/cdrom  iso9660  noauto,user,exec  0  0
```

### External Drives
```
/dev/sdb1  /media/usb  vfat  user,noauto,exec  0  0
```

### Remote Mounts with Authentication
```
# NFS with Kerberos
192.168.1.100:/share  /mnt/secure  nfs  sec=krb5  0  0

# CIFS with Credentials File
//server/share  /mnt/windows  cifs  credentials=/etc/samba/credentials  0  0
```

---

## Persistent Mounting Commands
### Mount All Entries
```
mount -a
```
  - If no error is shown, fstab is correct.
  - If an error appears, fix /etc/fstab before rebooting.

### Verify Configuration
```
findmnt --verify
```

---

## Best Practices

1. Always use UUID for persistent mounts
2. Backup `/etc/fstab` before editing
3. Test configurations before system-wide apply
4. Use appropriate security and performance options
5. Regularly check filesystem health

---

## Troubleshooting

- Use recovery mode for boot issues
- Temporarily comment problematic entries
- Check system logs
- Verify filesystem configurations

---
# Systemd Automounting: (Alternative to Fstab)

**Systemd offers a modern, dynamic alternative to `/etc/fstab` for managing filesystem mounts.**

## Key Advantages
- **On-Demand Mounting:** Mounts filesystems only when accessed
- **Reduced Boot Time:** Conserves system resources
- **Enhanced Reliability:** Faster recovery from mount failures
- **Detailed Logging:** Better error tracking

## Basic Systemd Mount Unit Example
```
[Unit]
Description=Mount Data Partition
DefaultDependencies=no
Before=local-fs.target

[Mount]
What=/dev/sda2
Where=/mnt/data
Type=ext4
Options=defaults

[Install]
WantedBy=multi-user.target
```

## Quick Setup

- Create Mount Unit
```
nano /etc/systemd/system/mnt-data.mount
```
- Enable and Start
```
systemctl enable mnt-data.mount
```
```
systemctl start mnt-data.mount
```

## Monitoring Commands
- Check Mount Status
```
systemctl status mnt-data.mount
```
- View Logs
```
journalctl -xe -u mnt-data.mount
```

## Comparison: Fstab vs Systemd Automount

| Feature           | Fstab           | Systemd Automount |
|------------------|-----------------|-------------------|
| Boot Performance | Static Mounting | On-Demand Mounting|
| Flexibility      | Limited         | High              |
| Error Handling   | Basic           | Advanced          |
| Logging          | Minimal         | Detailed          |

**Systemd automounting offers a more dynamic and flexible approach to filesystem management compared to traditional fstab configurations.**
