#### **What is a User Account?**

A **user account** represents a **user** (e.g., employee) who uses the system regularly. Every person who is allowed to work on the computer must have a **unique user account**. Through this account, all activities and tasks of that person are recorded, and they are given the rights to work on the system.


- **UID (User ID)**: Every user is assigned a unique **UID** (User ID), which helps to identify them in the system.
- **User Information**: Information such as the user’s name, UID, home directory, and shell is stored in the **`/etc/passwd`** file.

---

### **Types of Users in Linux**

1. **The Root User Account**

   The **Root** user is the most powerful account in Linux. This account is created automatically during the system installation and has the highest level of privileges.
   - The **Root user** can perform any task, whether system administration or access any file or service.
   - This account should only be used for **system administration** and should not be used for everyday tasks.
   - The **Root UID** is always **0**, and it cannot be **deleted**, but it can be **disabled** if needed.

2. **The Regular User Account**

   This is a regular user account that is used by anyone who is allowed to work on the system.  
   - A **Regular user** has **moderate privileges**, meaning they can only perform tasks for which they have been granted permission.
   - These accounts are used for **routine work** and can be **disabled** or **deleted** if needed.
   - **UID** typically starts from **1000** and can go up to **10000**.

3. **The Service/System Accounts**

   **Service accounts** are created to run **services** and **processes** on the system.  
   - These accounts are not used for **routine work**. 
   - Their **UID** usually ranges from **100** to **999**.

---

### **User's Home Directory**

- **Root User's Home Directory**: The root user's home directory is **`/root`**.
- **Regular User's Home Directory**: Every regular user has a home directory, which is typically **`/home/username`**. For example, if the user’s name is `john`, their home directory will be **`/home/john`**.

---

### **UID (User ID) in Detail**

- The **Root User** has a **UID** of **0**.
- A **Regular User** typically has a **UID** starting from **1000**.
- **System Accounts** have a **UID** between **100** and **999**.


### **Files Related to Users and Groups**

1. **`/etc/passwd`**:  
   This file contains information about all users, such as their **username**, **UID**, **home directory**, and **shell**. For example:
   ```
   john:x:1001:1001:John Doe:/home/john:/bin/bash
   ```
   
2. **`/etc/group`**:  
   This file contains information about all groups, such as the **group name**, **GID** (Group ID), and the users who are part of that group. For example:
   ```
   developers:x:1002:john,jane
   ```

---

#### **What is a Group in Linux?**

A **group** is a collection of users that allows system administrators to manage users with similar permissions or access rights collectively. Instead of assigning permissions to individual users, the administrator can assign them to a group, and then apply those permissions or restrictions to the entire group.

A **group** is a collection of users that enables system administrators to apply similar permissions and restrictions to a set of users collectively. When multiple users require similar rights, they can be placed in a group, and then permissions related to those rights can be applied to the entire group.
