# **IPTABLES COMMANDS**  

This guide provides a **quick reference** to essential `iptables` commands with a **one-line explanation** preceding every command.  

⚠ **Note:** `iptables` is **deprecated** in favor of `nftables`, which provides a more efficient and flexible way to manage firewall rules. However, many systems still use `iptables`, and it remains relevant for legacy support.
---

### **iptables Structure Summary**  

- **Tables**: The top-level container that holds chains and rules. Each table is designed for specific types of packet processing:  
  - **`filter`** (default) → For packet filtering (accept, drop, reject).  
  - **`nat`** → For Network Address Translation (DNAT, SNAT, masquerading).  
  - **`mangle`** → For modifying packet headers (marking, TTL changes).  
  - **`raw`** → For bypassing connection tracking (used for advanced cases).  
  - **`security`** → For Mandatory Access Control (MAC) filtering (SELinux/AppArmor).  

- **Chains**: A collection of rules that process packets at different points. Each chain is attached to a **hook** to define where in the packet flow it applies:  
  - **`PREROUTING`** → Before routing decisions (mainly used in `nat`, `mangle`).  
  - **`INPUT`** → Packets destined for the local system.  
  - **`FORWARD`** → Packets being routed through the system.  
  - **`OUTPUT`** → Packets originating from the local system.  
  - **`POSTROUTING`** → After routing, before packets leave the system.  

- **Rules**: Define how packets are handled based on conditions (**IP, ports, protocol, connection state**) and actions (**ACCEPT, DROP, REJECT, LOG, MASQUERADE, DNAT, SNAT**).  

**Workflow:**  
1. A **table** is used to define the purpose of the rules (**filter, nat, mangle, etc.**).  
2. **Chains** are added inside the table to process packets at specific points (**INPUT, OUTPUT, FORWARD, etc.**).  
3. **Rules** are placed in chains to control how packets are processed (**match conditions and apply actions**).  

---

## **1. Basic Setup**  

- **Install iptables on Debian/Ubuntu:**  
  Installs iptables using the apt package manager.  
  ```
  apt install iptables
  ```  

- **Install iptables on CentOS/RHEL:**  
  Installs iptables using the yum package manager.  
  ```
  yum install iptables-services
  ```  

- **Install iptables on Fedora:**  
  Installs iptables using the dnf package manager.  
  ```
  dnf install iptables-services
  ```  

- **Start iptables Service:**  
  Starts the iptables service.  
  ```
  systemctl start iptables
  ```  

- **Enable iptables Service at Boot:**  
  Ensures iptables starts automatically on boot.  
  ```
  systemctl enable iptables
  ```  

- **Check iptables Service Status:**  
  Displays the current status of the iptables service.  
  ```
  systemctl status iptables
  ```  

---

## **2. Basic Commands**  

- **Flush All Rules:**  
  Removes all existing rules, but keeps chains and tables.  
  ```
  iptables -F
  ```  

- **List All Rules:**  
  Displays all currently configured rules.  
  ```
  iptables -L -v -n
  ```  

- **Save Current Rules:**  
  Saves the current configuration to a file.  
  ```
  iptables-save > /etc/iptables.rules
  ```  

- **Restore Rules from Backup:**  
  Loads rules from a previously saved file.  
  ```
  iptables-restore < /etc/iptables.rules
  ```  

---

## **3. Managing Tables & Chains**  

- **List Available Tables:**  
  Displays all tables currently available.  
  ```
  iptables -t filter -L
  ```  

- **Flush a Specific Chain:**  
  Removes all rules from a specific chain (e.g., INPUT).  
  ```
  iptables -F INPUT
  ```  

- **Delete a Specific Chain:**  
  Deletes an empty chain from the table.  
  ```
  iptables -X my_chain
  ```  

- **Set Default Policy to DROP:**  
  Drops all packets unless explicitly allowed.  
  ```
  iptables -P INPUT DROP
  ```  

- **Set Default Policy to ACCEPT:**  
  Accepts all packets unless explicitly denied.  
  ```
  iptables -P INPUT ACCEPT
  ```  

---

## **4. Adding & Removing Rules**  

- **Allow SSH Traffic (Port 22):**  
  Allows incoming SSH connections.  
  ```
  iptables -A INPUT -p tcp --dport 22 -j ACCEPT
  ```  

- **Allow HTTP and HTTPS Traffic:**  
  Allows incoming web traffic.  
  ```
  iptables -A INPUT -p tcp -m multiport --dports 80,443 -j ACCEPT
  ```  

- **Drop All Incoming Traffic:**  
  Blocks all incoming connections.  
  ```
  iptables -A INPUT -j DROP
  ```  

- **Delete a Specific Rule (by Matching Condition):**  
  Removes the exact rule without needing line numbers.  
  ```
  iptables -D INPUT -p tcp --dport 22 -j ACCEPT
  ```  

---

## **5. Advanced Rules**  

- **Allow Traffic from a Specific IP:**  
  Accepts packets from 192.168.1.100.  
  ```
  iptables -A INPUT -s 192.168.1.100 -j ACCEPT
  ```  

- **Block Traffic from a Specific IP:**  
  Drops packets coming from 192.168.1.100.  
  ```
  iptables -A INPUT -s 192.168.1.100 -j DROP
  ```  

- **Limit Connections (Rate Limiting):**  
  Limits new connections to 10 per minute per IP.  
  ```
  iptables -A INPUT -p tcp --dport 22 -m limit --limit 10/min -j ACCEPT
  ```  

- **Drop Invalid Packets:**  
  Drops packets in an invalid connection state.  
  ```
  iptables -A INPUT -m conntrack --ctstate INVALID -j DROP
  ```  

---

## **6. NAT & Port Forwarding**  

- **Enable IP Masquerading (SNAT for outgoing traffic):**  
  ```
  iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
  ```  

- **Forward Port 80 to an Internal Server (DNAT):**  
  ```
  iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.100:8080
  ```  

---

## **7. Logging & Debugging**  

- **Log Dropped Packets:**  
  ```
  iptables -A INPUT -j LOG --log-prefix "DROPPED: " --log-level 4
  ```  

- **Enable Packet Counting:**  
  ```
  iptables -A INPUT -j ACCEPT -m comment --comment "Count accepted packets"
  ```  

---

## **8. IPv6-Specific Commands (ip6tables)**  

- **Allow IPv6 ICMP Traffic:**  
  ```
  ip6tables -A INPUT -p icmpv6 -j ACCEPT
  ```  

- **Drop All IPv6 Traffic:**  
  ```
  ip6tables -A INPUT -j DROP
  ```  

---

## **9. Persistent Rules**  

- **Save Ruleset for Persistence:**  
  ```
  iptables-save > /etc/iptables.rules
  ```  

- **Enable Automatic Loading at Boot:**  
  ```
  systemctl enable iptables
  ```  

---
