**Netstat Command**

## **Overview**

The `netstat` (network statistics) command is used to display **network connections, routing tables, interface statistics, and open ports**. It is useful for **troubleshooting network issues, monitoring connections, and checking which ports are in use**.

## **Key Features**

- Displays **active network connections** (TCP & UDP).
- Shows **listening ports** and **open sockets**.
- Provides **routing table information**.
- Displays **interface statistics** (packet transmission and errors).
- Supports **PID-to-process mapping** (`-p` option).
- Can **filter results** based on protocol (`-t` for TCP, `-u` for UDP).
- Works with **numeric IP addresses** (bypassing DNS resolution).
- Useful for **firewall auditing and network security monitoring**.
## **Syntax**

```bash
netstat [options]
```

## **Common Options and Their Usage**

### **1. Display Basic Network Connections**

#### **Command:**

```bash
netstat
```

#### **Description:**

- Displays all **active TCP connections** by default.

#### **Example Output:**

```
Proto Recv-Q Send-Q Local Address    Foreign Address  State  
tcp        0      0 192.168.1.10:22  203.0.113.5:54321 ESTABLISHED  
tcp        0      0 127.0.0.1:631    0.0.0.0:*        LISTEN  
```

#### **What the Output Shows:**

- `Proto`: Protocol (TCP or UDP)
- `Recv-Q` / `Send-Q`: Receive/send queue size
- `Local Address`: IP and port of the local machine
- `Foreign Address`: IP and port of the remote connection
- `State`: Connection state (e.g., LISTEN, ESTABLISHED)

---

### **2. Show All Active Connections (Listening + Established)**

#### **Command:**

```bash
netstat -a
```

#### **Description:**

- Displays **both active and listening TCP and UDP connections.**

#### **Example Output:**

```
Proto Recv-Q Send-Q Local Address    Foreign Address  State  
tcp        0      0 192.168.1.10:22  203.0.113.5:54321 ESTABLISHED  
tcp        0      0 0.0.0.0:80       0.0.0.0:*        LISTEN  
udp        0      0 0.0.0.0:68       0.0.0.0:*  
```

#### **What the Output Shows:**

- Includes **both TCP and UDP** connections.
- Shows **listening ports and established connections**.

---

### **3. Show Connections with Numeric Addresses (No DNS Resolution)**

#### **Command:**

```bash
netstat -na
```

#### **Description:**

- Same as `netstat -a` but **disables hostname resolution**, showing **IP addresses instead of domain names**.

#### **Example Output:**

```
Proto Recv-Q Send-Q Local Address    Foreign Address  State  
tcp        0      0 192.168.1.10:22  203.0.113.5:54321 ESTABLISHED  
tcp        0      0 0.0.0.0:80       0.0.0.0:*        LISTEN  
```

#### **What the Output Shows:**

- Useful when **troubleshooting DNS issues**.
- Prevents **slow output due to hostname resolution**.

---

### **4. Show Only TCP Connections**

#### **Command:**

```bash
netstat -t
```

#### **Description:**

- Displays **only TCP** connections (no UDP).

#### **Example Output:**

```
Proto Recv-Q Send-Q Local Address    Foreign Address  State  
tcp        0      0 192.168.1.10:22  203.0.113.5:54321 ESTABLISHED  
tcp        0      0 0.0.0.0:80       0.0.0.0:*        LISTEN  
```

#### **What the Output Shows:**

- Filters output to **only show TCP-based services**.

---

### **5. Show Only UDP Connections**

#### **Command:**

```bash
netstat -u
```

#### **Description:**

- Displays **only UDP** connections.

#### **Example Output:**

```
Proto Recv-Q Send-Q Local Address    Foreign Address  State  
udp        0      0 0.0.0.0:68       0.0.0.0:*  
udp        0      0 192.168.1.10:123 0.0.0.0:*  
```

#### **What the Output Shows:**

- No **connection state** since UDP is **connectionless**.
- Useful for **monitoring DNS, DHCP, and NTP services**.

---

### **6. Show Listening Ports Only**

#### **Command:**

```bash
netstat -l
```

#### **Description:**

- Displays **only listening ports**.

#### **Example Output:**

```
Proto Recv-Q Send-Q Local Address    Foreign Address  State  
tcp        0      0 0.0.0.0:22       0.0.0.0:*        LISTEN  
udp        0      0 0.0.0.0:53       0.0.0.0:*  
```

#### **What the Output Shows:**

- Helps identify **which services are running** and awaiting connections.

---

### **7. Show Listening Ports for TCP and UDP with Numeric Addresses**

#### **Command:**

```bash
netstat -ltun
```

#### **Description:**

- Displays **listening ports (TCP and UDP) with numeric IPs** (no hostname resolution).

#### **Example Output:**

```
Proto Recv-Q Send-Q Local Address    Foreign Address  State  
tcp        0      0 0.0.0.0:22       0.0.0.0:*        LISTEN  
udp        0      0 0.0.0.0:53       0.0.0.0:*  
```

#### **What the Output Shows:**

- Useful for **firewall rules and security auditing**.

---

### **8. Show Connections with Process IDs (PIDs)**

#### **Command:**

```bash
netstat -p
```

#### **Description:**

- Displays **which process (PID) is using each connection**.

#### **Example Output:**

```
Proto Recv-Q Send-Q Local Address    Foreign Address  State       PID/Program name  
tcp        0      0 192.168.1.10:22  203.0.113.5:54321 ESTABLISHED 1234/sshd  
tcp        0      0 0.0.0.0:80       0.0.0.0:*        LISTEN      5678/nginx  
```

#### **What the Output Shows:**

- Helps in **detecting malicious or unauthorized processes using the network**.

---

### **9. Show Listening Ports with PIDs and Numeric Addresses**

#### **Command:**

```bash
netstat -nltup
```

#### **Description:**

- Displays **listening ports, numeric IPs, and process IDs**.

#### **Example Output:**

```
Proto Recv-Q Send-Q Local Address    Foreign Address  State       PID/Program name  
tcp        0      0 0.0.0.0:22       0.0.0.0:*        LISTEN      1234/sshd  
udp        0      0 0.0.0.0:53       0.0.0.0:*                   2345/dnsmasq  
```

#### **What the Output Shows:**

- Useful for **firewall management and security audits**.

---

