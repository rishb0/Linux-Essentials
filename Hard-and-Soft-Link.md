### **Hard Link and Soft Link in Linux**  

In Linux, **links** are used to create references to files. There are two types:  

1️⃣ **Hard Link** → A duplicate entry pointing to the same **inode** (same data).  
2️⃣ **Soft Link (Symbolic Link)** → A shortcut pointing to the file’s **path**.  

---

## **1️⃣ Hard Link**  
- A **hard link** creates an additional name for a file.  
- Both the original and hard link share the **same inode** and data.  
- Deleting the original file **does not** affect the hard link.  

### **Command to Create a Hard Link**  
```bash
ln original_file hard_link_name
```

### **Example:**  
```bash
touch file1        # Create a file
ln file1 file1_hardlink  # Create a hard link
ls -li file1 file1_hardlink  # Check inode numbers
```
✔ Both files will have the **same inode number**, meaning they point to the same data.  

### **Delete the Original File and Check the Hard Link**  
```bash
rm file1
cat file1_hardlink  # Still accessible!
```
✔ Hard links are **independent** and persist even if the original file is deleted.  

---

## **2️⃣ Soft Link (Symbolic Link)**  
- A **soft link** is like a shortcut that points to the file’s **path**, not the data.  
- It has a **different inode** from the original file.  
- If the original file is **deleted**, the soft link **breaks** (becomes invalid).  

### **Command to Create a Soft Link**  
```bash
ln -s original_file soft_link_name
```

### **Example:**  
```bash
ln -s file1 file1_softlink
ls -l file1 file1_softlink  # Shows a symbolic link
```
✔ The soft link points to `file1` (`file1 -> file1_softlink`).  

### **Delete the Original File and Check the Soft Link**  
```bash
rm file1
cat file1_softlink  # Error: No such file or directory!
```
✔ The soft link **breaks** if the original file is removed.  

---

## **Differences Between Hard and Soft Links**
| Feature        | Hard Link | Soft Link |
|--------------|----------|----------|
| Type | Duplicate file name | Shortcut (path reference) |
| Inode Number | Same as original | Different from original |
| Works Across Filesystems | ❌ No | ✅ Yes |
| Works for Directories | ❌ No | ✅ Yes (but risky) |
| Survives Original File Deletion | ✅ Yes | ❌ No (breaks) |

---

## **Conclusion**
- ✅ **Use Hard Links** for **backup purposes** (files stay even if original is deleted).  
- ✅ **Use Soft Links** for **shortcuts and linking files across directories**.  

🚀 **Now you know how to use hard and soft links in Linux!** 💡
