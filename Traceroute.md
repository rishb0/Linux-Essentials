# **Traceroute Command (Network Path Analysis)**

The `traceroute` command is used to trace the route packets take from the source to the destination. It helps diagnose network issues by displaying each hop (router) along the way.

## **Key Features:**

- Identifies each hop a packet takes to reach its destination.
- Displays round-trip time (RTT) for each hop.
- Helps detect network latency, bottlenecks, and routing issues.
- Uses ICMP or UDP packets for tracing the path.

## **Syntax:**

```bash
traceroute [OPTIONS] DESTINATION
```

## **Commonly Used Options:**

- `-n` : Displays IP addresses instead of resolving hostnames.
- `-m TTL` : Sets the maximum number of hops (default is 30).
- `-q NUM` : Specifies the number of probe packets per hop (default is 3).
- `-w TIME` : Sets the timeout in seconds for each reply.
- `-I` : Uses ICMP echo requests instead of UDP packets.

---

## **Examples and Output Analysis:**

### **1. Basic Traceroute to a Website**

```bash
traceroute google.com
```

#### **Example Output:**

```
traceroute to google.com (142.250.183.14), 30 hops max, 60 byte packets  
 1  192.168.1.1 (192.168.1.1)  2.123 ms  1.987 ms  2.345 ms  
 2  10.10.10.1 (10.10.10.1)  5.678 ms  5.432 ms  5.210 ms  
 3  203.0.113.1 (203.0.113.1)  10.123 ms  9.876 ms  10.543 ms  
 4  142.250.183.14 (142.250.183.14)  15.432 ms  15.876 ms  16.123 ms  
```

#### **Explanation:**

- The destination is `google.com` (142.250.183.14).
- Each line represents a hop (router) the packet passes through.
- `192.168.1.1`: First hop, likely the user's home router.
- `10.10.10.1`: Second hop, an internal network device (ISP gateway).
- `203.0.113.1`: Third hop, an external ISP or backbone network.
- `142.250.183.14`: The final destination (Google server).
- Each hop has three round-trip times (RTTs) in milliseconds (ms), showing network latency for that hop.

---

### **2. Traceroute Without Hostname Resolution**

```bash
traceroute -n google.com
```

#### **Example Output:**

```
traceroute to 142.250.183.14, 30 hops max, 60 byte packets  
 1  192.168.1.1  2.567 ms  2.456 ms  2.789 ms  
 2  10.10.10.1  6.321 ms  6.543 ms  6.765 ms  
 3  203.0.113.1  12.789 ms  12.654 ms  12.876 ms  
 4  142.250.183.14  18.123 ms  18.654 ms  18.987 ms  
```

#### **Explanation:**

- This version does not resolve hostnames, making the output display only IP addresses.
- It speeds up execution by skipping DNS resolution.

---

### **3. Set Maximum Hops to 10**

```bash
traceroute -m 10 google.com
```

#### **Example Output:**

```
traceroute to google.com (142.250.183.14), 10 hops max, 60 byte packets  
 1  192.168.1.1  3.123 ms  3.456 ms  3.789 ms  
 2  10.10.10.1  7.432 ms  7.654 ms  7.876 ms  
 3  203.0.113.1  14.321 ms  14.654 ms  14.987 ms  
 4  * * *  
 5  * * *  
```

#### **Explanation:**

- Limits the maximum number of hops to 10.
- If a packet takes more than 10 hops, `* * *` appears, meaning the packet could not reach beyond this point.

---

### **4. Use ICMP Instead of UDP**

```bash
traceroute -I google.com
```

#### **Example Output:**

```
traceroute to google.com (142.250.183.14), 30 hops max, 60 byte packets  
 1  192.168.1.1  1.987 ms  2.123 ms  2.345 ms  
 2  10.10.10.1  5.876 ms  6.123 ms  6.432 ms  
 3  203.0.113.1  11.234 ms  11.654 ms  11.876 ms  
 4  142.250.183.14  17.456 ms  17.789 ms  18.123 ms  
```

#### **Explanation:**

- This version uses ICMP Echo Requests (like `ping`) instead of UDP packets.
- Some routers block UDP but allow ICMP, making this a useful alternative.

---

### **5. Change Timeout to 1 Second Per Hop**

```bash
traceroute -w 1 google.com
```

#### **Example Output:**

```
traceroute to google.com (142.250.183.14), 30 hops max, 60 byte packets  
 1  192.168.1.1  2.654 ms  2.876 ms  3.123 ms  
 2  10.10.10.1  7.321 ms  7.543 ms  7.765 ms  
 3  203.0.113.1  13.654 ms  13.876 ms  14.123 ms  
 4  * * *  
```

#### **Explanation:**

- Sets the timeout to 1 second per hop.
- If a response takes longer than 1 second, it is marked as `* * *`, meaning it was dropped or delayed.

---

## **When to Use Traceroute:**

- **Troubleshooting slow or failing network connections.**
    - If a website is slow, traceroute can help determine if an intermediate network is causing delays.
- **Identifying where packet loss or high latency occurs.**
    - If latency spikes in a particular hop, that router may be overloaded or misconfigured.
- **Checking routing paths for misconfigurations.**
    - If a packet takes an unexpected route, traceroute can reveal if the ISP is redirecting traffic incorrectly.
- **Understanding the number of hops between networks.**
    - Knowing how many hops exist between you and a server can help estimate the expected latency.

---
