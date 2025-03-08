**`cp` (copy)** aur **`mv` (move)** commands CentOS/Linux me files aur directories ko copy aur move karne ke liye use hoti hain. Inka syntax aur options kaafi simple aur straightforward hain.

---

### **`cp` Command**

- **Purpose:** Files ya directories ko copy karna.

### **Basic Syntax:**

```bash
cp [options] source destination

```

### **Examples:**

1. **Single File Copy:**
    
    ```bash
    cp file1.txt /path/to/destination/
    
    ```
    
    - `file1.txt` ko specified destination folder me copy karega.
2. **Multiple Files Copy:**
    
    ```bash
    cp file1.txt file2.txt /path/to/destination/
    
    ```
    
    - `file1.txt` aur `file2.txt` ko ek saath destination folder me copy karega.
3. **Directory Copy (Recursively):**
    
    ```bash
    cp -r directory_name /path/to/destination/
    
    ```
    
    - `r`: Directory aur uske andar ki saari files/subdirectories ko recursively copy karega.
4. **Preserve File Attributes:**
    
    ```bash
    cp -p file1.txt /path/to/destination/
    
    ```
    
    - `p`: Original file ke permissions, ownership, aur timestamps ko preserve karega.
5. **Interactive Mode:**
    
    ```bash
    cp -i file1.txt /path/to/destination/
    
    ```
    
    - `i`: Agar destination par file pehle se exist hai, to confirmation maangega.

---

### **`mv` Command**

- **Purpose:** Files ya directories ko move karna ya rename karna.

### **Basic Syntax:**

```bash
mv [options] source destination

```

### **Examples:**

1. **Move a File:**
    
    ```bash
    mv file1.txt /path/to/destination/
    
    ```
    
    - `file1.txt` ko destination par move karega (original location se delete ho jayega).
2. **Rename a File:**
    
    ```bash
    mv oldname.txt newname.txt
    
    ```
    
    - File ka naam `oldname.txt` se `newname.txt` me change karega.
3. **Move a Directory:**
    
    ```bash
    mv directory_name /path/to/destination/
    
    ```
    
    - Poore directory ko specified destination par move karega.
4. **Interactive Mode:**
    
    ```bash
    mv -i file1.txt /path/to/destination/
    
    ```
    
    - `i`: Agar destination par file pehle se exist hai, to confirmation maangega.
5. **Force Move:**
    
    ```bash
    mv -f file1.txt /path/to/destination/
    
    ```
    
    - `f`: Forcefully move karega, bina confirmation ke overwrite karega.

---

### **Key Differences Between `cp` and `mv`:**

| Feature | `cp` Command | `mv` Command |
| --- | --- | --- |
| **Action** | Copy file/directory. | Move or rename file/directory. |
| **Source File** | Original file remains. | Original file is removed. |
| **Usage** | For creating duplicates. | For relocation or renaming. |

---

### **Practical Examples:**

1. **Backup File Before Editing:**
    
    ```bash
    cp config.conf config.conf.bak
    
    ```
    
    - `config.conf` ka backup `config.conf.bak` ke naam se banayega.
2. **Move All Files to Another Directory:**
    
    ```bash
    mv *.txt /path/to/destination/
    
    ```
    
    - Current directory ke saare `.txt` files ko destination par move karega.
3. **Rename and Move Together:**
    
    ```bash
    mv file1.txt /path/to/destination/renamed_file.txt
    
    ```
    
    - `file1.txt` ko rename karke destination par `renamed_file.txt` ke naam se move karega.
4. **Preserve Attributes While Copying a Directory:**
    
    ```bash
    cp -rp directory_name /path/to/destination/
    
    ```
    
    - `r`: Recursively copy karega.
    - `p`: Permissions aur ownership preserve karega.

---

### **Tips:**

- **Backup Before Moving:** Important files ko move karte waqt backup banana zaroori hai.
- **Interactive Option:** `i` option use karna overwrite ke risk ko reduce karta hai.
- **Combine with Wildcards:** Commands ke saath `` aur `?` jaise wildcards ka use karna process ko efficient banata hai.

By mastering `cp` aur `mv`, aap CentOS/Linux me file management tasks ko efficiently handle kar sakte hain!
