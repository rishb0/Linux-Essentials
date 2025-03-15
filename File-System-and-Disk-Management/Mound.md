
## **📂 Mounting a File System**  

After creating a partition, it must be formatted and mounted for use.

### **Syntax**  
```bash
mount [options] device mount_point
```

### **Examples**  

- **Format a Partition (ext4 File System)**  
  ```bash
  mkfs.ext4 /dev/sda1
  ```

- **Create a Mount Directory**  
  ```bash
  mkdir /mnt/mydisk
  ```

- **Mount a Partition**  
  ```bash
  mount /dev/sda1 /mnt/mydisk
  ```

- **Verify Mounting**  
  ```bash
  df -h
  ```

- **Unmount a Partition**  
  ```bash
  umount /mnt/mydisk
  ```

💡 **Mounting allows access to a partition. Use `umount` before removing a disk.**
