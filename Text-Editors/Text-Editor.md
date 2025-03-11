# **Text Editors in Linux**

Text editors are programs used to view and modify the content of files. There are different types of text editors in Linux, and each has its features. Here are three commonly used ones: **`cat`**, **`nano`**, and **`vim`**.

---

### **1. `cat` Command**

The `cat` command is used to view the content of a file. It's simple and easy to use.

#### **Syntax:**
```bash
cat filename
```

#### **Examples:**

1. View the content of a file:
   ```bash
   cat file.txt
   ```

2. Display a file with scrolling:
   ```bash
   cat file.txt | less
   ```
   or simply:
   ```bash
   less file.txt
   ```

3. Create a new file and add content:
   ```bash
   cat > file1.txt
   ```
   (Press **Ctrl + C** to save and exit.)

4. Append content to an existing file:
   ```bash
   cat >> file1.txt
   ```

5. Combine multiple files into one:
   ```bash
   cat file1.txt file2.txt > merged.txt
   ```

6. Display line numbers while viewing a file:
   ```bash
   cat -n filename
   ```

7. Show end-of-line characters:
   ```bash
   cat -e filename
   ```

---

### **2. `nano` Command**

`nano` is a simple text editor that allows you to create and edit files directly in the terminal.

#### **Syntax:**
```bash
nano filename
```

#### **Examples:**

1. Open a file in `nano`:
   ```bash
   nano file.txt
   ```

2. Save changes in `nano` (after editing):
   - Press **Ctrl + O**, then **Enter**

3. Exit `nano`:
   - Press **Ctrl + X**

4. Search for a word:
   - Press **Ctrl + W**, then type the word and press **Enter**

5. Replace a word:
   - Press **Ctrl + \**, enter the search word, then the replacement word, and confirm.

6. Cut text:
   - Press **Ctrl + K**

7. Paste text:
   - Press **Ctrl + U**

8. Undo and redo:
   - Undo: **Alt + U**
   - Redo: **Alt + E**

9. Open a file and go to a specific line:
   ```bash
   nano +10 file.txt
   ```
   (Opens `file.txt` at line 10.)

---

### **3. `vim` Command**

`vim` is a powerful text editor with multiple modes for efficient file editing.

#### **Syntax:**
```bash
vim filename
```

#### **Examples:**

1. Open a file in `vim`:
   ```bash
   vim file.txt
   ```

2. Enter **Insert Mode** to edit text:
   - Press **i** (Insert before cursor)
   - Press **a** (Append after cursor)
   - Press **o** (Open a new line below)

3. Save and exit:
   - Save: `:w`
   - Save and exit: `:wq`
   - Exit without saving: `:q!`

4. Search for a word:
   ```bash
   /word
   ```
   (Press `n` to go to the next occurrence.)

5. Replace all occurrences of a word:
   ```bash
   :%s/old/new/g
   ```

6. Undo and redo:
   - Undo: **u**
   - Redo: **Ctrl + r**

7. Copy, cut, and paste:
   - Copy (yank) a line: **yy**
   - Cut (delete) a line: **dd**
   - Paste: **p**

8. Select text in Visual Mode:
   - Press **v**, move the cursor, then press **d** (cut) or **y** (copy)

9. Run a system command inside `vim`:
   ```bash
   :!ls
   ```

10. Open `vim` with multiple files:
   ```bash
   vim file1.txt file2.txt
   ```
   (Switch between files using `:n` and `:prev`.)

---

### **Summary of Key Commands**

#### **`cat` Commands:**
- View a file: `cat filename`
- View a file with scrolling: `cat filename | less`
- Create a new file: `cat > file1.txt`
- Show line numbers: `cat -n filename`

#### **`nano` Commands:**
- Open a file: `nano filename`
- Save: **Ctrl + O**
- Exit: **Ctrl + X**
- Find: **Ctrl + W**
- Replace: **Ctrl + \**
- Undo: **Alt + U**
- Redo: **Alt + E**

#### **`vim` Commands:**
- Open a file: `vim filename`
- Save: `:w`
- Quit: `:q`
- Save and quit: `:wq`
- Undo: `u`
- Redo: `Ctrl + r`
- Copy a line: `yy`
- Cut a line: `dd`
- Paste: `p`