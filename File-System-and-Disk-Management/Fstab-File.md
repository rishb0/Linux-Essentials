
## **📝 The `/etc/fstab` File**  

The `/etc/fstab` file defines persistent mounts that remain after a reboot.

### **Example `/etc/fstab` Entry**  
```ini
/dev/sda1  /mnt/mydisk  ext4  defaults  0  2
```

### **Fields Explained**  
| **Field** | **Description** |
|-----------|----------------|
| `/dev/sda1` | Device (partition) |
| `/mnt/mydisk` | Mount point |
| `ext4` | File system type |
| `defaults` | Mount options |
| `0` | Dump backup (0 = disabled) |
| `2` | Filesystem check order |

### **Making Mounts Persistent**  

- **Edit `/etc/fstab`**  
  ```bash
  vim /etc/fstab
  ```
- **Add an entry (UUID-based)**  
  ```ini
  UUID=abcd-1234  /mnt/mydisk  ext4  defaults  0  2
  ```
- **Apply Changes Without Rebooting**  
  ```bash
  mount -a
  ```

💡 **Using UUID instead of `/dev/sdX` prevents issues when disk order changes. Find UUID with:**  
```bash
blkid
```