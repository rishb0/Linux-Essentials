 **Tracepath Command (Network Path Discovery)**

The `tracepath` command is used to trace the network path packets take to a destination, similar to `traceroute`, but it **does not require root privileges**. It dynamically determines the **maximum transmission unit (MTU)** along the route, making it useful for detecting network bottlenecks and MTU-related issues.

## **Key Features:**

- Identifies each hop in the network path.
- Measures round-trip time (RTT) for each hop.
- Detects Maximum Transmission Unit (MTU) per hop.
- Uses **UDP packets** and does not require superuser permissions.

## **Syntax:**

```bash
tracepath [OPTIONS] DESTINATION
```

## **Commonly Used Options:**

- `-n` : Displays IP addresses instead of resolving hostnames.
- `-m TTL` : Sets the maximum number of hops (default is 30).
- `-b` : Displays both hostnames and IP addresses.
- `-l PACKET_SIZE` : Sets the packet size for testing MTU.
- `-p PORT` : Specifies the UDP port for sending probes.

---

## **Examples and Output Analysis:**

### **1. Basic Tracepath to a Website**

```bash
tracepath google.com
```

#### **Example Output:**

```
 1?: [LOCALHOST]                              pmtu 1500  
 1:  192.168.1.1                              1.234ms  
 2:  10.10.10.1                               5.678ms  
 3:  203.0.113.1                              10.543ms  
 4:  142.250.183.14                           15.876ms  
     Resume: pmtu 1500  
```

#### **Explanation:**

- **First line:** The `pmtu 1500` shows the initial **Path Maximum Transmission Unit (PMTU)**, which is **1500 bytes**.
- **Each hop (router) is listed with round-trip times (RTT) in milliseconds (ms).**
- `192.168.1.1`: Home router.
- `10.10.10.1`: ISP gateway.
- `203.0.113.1`: External network.
- `142.250.183.14`: Final destination (Google server).
- **Resume line:** Confirms the final PMTU remains **1500 bytes** after testing.

---

### **2. Tracepath Without Hostname Resolution**

```bash
tracepath -n google.com
```

#### **Example Output:**

```
 1?: [LOCALHOST]                              pmtu 1500  
 1:  192.168.1.1                              2.345ms  
 2:  10.10.10.1                               6.432ms  
 3:  203.0.113.1                              11.876ms  
 4:  142.250.183.14                           18.123ms  
     Resume: pmtu 1500  
```

#### **Explanation:**

- Same as the previous output but **only displays IP addresses** (no hostname resolution).
- This makes the command execute **faster** by skipping DNS lookups.

---

### **3. Set Maximum Hops to 10**

```bash
tracepath -m 10 google.com
```

#### **Example Output:**

```
 1?: [LOCALHOST]                              pmtu 1500  
 1:  192.168.1.1                              1.876ms  
 2:  10.10.10.1                               5.765ms  
 3:  203.0.113.1                              10.654ms  
 4:  *  
 5:  *  
```

#### **Explanation:**

- Limits the maximum number of hops to **10**.
- The `*` indicates **timeouts or unresponsive routers beyond the set limit**.

---

### **4. Display Both Hostnames and IP Addresses**

```bash
tracepath -b google.com
```

#### **Example Output:**

```
 1?: [LOCALHOST]                              pmtu 1500  
 1:  myrouter.home (192.168.1.1)              2.987ms  
 2:  isp.gateway (10.10.10.1)                 6.543ms  
 3:  backbone.net (203.0.113.1)               12.876ms  
 4:  google.com (142.250.183.14)              18.987ms  
     Resume: pmtu 1500  
```

#### **Explanation:**

- Displays both **hostnames and IP addresses** for each hop.
- Helps in identifying network infrastructure by **name** instead of just IP.

---

### **5. Set a Custom Packet Size to Test MTU**

```bash
tracepath -l 1200 google.com
```

#### **Example Output:**

```
 1?: [LOCALHOST]                              pmtu 1500  
 1:  192.168.1.1                              3.432ms  
 2:  10.10.10.1                               7.321ms  
 3:  203.0.113.1                              13.654ms  
 4:  142.250.183.14                           19.987ms  
     Resume: pmtu 1500  
```

#### **Explanation:**

- Sends packets of **1200 bytes** to check if all hops support that size.
- The **PMTU remains 1500**, meaning the network supports larger packets.

---

## **When to Use Tracepath:**

- **Diagnosing slow or failing network connections.**
    - Similar to `traceroute`, it helps detect where delays occur.
- **Checking MTU settings and detecting fragmentation issues.**
    - Ensures packets are not being **fragmented** due to MTU mismatches.
- **Determining routing paths and potential bottlenecks.**
    - Useful for analyzing ISP and network infrastructure performance.
- **Alternative to `traceroute` when running without root privileges.**
    - Since `tracepath` does not require superuser access, it can be used in restricted environments.

---

