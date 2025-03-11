# Network Diagnostic & Troubleshooting Commands

This document covers various tools and commands used for network diagnostics and troubleshooting on Linux systems.

---

## Ping

The `ping` command tests network connectivity between two devices by sending ICMP Echo Request packets and waiting for Echo Replies. It helps determine if the target is reachable and measures response time (latency) and packet loss.

> **Note:**  
> - In Windows, the default TTL starts at 128; in Linux, it starts at 64.  
> - Some servers block ping (ICMP) to prevent DDoS attacks, and many sites block ICMP traffic.  
> - Google’s DNS server (8.8.8.8) always responds to ping requests and is often used to test internet connectivity.

### Examples

- **Ping a host continuously until stopped (Ctrl + C):**

  ```
  ping 8.8.8.8
  ```

- **Ping a domain (resolves the domain’s IP and pings it):**

  ```
  ping armourinfosec.com
  ```

- **Ping using IPv6:**

  - Using the `-6` flag to force IPv6 resolution:
  
    ```
    ping -6 armourinfosec.com
    ```

  - Pinging a specific IPv6 address directly:
  
    ```
    ping 2606:4700:3030::6815:4001
    ```

- **Limit the Number of Ping Requests:**  
  Sends only 5 packets, then stops.

  ```
  ping -c 5 8.8.8.8
  ```

- **Set Packet Size:**  
  Sends packets of 1024 bytes instead of the default 56 bytes. (Maximum size may be up to 65535 bytes, but some servers like 8.8.8.8 may not reply to large packets.)

  ```
  ping -s 1024 google.com
  ```

- **Ping from a Specific Interface:**  
  Sends 4 ping packets from the `enp0s3` interface.

  ```
  ping -I enp0s3 192.168.1.1 -c 4
  ```

- **Using a Custom Payload:**  
  Fills the packet payload with a repeating hexadecimal value:
  
  ```
  ping 192.168.1.1 -p 42
  ```
  
  To send 4 pings with a payload of "AA":

  ```
  ping 192.168.1.1 -c 4 -p AA
  ```

  Or using a payload that repeats every 4 bytes:

  ```
  ping 192.168.1.1 -c 4 -p 1234ABCD
  ```

- **Set the Time Interval Between Pings:**  
  Sends a ping every 2 seconds (default is 1 second).

  ```
  ping -i 2 192.168.1.1
  ```

- **Flood Ping:**  
  Sends packets as fast as possible for testing high-speed networks. Use with caution, as it can be very resource intensive.

  ```
  ping -f 192.168.1.1
  ```

- **Set TTL:**  
  Sets the Time-To-Live (TTL) value to 5.

  ```
  ping -t 5 192.168.1.1
  ```

- **Set Total Runtime:**  
  Pings for 10 seconds then stops, regardless of how many packets were sent.

  ```
  ping -w 10 google.com
  ```

- **Specify Timeout for Each Ping Packet:**  
  Waits a maximum of 3 seconds for a reply before considering a packet lost.

  ```
  ping -W 3 google.com
  ```

- **Record Route:**  
  Displays the route taken by the packet (if supported by intermediate routers).

  ```
  ping -R 192.168.1.1
  ```

---

## Traceroute

The `traceroute` command traces the path that packets take from your system to a destination host, helping diagnose network issues by identifying each hop and measuring latency.

### Installation

- **Red Hat/CentOS/Fedora:**

  ```
  dnf install traceroute
  ```

- **Debian/Ubuntu:**

  ```
  apt install traceroute
  ```

### Usage

- **Trace the route to a host:**

  ```
  traceroute google.com
  ```
  
  or

  ```
  traceroute 8.8.8.8
  ```

  *Example Output:*

      traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
       1  _gateway (192.168.1.1)  4.010 ms  3.270 ms  2.331 ms
       2  125.21.20.121 (125.21.20.121)  9.489 ms  8.892 ms  125.16.168.89 (125.16.168.89)  7.833 ms
       3  116.119.73.90 (116.119.73.90)  25.328 ms  116.119.106.218 (116.119.106.218)  23.139 ms  116.119.106.214 (116.119.106.214)  22.960 ms
       4  72.14.212.48 (72.14.212.48)  28.761 ms  27.855 ms  30.291 ms
       5  * * *
       6  dns.google (8.8.8.8)  24.913 ms  22.258 ms  24.396 ms

  The `* * *` indicates that the router is not responding to the probes.
  A probe is a test packet sent to each router (hop) along the path.

