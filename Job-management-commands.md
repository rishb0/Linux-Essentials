# Job-management-commands


# **1. Jobs Command**

## **Overview**

The `jobs` command is used to **display and manage background and stopped jobs** in the current shell session. It helps in **tracking active, suspended, or completed jobs**, allowing users to control processes running in the background.

---

## **Key Features**

- Lists all background and stopped jobs.
- Displays job IDs and process statuses.
- Works alongside `fg`, `bg`, `kill`, and `disown` for job control.
- Can show process IDs (PIDs) and changed job statuses.
- Only functions in interactive shell sessions.

---

## **Syntax**

```bash
jobs [options]

```

- `options` modify the output format.

---

## **Common Options**

| Option | Description |
| --- | --- |
| `-l` | Displays job IDs along with process IDs (PIDs). |
| `-n` | Shows jobs that have changed status since the last check. |
| `-p` | Displays only process IDs (PIDs) of jobs. |
| `-r` | Lists only running jobs. |
| `-s` | Shows only stopped (suspended) jobs. |

---

## **Examples**

### **1. List all background jobs**

```bash
jobs

```

**Output:**

```
[1]+  Running    long_script.sh &
[2]-  Stopped    nano notes.txt

```

- `+` → Most recent job.
- → Second most recent job.

---

### **2. Display job numbers and PIDs**

```bash
jobs -l

```

**Output:**

```
[1]+  12345 Running    long_script.sh &
[2]-  12346 Stopped    nano notes.txt

```

- Shows **job IDs** (`[1]`, `[2]`) and **PIDs** (`12345`, `12346`).

---

### **3. Show only jobs that changed status**

```bash
jobs -n

```

- Displays only jobs whose state changed since the last `jobs` command.

---

### **4. Display only running jobs**

```bash
jobs -r

```

**Output:**

```
[1]+  Running    long_script.sh &

```

- Lists only active jobs.

---

### **5. Display only stopped jobs**

```bash
jobs -s

```

**Output:**

```
[2]-  Stopped    nano notes.txt

```

- Lists jobs that are paused or suspended.

---

### **6. Display only process IDs**

```bash
jobs -p

```

**Output:**

```
12345
12346

```

- Shows only the **PIDs** of jobs.

---

## **Use Cases**

- **Tracking background processes** without switching terminals.
- **Resuming stopped jobs** using `fg %job_id` or `bg %job_id`.
- **Managing long-running tasks** efficiently.
- **Checking job statuses** before logging out or closing the session.

---

# 2. PS (Process Status) Command

The **`ps` (Process Status)** command is used to **display active processes** running on a Linux system. It provides details such as **process ID (PID), user, CPU usage, memory usage, and command execution path**.

---

## **Key Features of ps Command**

- View currently running processes
- Show detailed information like PID, user, CPU, and memory usage
- Customize output using different options
- Filter processes by user, parent process, or terminal
- Sort processes based on CPU, memory, or start time
- Display process hierarchy in tree format
- Identify high CPU or memory-consuming processes

---

## **Basic Syntax**

```
ps [options]

```

- `options` → Modify the output to display specific process details.

---

## **Examples with Output & Explanation**

### **1 Show All Running Processes**

**Command:**

```
ps -e

```

**Explanation:**

- `e` → Displays **all processes** running on the system, including those not linked to a terminal.

**Output:**

```
  PID TTY          TIME CMD
    1 ?        00:00:02 systemd
  234 ?        00:00:00 sshd
  567 ?        00:00:01 nginx
 1023 ?        00:00:03 firefox

```

**Output Breakdown:**

- **PID** → Process ID
- **TTY** → Terminal associated with the process (`?` means no terminal)
- **TIME** → CPU time used by the process
- **CMD** → Command that started the process

---

### **2 Show All Processes with Full Details**

**Command:**

```
ps -ef

```

**Explanation:**

- `e` → Show all processes
- `f` → Full-format listing with extra details

**Output:**

```
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 10:00 ?        00:00:02 /sbin/init
root       234     1  0 10:01 ?        00:00:00 /usr/sbin/sshd
user      1023   234  1 10:05 ?        00:00:03 firefox

```

**Output Breakdown:**

- **UID** → User running the process
- **PID** → Process ID
- **PPID** → Parent Process ID
- **C** → CPU utilization
- **STIME** → Process start time
- **TTY** → Terminal (if any)
- **CMD** → Command that started the process

