
<h1 align="center">Basic Linux Commands</h1>

## `pwd`  
Prints the current working directory.  

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
- Sort by modification time  
  ```
  ls -lt
  ```
- List only directories  
  ```
  ls -d */
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
- Return to the previous directory  
  ```
  cd -
  ```
- Go to the home directory  
  ```
  cd ~
  ```

## **System Information**  

## `date`  
Displays the current date and time.  

**Example:**  
```
date
```

## `time`  
Displays the system's current time.  

**Example:**  
```
time
```

## `cal`  
Displays a calendar for the current month.  

**Example:**  
```
cal
```

## `uptime`  
Shows how long the system has been running.  

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

## `lscpu`  
Displays CPU architecture details.  
**Example:**  
```
lscpu
```

## `lsusb`  
Lists USB devices connected to the system.  
**Example:**  
```
lsusb
```

## `df -h`  
Shows disk space usage in a human-readable format.  
**Example:**  
```
df -h
```

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
- List all logged-in users
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
- ```
  id user
  ```


## **Process and Memory Information**  

## `ps -aux`  
Lists all running processes.  
**Example:**  
```
ps -aux
```

## `top`  
Shows real-time system statistics.  

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

## **Help and Documentation**  

## `man`  
Displays the manual for a command.  
**Syntax:**  
```
man [command]
```
**Example:**  
```
man ls
```

## `info`  
Provides more detailed information about a command.  
**Syntax:**  
```
info [command]
```
**Example:**  
```
info ls
```

## `help`  
Displays brief help information for built-in commands.  
**Syntax:**  
```
help [command]
```
**Example:**  
```
help cd
```

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