- **Using ICMP Instead of UDP:**

  Some firewalls may block UDP packets, so use the `-I` flag to force ICMP Echo Requests:

  ```
  traceroute -I google.com
  ```

- **Using TCP Instead of UDP:**

  For environments where both UDP and ICMP are blocked, use TCP SYN packets with the `-T` flag:

  ```
  traceroute -T google.com
  ```

- **Set Maximum Hops (TTL):**

  Limits maximum hops to 40 instead of the default 30

  ```
  traceroute -m 40 google.com
  ```

- **Set Query Packets per Hop:**

  Sends 2 probes per hop instead of the default of 3.	( A **probe** is a test packet sent to each router (hop) along the path. )

  ```
  traceroute -q 2 google.com
  ```

- **Set Packet Size:**

  Sends packets of 100 bytes instead of the default 60 bytes.

  ```
  traceroute -s 100 google.com
  ```

- **Show AS Numbers:**

  Displays Autonomous System (AS) numbers for each hop.

  ```
  traceroute -A google.com
  ```

  *Example Output:*

      traceroute to google.com (142.250.183.174), 30 hops max, 60 byte packets
       1  _gateway (192.168.1.1) [*]  3.467 ms  2.737 ms  2.317 ms
       2  125.21.18.205 (125.21.18.205) [AS9498]  9.766 ms nsg-static-025.124.71.182.airtel.in (182.71.124.25) [AS9498]  9.067 ms nsg-static-029.124.71.182.airtel.in (182.71.124.29) [AS9498]  8.591 ms
       3  116.119.73.21 (116.119.73.21) [AS55536]  23.609 ms 116.119.106.212 (116.119.106.212) [AS55536]  29.498 ms 116.119.158.84 (116.119.158.84) [*]  28.703 ms
       ... (additional hops)

---

## tcptraceroute

`tcptraceroute` is a variation of `traceroute` that uses TCP packets instead of the default UDP or ICMP. This can be useful when firewalls block UDP/ICMP traffic, but TCP is allowed.

### Example

- **Trace the route to Google on TCP port 80:**

  ```
  tcptraceroute google.com 80
  ```

---

## tracepath

`tracepath` is a simple alternative to `traceroute` that does not require root privileges and automatically determines the maximum transmission unit (MTU).

### Installation

- **Red Hat/CentOS:**

  ```
  yum install iputils-tracepath
  ```

- **Debian/Ubuntu:**

  ```
  apt install iputils-tracepath
  ```

### Usage

- **Trace the route to a host (e.g., 8.8.8.8):**

  ```
  tracepath 8.8.8.8
  ```

  *Example Output:*

      1?: [LOCALHOST]                                           pmtu 1500
      1:  _gateway                                              4.291ms
      1:  _gateway                                              4.046ms
      2:  _gateway                                              3.887ms pmtu 1472
      2:  abts-mh-dynamic-001.32.169.122.airtelbroadband.in     9.990ms
      3:  125.16.168.89                                        10.227ms asymm  5
      4:  116.119.73.209                                       23.644ms asymm  5
      5:  72.14.212.48                                         28.851ms asymm  9

- **Trace the route to your local network gateway:**

  ```
  tracepath 192.168.1.1
  ```

---

## Sockets

### Overview

- A **socket** is an endpoint for communication between two devices or processes on the same machine. It is typically represented as an IP address and port (e.g., 192.168.1.10:22).

### Types of Sockets in Linux

Sockets in Linux can be categorized based on protocol type and communication type.

#### A) Protocol-Based Sockets

