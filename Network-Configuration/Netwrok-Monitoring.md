# **Network Monitoring with `netstat` and `ss`**

## Installation

To install the required tools, use:

```bash
yum install net-tools -y

```

## **Using `netstat`**

The `netstat` command is used to monitor network connections, routing tables, interface statistics, masquerade connections, and more.

### **Basic Usage**

- Display active connections:
    
    ```bash
    netstat
    
    ```
    
- Show all listening and non-listening (active) connections:
    
    ```bash
    netstat -a
    
    ```
    
- Display numeric addresses instead of resolving hostnames:
    
    ```bash
    netstat -na
    
    ```
    
- Filter by protocol:
    - Show only TCP connections:
        
        ```bash
        netstat -t
        
        ```
        
    - Show only UDP connections:
        
        ```bash
        netstat -u
        
        ```
        
    - Show both TCP and UDP connections:
        
        ```bash
        netstat -tu
        
        ```
        
- Display TCP and UDP connections in numeric format:
    
    ```bash
    netstat -tun
    
    ```
    
- Show listening TCP and UDP ports:
    
    ```bash
    netstat -ltun
    
    ```
    
- Display all listening services, numeric IPs, and process details (more accurate):
    
    ```bash
    netstat -nltup
    netstat -natup
    
    ```
    

## **Using `ss`**

The `ss` command is a faster alternative to `netstat` for displaying socket statistics.

### **Basic Usage**

- Display active connections:
    
    ```bash
    ss
    
    ```
    
- Show all listening sockets:
    
    ```bash
    ss -l
    
    ```
    
- Display TCP connections:
    
    ```bash
    ss -t
    
    ```
    
- Display UDP connections:
    
    ```bash
    ss -u
    
    ```
    
- Display listening TCP and UDP ports:
    
    ```bash
    ss -ltun
    
    ```
    
- Display detailed process information for each socket:
    
    ```bash
    ss -tp
    
    ```
    

## **Comparison: `netstat` vs. `ss`**

| Feature | `netstat` | `ss` |
| --- | --- | --- |
| Speed | Slower | Faster |
| Availability | Requires `net-tools` package | Pre-installed in modern Linux |
| Features | Comprehensive but outdated | More detailed and efficient |
| Performance | Higher resource usage | Lower resource usage |
| Filtering | Basic filtering | Advanced filtering |
| IPv6 Support | Limited support | Full support |

## **Conclusion**

`netstat` and `ss` are essential tools for monitoring and troubleshooting network connections in CentOS. While `netstat` is widely used, `ss` is a faster and more efficient alternative for analyzing socket connections. Both tools provide detailed insights into active connections, routing, and protocol-specific statistics, making them valuable for network administrators and system engineers.