---

### **3 Show Processes of a Specific User**

**Command:**

```
ps -u user

```

**Explanation:**

- `u user` → Displays only processes **owned by the specified user**.

**Output:**

```
  PID TTY          TIME CMD
 1023 ?        00:00:03 firefox
 1098 ?        00:00:00 gedit

```

**Output Breakdown:**

- Shows only the processes **owned by "user"**

---

### **4 Show Processes in Hierarchical Format**

**Command:**

```
ps -ef --forest

```

**Explanation:**

- `-forest` → Displays processes in a **tree structure**, showing parent-child relationships.

**Output:**

```
  PID  PPID CMD
    1     0 systemd
  234     1  \\_ sshd
 1023   234      \\_ firefox
 1098   234      \\_ gedit

```

**Output Breakdown:**

- `_` → Shows **child processes** under their **parent process**.
- `firefox` and `gedit` are running under `sshd` (process ID **234**).

---

### **5 Show a Specific Process by PID**

**Command:**

```
ps -p 1234

```

**Explanation:**

- `p <PID>` → Shows only the **specified process ID**.

**Output:**

```
  PID TTY          TIME CMD
 1234 ?        00:00:02 python3

```

**Output Breakdown:**

- Displays **only process 1234**, which is running **python3**.

---

### **6 Show Child Processes of a Specific Parent Process**

**Command:**

```
ps --ppid 1

```

**Explanation:**

- `-ppid <PID>` → Shows processes that have **PID 1** as their **parent**.

**Output:**

```
  PID TTY          TIME CMD
  234 ?        00:00:00 sshd
  567 ?        00:00:01 nginx

```

**Output Breakdown:**

- `sshd` and `nginx` are **child processes of process 1**.

---

### **7 Show Only Running Processes**

**Command:**

```
ps -r

```

**Explanation:**

- `r` → Displays **only active/running processes**, excluding sleeping processes.

**Output:**

```
  PID TTY          TIME CMD
 1023 ?        00:00:03 firefox
 2098 ?        00:00:02 chrome

```

**Output Breakdown:**

- Only shows **currently running** processes.

---

### **8 Show Process Memory Usage**

**Command:**

```
ps -eo pid,%mem,cmd --sort=-%mem

```

**Explanation:**

- `e` → Show all processes
- `o` → Customize output format
- `%mem` → Display memory usage percentage
- `-sort=-%mem` → Sort results in **descending order of memory usage**

**Output:**

```
  PID %MEM CMD
 1023  6.5 firefox
 2098  5.3 chrome
  567  2.0 nginx

```

**Output Breakdown:**

- Shows processes **sorted by memory usage** from highest to lowest.

---

### **9 Show Process CPU Usage**

**Command:**

```
ps -eo pid,%cpu,cmd --sort=-%cpu

```

**Explanation:**

- `%cpu` → Displays CPU usage percentage
- `-sort=-%cpu` → Sort results in **descending order of CPU usage**

**Output:**

```
  PID %CPU CMD
 2098 15.2 chrome
 1023 12.4 firefox
  567  2.1 nginx

```

**Output Breakdown:**

- Shows processes **sorted by CPU usage** from highest to lowest.

---

### **10 Show Only Specific Columns**

**Command:**

```
ps -eo pid,ppid,cmd

```

**Explanation:**

- `e` → Show all processes
- `o pid,ppid,cmd` → Customize output to show **PID, PPID, and command**

**Output:**

```
  PID  PPID CMD
    1     0 systemd
  234     1 sshd
 1023   234 firefox

```

**Output Breakdown:**

- Shows **only selected fields** (PID, PPID, CMD).

---

### **11 Show Processes Sorted by Start Time**

**Command:**

```
ps -eo pid,stime,cmd --sort=stime

```

**Explanation:**

- `stime` → Displays **start time of processes**
- `-sort=stime` → Sorts processes in **ascending order of start time**

**Output:**

```
  PID STIME CMD
    1 10:00 systemd
  234 10:01 sshd
 1023 10:05 firefox

```

**Output Breakdown:**

- Shows processes **sorted by start time** (oldest to newest).

---

# 3. HTOP COMMAND

## Overview

`htop` is an interactive system-monitoring tool that provides a real-time view of system processes, resource usage, and allows direct process management. It is a more advanced alternative to `top`.

---

## Key Features