| Protocol                  | Description                                                                                         |
| ------------------------- | --------------------------------------------------------------------------------------------------- |
| TCP (Transmission Control Protocol) | Reliable, connection-oriented communication (e.g., SSH, HTTP, FTP).                          |
| UDP (User Datagram Protocol)          | Fast, connectionless communication but unreliable (e.g., DNS, VoIP, DHCP).                 |
| TCP6                     | TCP over IPv6.                                                                                      |
| UDP6                     | UDP over IPv6.                                                                                      |
| Netlink Sockets          | Special sockets for kernel-user space communication (used by tools like `ss`, `ip`, `tc`).           |
| UNIX Domain Sockets      | Used for inter-process communication (IPC) within the same machine.                                  |
| Raw Sockets              | Provide direct access to network packets (e.g., used by tools like `ping`).                           |

#### B) Communication-Type Sockets

| Type                           | Description                                                         |
| ------------------------------ | ------------------------------------------------------------------- |
| Internet Sockets (IPv4, IPv6)      | Used for network communication over TCP or UDP.                    |
| UNIX Domain Sockets           | Used for local inter-process communication (IPC) only.              |
| Raw Sockets                   | Provide low-level access to network packets (bypasses TCP/UDP headers).|
| Netlink Sockets               | Facilitate kernel-user space communication (used by networking tools).|

### Connection

- A **connection** refers to the communication link between two devices over a network.

---

## netstat Command *(Deprecated in Modern Linux Systems)*

The `netstat` command displays network connections, routing tables, interface statistics, masquerade connections, and more. Although it is deprecated in favor of `ss`, it is still widely used.

### Supported Protocols

- TCP, UDP, and ICMP are supported.

### What netstat Shows

- **Sockets:** (both Internet and UNIX Domain)
- **Established Connections:** Active connections between devices.
- **Listening Services:** Sockets waiting for incoming connections.
- **Routing Tables:** Network routes.
- **Network Interface Statistics**

### Files Used by netstat

- **Active TCP Connections:** `/proc/net/tcp`, `/proc/net/tcp6`
- **Active UDP Connections:** `/proc/net/udp`, `/proc/net/udp6`
- **Active UNIX Domain Sockets:** `/proc/net/unix`
- **Active RAW Sockets:** `/proc/net/raw`, `/proc/net/raw6`
- **Routing Table:** `/proc/net/route`
- **ARP Table:** `/proc/net/arp`
- **Multicast Memberships:** `/proc/net/igmp` (IPv4), `/proc/net/ipv6_mcast` (IPv6)
- **Network Interfaces:** `/proc/net/dev`

### Connection States

| State       | Meaning                                                                                     |
| ----------- | ------------------------------------------------------------------------------------------- |
| LISTEN      | The server is waiting for incoming connections.                                           |
| ESTABLISHED | An active connection exists between two devices.                                           |
| CLOSE_WAIT  | The remote side has closed the connection, but the local side hasn’t yet closed it.          |
| TIME_WAIT   | The connection is closed but remains in a timeout phase before full termination.             |
| SYN_SENT    | A connection request has been sent but not yet acknowledged.                                |
| SYN_RECV    | A connection request has been received and is awaiting confirmation.                        |
| FIN_WAIT1   | The connection is closing (first stage).                                                    |
| FIN_WAIT2   | The connection is closing (second stage).                                                   |
| CLOSED      | The connection is completely closed.                                                        |

### Common netstat Commands

- **Show All Active Network Connections:**  
  (Displays all active TCP connections; does not show listening ports.)

  ```
  netstat
  ```

  *Example Output:*

      Active Internet connections (w/o servers)
      Proto Recv-Q Send-Q Local Address           Foreign Address         State
      tcp        0      0 centos:ssh              192.168.1.7:57286       ESTABLISHED

- **Show Numerical Addresses Instead of Resolving Names:**

  ```
  netstat -n
  ```

- **Display All Connection States (Listening & Established):**

  ```
  netstat -a
  ```

- **Show Only TCP Connections:**

  ```
  netstat -t
  ```

- **Show Only UDP Connections:**

  ```
  netstat -u
  ```

  (Note: UDP is connectionless, so no "State" column appears.)

