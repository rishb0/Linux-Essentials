# File Permissions in Linux/Unix

File permissions define who can read, write, or execute a file. In Linux/Unix-like systems, file permissions are set for three different groups of users: the owner of the file, the group associated with the file, and others.

  ### Types of Permissions
   - **Read (r)**: Allows the file to be opened and read.
   - **Write (w)**: Allows modifying or deleting the file.
   - **Execute (x)**: Allows executing the file as a program.
     
  ### Categories of Users
   - **User (u)**: The owner of the file.
   - **Group (g)**: A set of users who share the same group.
   - **Others (o)**: All other users on the system.
     
  ### File Permission Format
  File permissions are often displayed as a string of characters such as:
    -**-rwxr-xr--**
    
  This string consists of 10 characters, with the following breakdown:
   - The first character represents the file type:
     - `-` for a regular file
     - `d` for a directory
     - `l` for a symbolic link
     - `b` Block device (e.g., hard drives, USB drives)
     - `c` Character device (e.g., keyboards, mice)
  
  - The remaining 9 characters represent the permissions for **user (owner)**, **group**, and **others** in the following order:
     - **User (Owner)**: The first three characters
     - **Group**: The next three characters
     - **Others**: The last three characters

  For example, `rwxr-xr--` means:
    - **User**: `rwx` (read, write, and execute permissions)
    - **Group**: `r-x` (read and execute permissions)
    - **Others**: `r--` (read permission)


  ### Numeric Representation of Permissions

  Permissions can also be represented by numeric values:
  | Permission | Numeric Value |
  |------------|---------------|
  | Read (r)   | 4             |
  | Write (w)  | 2             |
  | Execute (x)| 1             |

  Each permission type can be assigned a numeric value, and the sum of those values determines the permission setting.
  For example:
   - `rwx` = 4 + 2 + 1 = **7**
   - `r-x` = 4 + 0 + 1 = **5**
   - `r--` = 4 + 0 + 0 = **4**

  Thus, the permission `rwxr-xr--` corresponds to **755** in numeric form.

  ## Changing File Permissions
   You can use the `chmod` command to change file permissions. 

  ### Example Commands:
   - **Add execute permission for user**:

    - Set permissions to `rwxr-xr--` (755):
    
    - Set permission `rw-r--r--` (644):
    
    - Set permission `rwx------` (700) (Only the owner can read, write, and execute):
    
    - Set permission `rwxrwxrwx` (777) (Everyone has full access):
 
  - **Symbolic**: `chmod u+x file.txt` (adds execute permission to the user).

  - **Numeric**: `chmod 755 file.txt` (sets permissions to `rwxr-xr--`).

## **1.Checking File Permissions**
To check file permissions, use the ls -l command:

```bash
ls -l /path/to/file
```
Example output:

```bash
drwxr-xr-x  2 user user  4096 Feb 9 10:30 my_folder
-rw-r--r--  1 user user  1024 Feb 9 10:30 file.txt
lrwxrwxrwx  1 user user    10 Feb 9 10:30 link -> file.txt
```

## **2.Changing File Permissions**
Use the chmod command to modify file permissions:

**Symbolic Method**

```bash
chmod u+x file.txt   # Add execute permission for user
```

```bash
chmod g-w file.txt   # Remove write permission for group
```

```bash
chmod o+r file.txt   # Add read permission for others
```

```bash
chmod a+x file.txt   # Add execute permission for everyone
```

**Numeric Method**

```bash
chmod 644 file.txt   # rw-r--r--
```

```bash
chmod 755 script.sh  # rwxr-xr-x
```

```bash
chmod 777 public.sh  # rwxrwxrwx (full permissions)
```


## **3.Changing File Ownership**
Use the chown command to change the owner and group of a file:

```bash
chown username file.txt        # Change owner
```

```bash
chown username:groupname file.txt  # Change owner and group
```

## **4. Default File Permissions (umask)**
To check the current default permissions:

```bash
umask
To set a new default permission (e.g., 022 for 755 permissions):
```

```bash
umask 022
```
