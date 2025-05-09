## Special Permissions in Linux

Special permissions in Linux extend beyond the standard **read (r)**, **write (w)**, and **execute (x)** permissions. They provide additional functionality and security features for files and directories. The three special permissions are:

1. **Setuid (SUID)**
2. **Setgid (SGID)**
3. **Sticky Bit**


---

### **Setuid (SUID)**
- **Symbol**: `s` in the **user execute position**.
- **Numeric Value**: `4` (e.g., `4755`).
- **Purpose**: When set on an **executable file**, the file runs with the **privileges of the file owner**, not the user executing it. This is useful for programs that need elevated privileges (e.g., `passwd`).
- **Example**:
  ```bash
  chmod u+s filename
  ```
  or
  ```bash
  chmod 4755 filename
  ```
- **Viewing**:
  ```bash
  ls -l filename
  ```
  **Output**:
  ```
  -rwsr-xr-x 1 owner group 4096 Jan 1 12:34 filename
  ```
  - The `s` in the user execute position indicates SUID is set.

---

### **Setgid (SGID)**
- **Symbol**: `s` in the **group execute position**.
- **Numeric Value**: `2` (e.g., `2755`).
- **Purpose**:
  - On an **executable file**: The file runs with the **privileges of the file's group**.
  - On a **directory**: New files and subdirectories created within the directory inherit the **group ID of the parent directory**, not the primary group of the user who created them.
- **Example**:
  ```bash
  chmod g+s directory
  ```
  or
  ```bash
  chmod 2755 directory
  ```
- **Viewing**:
  ```bash
  ls -l directory
  ```
  **Output**:
  ```
  drwxr-sr-x 2 owner group 4096 Jan 1 12:34 directory
  ```
  - The `s` in the group execute position indicates SGID is set.

---

### **Sticky Bit**
- **Symbol**: `t` in the **others execute position**.
- **Numeric Value**: `1` (e.g., `1755`).
- **Purpose**: When set on a **directory**, only the **file owner**, **directory owner**, or **root** can delete or rename files within the directory. This is commonly used in shared directories like `/tmp`.
- **Example**:
  ```bash
  chmod +t directory
  ```
  or
  ```bash
  chmod 1755 directory
  ```
- **Viewing**:
  ```bash
  ls -l directory
  ```
  **Output**:
  ```
  drwxr-xr-t 2 owner group 4096 Jan 1 12:34 directory
  ```
  - The `t` in the others execute position indicates the Sticky Bit is set.

---

### **Examples of Special Permissions**
- File runs with owner's privileges.
   ```bash
   chmod 4755 filename
   ```
- New files inherit the directory's group.
   ```bash
   chmod 2755 directory
   ```
   

- Only owners can delete their files in the directory.
   ```bash
   chmod 1755 directory
   ```

---


### **Numeric Representation of Special Permissions**
Special permissions are represented as a **fourth digit** in the numeric mode:
- **SUID**: `4` (e.g., `4755`)
- **SGID**: `2` (e.g., `2755`)
- **Sticky Bit**: `1` (e.g., `1755`)

You can combine them:
- SUID + SGID: `6` (e.g., `6755`)
- SUID + Sticky Bit: `5` (e.g., `5755`)
- SGID + Sticky Bit: `3` (e.g., `3755`)
- SUID + SGID + Sticky Bit: `7` (e.g., `7755`)