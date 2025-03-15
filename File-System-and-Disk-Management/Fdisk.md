# fdisk: A Deep, Unembellished Explanation of How to Manage Partitions on Linux




### What is fdisk?

`fdisk` is a utility for managing disk partitions on a Linux system. It allows users to create, delete, modify, and inspect disk partitions. The tool works with MBR (Master Boot Record) partition tables, but newer systems might use GPT (GUID Partition Table), which is handled by other utilities like `gdisk`.

### Basic Concepts

- **Disk**: A storage device like `/dev/sda`, `/dev/sdb`, etc.
- **Partition**: A subdivision of a disk. It can contain a file system or swap space. For example, `/dev/sda1` is the first partition on the first disk (`/dev/sda`).
- **MBR vs GPT**: MBR is an older partitioning scheme, while GPT is the newer and more flexible scheme.

### fdisk Command Syntax

To run `fdisk`, you need to specify the disk you want to manage. You typically do this by specifying the device path, like `/dev/sda` for the first disk.

```bash
sudo fdisk /dev/sda
```

### Main fdisk Commands

After running `fdisk`, you enter a command prompt. From here, you can use a series of commands to manipulate the partition table.

#### 1. **List Partitions (-l)**

To list all the partitions on the system, you can run:

```bash
sudo fdisk -l
```

This will display detailed information about each disk and its partitions, such as device names (e.g., `/dev/sda1`), partition sizes, types, and system flags.



#### 2. **Start fdisk on a Disk**

When you want to modify a specific disk, use:

```bash
sudo fdisk /dev/sda
```

This will open the partition table for `/dev/sda`. Once you enter the `fdisk` command for a disk, you’ll be in the interactive `fdisk` prompt.

#### 3. **Display Current Partition Table (p)**

Once inside the `fdisk` interactive mode, use the `p` command to print the partition table of the selected disk.

```bash
Command (m for help): p
```

This shows the existing partitions and their details (e.g., partition number, size, type).

#### 4. **Create a New Partition (n)**

To create a new partition, use the `n` command:

```bash
Command (m for help): n
```

You will be prompted to provide the following details:
- **Partition type**: primary or extended. Most of the time, you'll choose primary.
- **Partition number**: The number for the new partition. If you're creating the first partition, it'll be 1, the second will be 2, and so on.
- **First sector**: The starting point for the partition. You can press Enter to accept the default.
- **Last sector**: The endpoint for the partition. Again, pressing Enter will set it to the default, which will take up all the remaining space.

After completing the prompts, the partition is created, but the changes aren’t written to disk until you save them.

#### 5. **Delete a Partition (d)**

If you need to delete an existing partition, use the `d` command:

```bash
Command (m for help): d
```

You’ll be asked for the partition number. Once you provide it, the partition will be marked for deletion, but the actual changes won't happen until you write the changes to the disk.

#### 6. **Change Partition Type (t)**

If you need to change the partition type (e.g., from Linux filesystem to swap), you can use the `t` command:

```bash
Command (m for help): t
```

You’ll be prompted for the partition number and the type. For example, `82` is for Linux swap, and `83` is for Linux filesystem.

#### 7. **Write Changes to Disk (w)**

Once you're done making changes, you must write those changes to the disk. Use the `w` command:

```bash
Command (m for help): w
```

This will write the partition table to the disk and exit `fdisk`.

#### 8. **Quit Without Saving (q)**

If you decide to exit `fdisk` without making any changes, use the `q` command:

```bash
Command (m for help): q
```

This will quit `fdisk` without saving any modifications.

#### 9. **Print Partition Table Again (p)**

If at any time you want to see the partition table after making changes, you can use the `p` command again.

#### 10. **Help (m)**

To view all available commands in `fdisk`, type `m`:

```bash
Command (m for help): m
```

This will list all the available commands and their descriptions.

### Partition Types and Codes

Each partition has a type code associated with it. Some of the common ones are:
- `83` – Linux
- `82` – Linux swap
- `7` – NTFS (used by Windows)
- `a5` – FreeBSD
- `8e` – Linux LVM (Logical Volume Manager)

You can change the partition type using the `t` command and entering the type code.

### Example of a Simple Workflow

1. Start `fdisk` on the desired disk:

   ```bash
   sudo fdisk /dev/sda
   ```

2. Print the partition table:

   ```bash
   Command (m for help): p
   ```

3. Create a new partition:

   ```bash
   Command (m for help): n
   ```

4. Choose the default options for the partition (first sector, last sector, etc.).

5. Write the changes:

   ```bash
   Command (m for help): w
   ```

6. Exit `fdisk`:

   ```bash
   Command (m for help): q
   ```

---

### Additional Considerations

- **Backup**: Always make sure you have a backup before modifying partitions, as data loss is possible if mistakes are made.
- **Partitioning Scheme**: If you're working with GPT (instead of MBR), `fdisk` will not be sufficient. Use `gdisk` or `parted` for GPT disks.
- **Formatting**: After creating or modifying a partition, you will typically need to format it with a filesystem (like `ext4`, `xfs`, etc.) using a tool like `mkfs`


<p/>



# Managing disks in Linux involves tasks such as viewing disk information, partitioning, creating filesystems, and monitoring disk usage. Here's a concise guide to these essential operations

**1. Viewing Disk Information:**

To list all available block devices and their partitions:

```bash
lsblk
```

This command displays a tree-like structure of your storage devices, including their mount points.

**2. Viewing Disk Usage:**

To check disk space usage:

```bash
df -h
```

The `-h` flag presents the output in a human-readable format (e.g., GB, MB).

**3. Viewing Disk Partitions:**

To list all partitions:

```bash
fdisk -l
```

This command provides detailed information about each partition on your system.

**4. Creating a New Partition:**

To create a new partition on a disk (e.g., `/dev/sda`):

```bash
sudo fdisk /dev/sda
```

Within the `fdisk` prompt:

- Type `n` to create a new partition.
- Choose `p` for primary or `e` for extended.
- Specify the partition number, first sector, and last sector or size.
- Type `w` to write changes and exit.

**5. Creating a Filesystem:**

After creating a partition (e.g., `/dev/sda1`), format it with a filesystem:

```bash
sudo mkfs.ext4 /dev/sda1
```

Replace `ext4` with your desired filesystem type (e.g., `ext3`, `xfs`).

**6. Mounting a Partition:**

To mount a partition to a directory:

```bash
sudo mount /dev/sda1 /mnt
```

Replace `/mnt` with your target directory.

**7. Checking Filesystem Consistency:**

To check and repair a filesystem:

```bash
sudo fsck /dev/sda1
```

This command scans and fixes filesystem errors on the specified partition.

**8. Monitoring Disk I/O:**

To monitor disk input/output operations:

```bash
iostat -x 1
```

The `-x` flag provides extended statistics, and `1` sets the interval in seconds.

**9. Viewing Disk Health:**

To check the health of a disk:

```bash
sudo smartctl -a /dev/sda
```