- Displays CPU, memory, and swap usage in a graphical format
- Allows scrolling to view all processes
- Provides search, filtering, and sorting options
- Supports process management such as killing and renicing
- Works with both keyboard and mouse

---

## Syntax

```
htop [OPTIONS]

```

Running `htop` without any options starts the interactive system monitor.

---

## Common Options with Examples and Output

### 1. Default htop Usage

```
htop

```

**Output:**

```
  PID USER      PRI  NI  VIRT   RES   SHR S CPU% MEM%   TIME+ Command
 1234 root       20   0 123M   11M   2M  S  2.5  1.2   0:05.23 nginx
 5678 user       20   0 256M   32M   5M  R  3.8  4.5   0:15.67 firefox

```

**Explanation:**

Displays running processes along with CPU and memory usage in a graphical format.

---

### 2. Set Update Delay

```
htop -d 20

```

**Output:**

```
[Updating every 2 seconds...]

```

**Explanation:**

Changes the refresh rate of process updates to 2 seconds. The default is around 0.5 seconds.

---

### 3. Disable Color

```
htop -C

```

**Output:**

```
Monochrome mode activated...

```

**Explanation:**

Removes color formatting and runs `htop` in black-and-white mode.

---

### 4. Show Processes for a Specific User

```
htop -u root

```

**Output:**

```
  PID USER      PRI  NI  VIRT   RES   SHR S CPU% MEM%   TIME+ Command
 1234 root       20   0 123M   11M   2M  S  2.5  1.2   0:05.23 nginx
 2345 root       20   0 512M   56M   8M  R  4.2  6.8   0:20.14 apache2

```

**Explanation:**

Shows only processes belonging to the specified user.

---

### 5. Sort Processes by Memory Usage

```
htop -s MEM%

```

**Output:**

```
  PID USER      PRI  NI  VIRT   RES   SHR S CPU% MEM%   TIME+ Command
 2345 apache     20   0 512M   56M   8M  R  4.2  6.8   0:20.14 apache2
 5678 user       20   0 256M   32M   5M  R  3.8  4.5   0:15.67 firefox

```

**Explanation:**

Sorts processes in descending order based on memory usage.

---

### 6. Monitor Specific PIDs

```
htop -p 1234,5678

```

**Output:**

```
  PID USER      PRI  NI  VIRT   RES   SHR S CPU% MEM%   TIME+ Command
 1234 root       20   0 123M   11M   2M  S  2.5  1.2   0:05.23 nginx
 5678 user       20   0 256M   32M   5M  R  3.8  4.5   0:15.67 firefox

```

**Explanation:**

Shows only the specified processes by PID.

---

### 7. Display Process Tree

```
htop -t

```

**Output:**

```
|- init (1)
|-- systemd (2)
|--- sshd (2345)
|---- bash (6789)

```

**Explanation:**

Displays processes in a tree structure, showing parent-child relationships.

---

### 8. Filter Processes

```
htop --filter=nginx

```

**Output:**

```
  PID USER      PRI  NI  VIRT   RES   SHR S CPU% MEM%   TIME+ Command
 1234 root       20   0 123M   11M   2M  S  2.5  1.2   0:05.23 nginx

```

**Explanation:**

Shows only processes that match the specified name or keyword.

---

### 9. Hide Header

```
htop --no-header

```

**Output:**

```
  PID USER      PRI  NI  VIRT   RES   SHR S CPU% MEM%   TIME+ Command
 2345 root       20   0 512M   56M   8M  R  4.2  6.8   0:20.14 apache2
 5678 user       20   0 256M   32M   5M  R  3.8  4.5   0:15.67 firefox

```

**Explanation:**

Removes the CPU and memory usage bars, making the display simpler.

---

### 10. Disable Mouse Support

```
htop --no-mouse

```

**Output:**

```
Mouse interactions disabled...

```

**Explanation:**

Disables mouse support, useful in remote SSH sessions.

---

## Comparison: htop vs top

| Feature | htop | top |
| --- | --- | --- |
| Interface | Colorful, interactive | Basic, text-based |
| Scrolling | Yes | Limited |
| Mouse Support | Yes | No |
| Process Tree | Yes | No |
| Search | Yes | No |
| Kill Multiple Processes | Yes | No |

---

## Use Cases

- Monitoring system resource usage in real-time
- Finding and managing high CPU or memory-consuming processes
- Filtering processes based on user, name, or PID
- Checking process hierarchy and dependencies
