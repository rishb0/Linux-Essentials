# **ss (Socket Statistics) Command**

The **ss (Socket Statistics)** command is used to **display detailed information about network connections, listening sockets, and socket states**. It is faster than `netstat` and provides more filtering options.

---

## **Key Features**

- Faster and more efficient than `netstat`.
- Provides detailed insights into socket states.
- Supports filtering by protocol, state, and connection type.
- Displays process IDs (PIDs) and program names for sockets.
- Supports IPv4 and IPv6 connections.
- Useful for network troubleshooting and security analysis.

---

## **Basic Syntax**

```
ss [options]

```

- `options` → Modify the output to display specific connection types, states, or protocols.

---

## **Common Options and Their Descriptions**

| **Option** | **Description** |
| --- | --- |
| `-l` | Show only listening sockets. |
| `-t` | Show only TCP connections. |
| `-u` | Show only UDP connections. |
| `-a` | Show all sockets (both listening & established). |
| `-n` | Display IP addresses without resolving hostnames. |
| `-p` | Show process IDs (PIDs) and program names. |
| `-r` | Resolve service names (default behavior). |
| `-4` | Show only IPv4 sockets. |
| `-6` | Show only IPv6 sockets. |

---

## **Examples with Command Descriptions and Outputs**

### **1 Show All Sockets (Default)**

**Command:**

```
ss

```

**Description:**

Displays all active network sockets, including TCP and UDP connections.

**Output:**

```
Netid  State      Recv-Q Send-Q Local Address:Port   Peer Address:Port
tcp    ESTAB      0      0      192.168.1.10:44322   142.250.180.78:443
udp    UNCONN     0      0      192.168.1.10:68      0.0.0.0:*

```

**Explanation:**

- TCP ESTAB (Established) → A connection is active to a remote server (142.250.180.78).
- UDP UNCONN (Unconnected) → The system is waiting for a request on port 68 (used for DHCP).

---

### **2 Show Only Listening Sockets**

**Command:**

```
ss -l

```

**Description:**

Displays only sockets that are actively listening for incoming connections.

**Output:**

```
Netid  State   Recv-Q Send-Q Local Address:Port  Peer Address:Port
tcp    LISTEN  0      128    0.0.0.0:22         0.0.0.0:*
tcp    LISTEN  0      128    127.0.0.1:3306     0.0.0.0:*

```

**Explanation:**

- Port 22 (SSH) → Open for remote login.
- Port 3306 (MySQL) → Listening only on localhost, meaning external connections are blocked.

---

### **3 Show Listening TCP & UDP Sockets**

**Command:**

```
ss -ltu

```

**Description:**

Shows only listening TCP and UDP sockets.

**Output:**

```
Netid  State   Recv-Q Send-Q Local Address:Port  Peer Address:Port
tcp    LISTEN  0      128    0.0.0.0:80         0.0.0.0:*
udp    UNCONN  0      0      192.168.1.10:53    0.0.0.0:*

```

**Explanation:**

- TCP LISTEN on port 80 → Web server (HTTP) is running.
- UDP UNCONN on port 53 → A DNS resolver is waiting for queries.

---

### **4 Show Only TCP Connections**

**Command:**

```
ss -t

```

**Description:**

Shows only active TCP connections.

**Output:**

```
Netid  State      Recv-Q Send-Q Local Address:Port   Peer Address:Port
tcp    ESTAB      0      0      192.168.1.10:54231   13.227.220.41:443
tcp    TIME-WAIT  0      0      192.168.1.10:56789   142.250.183.4:443

```

**Explanation:**

- ESTAB (Established) → Active connection (possibly to a website).
- TIME-WAIT → The connection is closing.

---

### **5 Show Only UDP Connections**

**Command:**

```
ss -u

```

**Description:**

Shows only active UDP sockets.

**Output:**

```
Netid  State   Recv-Q Send-Q Local Address:Port  Peer Address:Port
udp    UNCONN  0      0      192.168.1.10:123    0.0.0.0:*
udp    UNCONN  0      0      192.168.1.10:5353   0.0.0.0:*

```

**Explanation:**

- Port 123 → Used for NTP (Network Time Protocol).
- Port 5353 → Used for mDNS (Multicast DNS).

---

### **6 Show All Sockets in Numeric Format**

**Command:**

```
ss -na

```

**Description:**

Disables DNS resolution and displays numeric IPs for faster output.

---

### **7 Show Listening TCP/UDP Sockets with Processes**

**Command:**

```
ss -nltup

```

**Description:**

Shows all listening TCP/UDP sockets along with process IDs (PIDs) and program names.

**Output:**

```
Netid  State   Recv-Q Send-Q Local Address:Port  Peer Address:Port  PID/Program name
tcp    LISTEN  0      128    0.0.0.0:22         0.0.0.0:*          1234/sshd
udp    UNCONN  0      0      127.0.0.1:53       0.0.0.0:*          5678/dnsmasq

```

**Explanation:**

- Port 22 (SSH) → Running under process `sshd` (PID 1234).
- Port 53 (DNS resolver) → Handled by `dnsmasq` (PID 5678).

---

### **8 Show All Active TCP/UDP Sockets with Processes**

**Command:**

```
ss -naltup

```

**Description:**

Shows both active and listening sockets with process IDs.

**Output:**

```
Netid  State    Recv-Q Send-Q Local Address:Port  Peer Address:Port  PID/Program name
tcp    LISTEN   0      128    0.0.0.0:443        0.0.0.0:*          1350/nginx
tcp    ESTAB    0      0      192.168.1.10:54231 13.227.220.41:443  2345/firefox
udp    UNCONN   0      0      127.0.0.1:53       0.0.0.0:*          5678/dnsmasq

```

**Explanation:**

- Port 443 (HTTPS) → Managed by Nginx (PID 1350).
- Active TCP connection → Firefox (PID 2345) accessing a website.

---

## **Use Cases**

- Find open and listening ports.
- Identify active network connections.
- Check which process is using a port.
- Debug network-related performance issues.