- **Show Only Listening Ports:**

  ```
  netstat -l
  ```

- **Display Process ID (PID) and Program Name:**

  ```
  netstat -p
  ```

- **Monitor Network Connections in Real-Time:**

  ```
  netstat -c
  ```

- **Show Kernel Routing Table:**

  ```
  netstat -r
  ```

- **Show Interface Statistics:**

  ```
  netstat -i
  ```

- **Display Detailed Network Statistics:**

  ```
  netstat -s
  ```

- **Combined Forms:**

  - Active and listening connections in numerical form:

    ```
    netstat -an
    ```

  - Both TCP and UDP connections:

    ```
    netstat -ut
    ```

  - Extended details including errors and dropped packets:

    ```
    netstat -ie
    ```

  - Listening TCP and UDP ports in numeric form:

    ```
    netstat -ltun
    ```

  - Only listening connections (TCP & UDP) in numeric form:

    ```
    netstat -nltup
    ```

  - Both active and listening connections (TCP & UDP) in numeric form:

    ```
    netstat -natup
    ```

  - To filter for the process listening on port 22:

    ```
    netstat -nltup | grep :22
    ```

---

## ss Command (Socket Statistics)

The `ss` command is a modern alternative to `netstat` that displays detailed information about network connections quickly by directly querying the kernel via Netlink sockets.

### Advantages

- Faster and more efficient than `netstat` because it does not parse `/proc/net/*` files.
- Provides detailed information about network connections.

### Installation

- **CentOS:**

  ```
  dnf install iproute
  ```

- **Debian/Ubuntu:**

  ```
  apt install iproute2
  ```

### Common ss Commands

- **Show all active and listening connections:**

  ```
  ss
  ```

  *Example Output:*

      Netid  State      Recv-Q Send-Q   Local Address:Port   Peer Address:Port
      tcp    ESTAB      0      0        192.168.1.5:ssh      192.168.1.7:57286
      tcp    LISTEN     0      128      0.0.0.0:ssh          0.0.0.0:*
      tcp    LISTEN     0      128      [::]:ssh             [::]:*

- **Understanding the Output Columns:**

  | Column        | Description                                      |
  | ------------- | ------------------------------------------------ |
  | Netid         | Network protocol (TCP, UDP, UNIX, etc.)          |
  | State         | Connection state (e.g., LISTEN, ESTABLISHED)       |
  | Recv-Q / Send-Q | Bytes waiting to be received/sent              |
  | Local Address | Local IP and port                                |
  | Peer Address  | Remote IP and port                               |

- **Connection States**

| State       | Description                                                      |
|-------------|------------------------------------------------------------------|
| LISTEN      | The server is waiting for connections                          |
| ESTABLISHED | A connection is active and data is being exchanged               |
| CLOSE-WAIT  | Waiting for the application to close the connection              |
| TIME-WAIT   | Connection is closing but waiting before complete removal        |
| SYN-SENT    | A client is trying to establish a connection                     |
| FIN-WAIT1/2 | The connection is closing                                        |

- **Show All Active and Listening Sockets:**

  ```
  ss -a
  ```

- **Show Only Listening Sockets:**

  ```
  ss -l
  ```

- **Show Only TCP Connections:**

  ```
  ss -t
  ```

- **Show Only UDP Connections:**

  ```
  ss -u
  ```

- **Show Numerical IP Addresses:**  
  (Disables service name resolution)

  ```
  ss -n
  ```

- **Show Process Associations with Connections:**

  ```
  ss -p
  ```

- **Advanced Examples:**

  - Show listening TCP connections:

    ```
    ss -tl
    ```

  - Show listening UDP connections:

    ```
    ss -ul
    ```

  - Show all active connections and listening ports in numeric form:

    ```
    ss -na
    ```

  - Show listening TCP and UDP ports in numeric form:

    ```
    ss -ntul
    ```

  - Show all listening TCP/UDP connections with process IDs in numeric form:

    ```
    ss -nltup
    ```

  - Show both active and listening TCP/UDP connections with process information in numeric form:

    ```
    ss -natup
    ```
