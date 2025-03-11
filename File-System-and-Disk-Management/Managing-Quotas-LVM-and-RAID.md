
# Quota Management in Linux

Quota management in Linux is used to restrict and monitor disk space and inode usage by users and groups on a filesystem. It helps prevent a single user or process from consuming excessive resources.

## Enabling Disk Quotas

### Install Quota Package

- **Debian-based systems:**
  ```bash
  sudo apt install quota -y
  ```

- **RHEL/CentOS:**
  ```bash
  sudo yum install quota -y
  ```

- **Fedora:**
  ```bash
  sudo dnf install quota -y
  ```

## Enable Quotas on a Filesystem

### Modify `/etc/fstab` File
Add quota options for the desired partition:
```bash
/dev/sdb1 /d1 ext4 defaults,usrquota,grpquota 0 0
```

### Remount the Filesystem
```bash
sudo mount -o remount /d1
```

## Create Quota Database
Run the following command to check and create the quota database:
```bash
sudo quotacheck -cum /home
```

### Command Breakdown:
- `c`: Create quota files
- `u`: Check user quotas
- `m`: Do not remount the filesystem as read-only

## Enable Quota
1. Initialize quotas on the filesystem:
    ```bash
    sudo quotaon /d1
    ```
2. Verify quota status:
    ```bash
    sudo quota -ap
    ```

## Additional Commands and Tools

1. **Check Block Device Information:**
    ```bash
    lsblk
    blkid
    df -h
    ```

2. **Format Filesystem:**
    ```bash
    sudo mkfs.ext4 /dev/sdb1
    sudo mkfs.xfs /dev/sdb1
    ```

3. **Quota Management Commands:**
    - `quotacheck -cum /d1`: Check and create quota files
    - `quotacheck -cugv /d2`: Check quotas for users and groups
    - `quota -ap`: Display all quotas
    - `edquota username`: Edit user quotas
    - `touch /d1/aquota.user /d1/aquota.group`: Create required quota files
    - `tune2fs -O quota /dev/sdb1`: Enable quota feature on ext4 filesystem

# Logical Volume Manager (LVM) and RAID Setup and Management

Logical Volume Manager (LVM) is a storage management solution in Linux that provides flexibility and advanced features for managing disk space. It allows dynamic resizing of partitions.

## LVM Setup and Management Guide

### Key Components of LVM
- **Physical Volume (PV):** The actual storage device (e.g., /dev/sdb, /dev/sdc).
- **Volume Group (VG):** A pool of storage created from one or more PVs.
- **Logical Volume (LV):** A partition-like structure inside a VG, where file systems are created.

## Setting Up LVM

### Step 1: Install LVM (If Not Installed)
- **Debian/Ubuntu:**
  ```bash
  apt install lvm2 -y
  ```
- **RHEL/CentOS:**
  ```bash
  yum install lvm2 -y
  ```

### Verify Installation:
- Check installed packages:
  ```bash
  rpm -qa | grep lvm2
  ```
- List package files:
  ```bash
  rpm -ql | grep lvm2
  ```
- Display package information:
  ```bash
  rpm -qi lvm2
  ```

### Disk Preparation
- Free the disk:
  ```bash
  fdisk /dev/sdb
  ```
- Create a single partition:
  ```bash
  fdisk /dev/sdb
  ```
- Check system block devices:
  ```bash
  lsblk
  ```
- View mounted filesystems:
  ```bash
  df -h
  ```
- Edit fstab (remove any unwanted entries):
  ```bash
  vim /etc/fstab
  ```

### Step 2: Create Physical Volume
- Identify available disks:
  ```bash
  lsblk
  ```
- Initialize the disk as an LVM physical volume:
  ```bash
  pvcreate /dev/sdb /dev/sdc
  ```
- Display physical volume details:
  ```bash
  pvdisplay
  ```
- Verify physical volumes:
  ```bash
  pvs
  ```

### Step 3: Create a Volume Group
- Create a volume group named `vg_data`:
  ```bash
  vgcreate vg_data /dev/sdb /dev/sdc
  ```
- Display volume group details:
  ```bash
  vgdisplay
  ```

### Step 4: Create a Logical Volume
- Create a 60 GB logical volume named `lv_storage`:
  ```bash
  lvcreate -L 60G -n lv_storage vg_data
  ```
- Check the logical volume content:
  ```bash
  lvs
  ```

### Step 5: Formatting and Mounting the LVM Partition
- Format the logical volume:
  ```bash
  mkfs.ext4 /dev/vg_data/lv_storage
  ```
- Create a mount point:
  ```bash
  mkdir /mnt/storage
  ```
- Mount the logical volume:
  ```bash
  mount /dev/vg_data/lv_storage /mnt/storage
  ```
- Verify the block devices:
  ```bash
  lsblk
  ```
- Check filesystem UUID:
  ```bash
  blkid
  ```
- Verify the mount:
  ```bash
  df -h
  ```
- Copy logs as a test:
  ```bash
  cp -vr /var/log/* /mnt/storage
  ```
- List contents:
  ```bash
  ls -lh /mnt/storage
  ```

### Resizing Logical Volumes

#### Extend an LV (Increase Size)
- Extend the logical volume by 10 GB:
  ```bash
  lvextend -L +10G /dev/vg_data/lv_storage
  ```
- Resize the filesystem:
  ```bash
  resize2fs /dev/vg_data/lv_storage
  ```
- Verify the change:
  ```bash
  df -h /mnt/storage
  ```

#### Shrink an LV (Reduce Size)
- Unmount the volume:
  ```bash
  umount /mnt/storage
  ```
- Check and reduce the filesystem:
  ```bash
  e2fsck -f /dev/vg_data/lv_storage
  resize2fs /dev/vg_data/lv_storage 15G
  ```
- Reduce the logical volume size:
  ```bash
  lvreduce -L 15G /dev/vg_data/lv_storage
  ```
- Remount the volume:
  ```bash
  mount /dev/vg_data/lv_storage /mnt/storage
  ```

### Mounting Snapshots
- Mount the snapshot:
  ```bash
  mount /dev/vg_data/lv_snapshot /mnt/snapshot
  ```
- Remove the snapshot after use:
  ```bash
  umount /dev/vg_data/lv_snapshot
  lvremove /dev/vg_data/lv_snapshot
  ```

### Removing LVM Components

#### Remove a Logical Volume
- Unmount the logical volume:
  ```bash
  umount /mnt/storage
  ```
- Remove the logical volume:
  ```bash
  lvremove /dev/vg_data/lv_storage
  ```
- Verify removal:
  ```bash
  lvdisplay
  ```


