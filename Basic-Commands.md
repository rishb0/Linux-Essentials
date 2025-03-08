# **Basic Linux Commands**  

## **File and Directory Management**  

## `pwd`  
Prints the current working directory.  

**Example:**  
```
pwd
```

## `ls`  
Lists files and directories in the current directory.  
**Syntax:**  
```
ls [options] [directory]
```
**Examples:**  
- Current location available file/directory list  
  ```
  ls
  ```
- Detailed view  
  ```
  ls -l
  ```
- Show hidden files  
  ```
  ls -a
  ```
- Human-readable sizes  
  ```
  ls -lh
  ```
- Recursive listing  
  ```
  ls -R
  ```

## `cd`  
Changes the current directory.  
**Syntax:**  
```
cd [directory]
```
**Examples:**  
- Go to a specific folder  
  ```
  cd /home/user/documents
  ```
- Move up one level  
  ```
  cd ..
  ```
- Go to root  
  ```
  cd /
  ```

## `mkdir`  
Creates a new directory.  
**Syntax:**  
```
mkdir [directory_name]
```
**Examples:**  
- Create a single directory  
  ```
  mkdir new_folder
  ```
- Create nested directories  
  ```
  mkdir -p parent/child/grandchild
  ```

## `rmdir`  
Deletes an empty directory.  
**Syntax:**  
```
rmdir [directory_name]
```
**Example:**  
```
rmdir old_folder
```

## `rm`  
Removes files or directories.  
**Syntax:**  
```
rm [options] [file/directory]
```
**Examples:**  
- Remove a file  
  ```
  rm file.txt
  ```
- Remove a folder and its contents  
  ```
  rm -rf foldername
  ```

---

## **File Operations**  

## `touch`  
Creates an empty file.  
**Syntax:**  
```
touch [filename]
```
**Example:**  
```
touch myfile.txt
```

## `cat`  
Displays the contents of a file.  
**Syntax:**  
```
cat [filename]
```
**Example:**  
```
cat file.txt
```

## `cp`  
Copies files and directories.  
**Syntax:**  
```
cp [options] source destination
```
**Examples:**  
- Copy a file  
  ```
  cp file.txt /backup/
  ```
- Copy a directory  
  ```
  cp -r myfolder newfolder
  ```

## `mv`  
Moves or renames files and directories.  
**Syntax:**  
```
mv [source] [destination]
```
**Examples:**  
- Rename a file  
  ```
  mv oldname.txt newname.txt
  ```
- Move a file  
  ```
  mv file.txt /new/location/
  ```

## `ln`  
Creates links between files.  
**Syntax:**  
```
ln [options] target link_name
```
**Examples:**  
- Symbolic link  
  ```
  ln -s /path/to/file symlink
  ```
- Hard link  
  ```
  ln /path/to/file hardlink
  ```

---

## **System Information**  

## `date`  
Displays the current date and time.  
**Syntax:**  
```
date
```
**Example:**  
```
date
```

## `uptime`  
Shows how long the system has been running.  
**Syntax:**  
```
uptime
```
**Example:**  
```
uptime
```

## `uname -a`  
Displays system and kernel information.  
**Example:**  
```
uname -a
```

---

## **User and Session Information**  

## `whoami`  
Displays the currently logged-in user.  
**Example:**  
```
whoami
```

## `who`  
Lists all logged-in users.  
**Example:**  
```
who
```

## `id`  
Displays user ID and group information.  
**Syntax:**  
```
id [username]
```
**Example:**  
```
id user
```

---

## **Process and Memory Information**  

## `ps -aux`  
Lists all running processes.  
**Example:**  
```
ps -aux
```

## `top`  
Shows real-time system statistics.  
**Syntax:**  
```
top
```
**Example:**  
```
top
```

## `free -h`  
Displays memory and swap usage in a human-readable format.  
**Example:**  
```
free -h
```

---

## **System Shutdown and Reboot**  

## `shutdown`  
Shuts down or reboots the system.  
**Syntax:**  
```
shutdown [options] [time]
```
**Examples:**  
- Power off immediately  
  ```
  shutdown -P now
  ```
- Restart immediately  
  ```
  shutdown -r now
  ```
- Cancel scheduled shutdown  
  ```
  shutdown -c
  ```

## `reboot`  
Reboots the system.  
**Example:**  
```
reboot
```