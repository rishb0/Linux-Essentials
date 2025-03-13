# **NFTABLES COMMANDS **

This guide provides a quick reference to essential nftables commands with a one-line explanation preceding every command.

---

### **NFTables Structure Summary**  

- **Tables**: The top-level container that holds chains and rules. It defines the protocol family (**`ip` (IPv4), `ip6` (IPv6), `inet` (Both), `arp` (ARP), `bridge` (Bridging), `netdev` (Per-interface filtering)**).  
- **Chains**: A collection of rules that determine how packets are processed. Each chain is attached to a hook (**`prerouting`, `input`, `forward`, `output`, `postrouting`**), specifying where it applies in packet processing. Chains must have a type (**`filter` (firewall), `nat` (address translation), `route` (routing)**) and a priority (**`-300` (raw), `-200` (mangle), `-100` (NAT), `0` (filter)**).  
- **Rules**: The actual filtering logic inside chains. They define conditions (**IP, ports, connection state, interfaces**) and actions (**`accept`, `drop`, `reject`, `log`, `counter`, `dnat`, `snat`, `masquerade`**).  

**Workflow:**  
1. A table is created to organize rules (**must specify a family**).  
2. Chains are added inside the table to handle different traffic types (**must specify type, hook, and priority**).  
3. Rules are placed in chains to control how packets are processed (**match conditions and apply actions**).  

---

## **1. Basic Setup**

- **Install nftables on Debian/Ubuntu:**  
  Installs nftables using the apt package manager.
  ```
  apt install nftables
  ```

- **Install nftables on CentOS/RHEL:**  
  Installs nftables using the yum package manager.
  ```
  yum install nftables
  ```

- **Install nftables on Fedora:**  
  Installs nftables using the dnf package manager.
  ```
  dnf install nftables
  ```

- **Start nftables Service:**  
  Starts the nftables service.
  ```
  systemctl start nftables
  ```

- **Enable nftables Service at Boot:**  
  Enables nftables to automatically start at boot.
  ```
  systemctl enable nftables
  ```

- **Check nftables Service Status:**  
  Displays the current status of the nftables service.
  ```
  systemctl status nftables
  ```

---

## **2. Basic Commands**

- **Flush the Entire Ruleset:**  
  Removes all existing rules, chains, and tables.
  ```
  nft flush ruleset
  ```

- **List the Current Ruleset:**  
  Displays all the tables, chains, and rules currently loaded.
  ```
  nft list ruleset
  ```

- **Save the Current Ruleset:**  
  Exports the current configuration to a backup file.
  ```
  nft list ruleset > backup.nft
  ```

- **Restore the Ruleset from Backup:**  
  Loads rules from a previously saved configuration file.
  ```
  nft -f backup.nft
  ```

---

## **3. Create Table & Chains**

- **Create a New Table:**  
  Creates a new table in the 'inet' family named "my_table".
  ```
  nft add table inet my_table
  ```

- **Delete an Existing Table:**  
  Removes the table named "my_table" from the 'inet' family.
  ```
  nft delete table inet my_table
  ```

- **List All Tables:**  
  Lists all tables currently configured.
  ```
  nft list tables
  ```

- **Create a New Chain:**  
  Creates a new chain "my_chain" in table "my_table" with filter type and "input" hook.
  ```
  nft add chain inet my_table my_chain { type filter hook input priority 0 \; }
  ```

- **Delete an Existing Chain:**  
  Deletes the chain "my_chain" from table "my_table".
  ```
  nft delete chain inet my_table my_chain
  ```

- **List All Chains:**  
  Lists all chains on the system.
  ```
  nft list chains
  ```

- **List Chains within a Specific Table:**  
  Displays all chains belonging to "my_table".
  ```
  nft list table inet my_table
  ```

- **List Rules from a Specific Chain Only:**  
  Displays rules for "my_chain" without listing other chains.
  ```
  nft list chain inet my_table my_chain
  ```

- **Set Default Policy to Drop:**  
  Ensures that any packet not explicitly allowed is dropped.
  ```
  nft add chain inet my_table my_chain { type filter hook input priority 0 \; policy drop; }
  ```

- **Set Default Policy to Accept:**  
  Allows all packets unless explicitly denied.
  ```
  nft add chain inet my_table my_chain { type filter hook input priority 0 \; policy accept; }
  ```

---

## **4. Flushing Specific Components**

- **Flush All Rules in a Specific Table:**  
  Removes all rules while keeping chains and the table itself.
  ```
  nft flush table inet my_table
  ```

- **Flush Rules from a Specific Chain Only:**  
  Clears all rules in the specified chain but keeps the chain itself.
  ```
  nft flush chain inet my_table my_chain
  ```

- **Delete a Specific Rule Based on Condition (Without Handle Number):**  
  Removes the exact rule matching the condition without using handle numbers manually.
  ```
  nft delete rule inet my_table my_chain tcp dport 22 accept
  ```

---

## **5. IPv6-Specific Commands**

- **Allow IPv6 ICMP Traffic:**  
  Essential for proper IPv6 network operation.
  ```
  nft add rule inet my_table my_chain ip6 nexthdr icmpv6 accept
  ```

- **Drop All IPv6 Traffic:**  
  Blocks all IPv6 traffic if IPv6 is not required.
  ```
  nft add rule inet my_table my_chain ip6 drop
  ```

---

## **6. Advanced Rules**

- **Allow Traffic from a Specific IP:**  
  Accepts traffic originating from IP address 192.168.1.100.
  ```
  nft add rule inet my_table my_chain ip saddr 192.168.1.100 accept
  ```

- **Block Traffic from a Specific IP:**  
  Drops packets coming from IP address 192.168.1.100.
  ```
  nft add rule inet my_table my_chain ip saddr 192.168.1.100 drop
  ```

- **Limit Connections (Rate Limiting):**  
  Limits connections from any source to 10 per minute.
  ```
  nft add rule inet my_table my_chain ip saddr 0.0.0.0/0 limit rate 10/minute accept
  ```

- **Drop Invalid Packets:**  
  Drops packets that are in an invalid connection state to prevent malformed traffic.
  ```
  nft add rule inet my_table my_chain ct state invalid drop
  ```

- **Port Forwarding (NAT):**  
  Sets up a NAT table, creates a prerouting chain, and forwards HTTP traffic to an internal server.
  ```
  nft add table nat
  ```

  ```
  nft add chain nat prerouting { type nat hook prerouting priority 0 \; }
  ```

  ```
  nft add rule nat prerouting ip daddr 203.0.113.1 tcp dport 80 dnat to 192.168.1.100:8080
  ```

---

## **7. Logging & Debugging**

- **Log Dropped Packets:**  
  Logs packets that are dropped with a "DROPPED: " prefix.
  ```
  nft add rule inet my_table my_chain drop log prefix "DROPPED: "
  ```

- **Enable Packet Counting:**  
  Adds a counter to track the number of packets matching this rule.
  ```
  nft add rule inet my_table my_chain counter
  ```

- **Check Rule Counters:**  
  Lists the current ruleset, including counters.
  ```
  nft list ruleset
  ```

---

## **8. Persistent Rules**

- **Save Ruleset for Persistence:**  
  Exports the entire ruleset to /etc/nftables.conf for loading on reboot.
  ```
  nft list ruleset > /etc/nftables.conf
  ```

- **Enable Automatic Loading at Boot:**  
  Ensures nftables rules are loaded automatically at system startup.
  ```
  systemctl enable nftables
  ```

---

## **9. Firewall Ruleset Example**

- **Flush Existing Rules:**  
  Clears all current nftables configuration.
  ```
  nft flush ruleset
  ```

- **Create a Filter Table in the 'inet' Family:**  
  Creates a new table named "filter".
  ```
  nft add table inet filter
  ```

- **Create an Input Chain:**  
  Adds an "input" chain with a filter hook and priority 0.
  ```
  nft add chain inet filter input { type filter hook input priority 0 \; }
  ```

- **Allow Loopback Traffic:**  
  Accepts traffic on the loopback interface.
  ```
  nft add rule inet filter input iif lo accept
  ```

- **Allow Established Connections:**  
  Accepts packets that are part of established or related connections.
  ```
  nft add rule inet filter input ct state established,related accept
  ```

- **Allow SSH, HTTP, and HTTPS Traffic:**  
  Accepts TCP traffic destined for ports 22, 80, and 443.
  ```
  nft add rule inet filter input tcp dport { 22, 80, 443 } accept
  ```

- **Allow Traffic from a Specific Subnet:**  
  Accepts packets from the subnet 192.168.1.0/24.
  ```
  nft add rule inet filter input ip saddr 192.168.1.0/24 accept
  ```

- **Drop and Count All Other Traffic:**  
  Drops all remaining traffic while counting them.
  ```
  nft add rule inet filter input counter drop
  ```

- **List the Final Ruleset:**  
  Displays the complete configuration for verification.
  ```
  nft list ruleset
  ```

---

## **10. Firewalld Rules Management**

- **Reload Firewalld Rules:**  
  Reloads the firewalld configuration without restarting the service.
  ```
  firewall-cmd --reload
  ```

- **Restart the Firewalld Service:**  
  Restarts firewalld.
  ```
  systemctl restart firewalld
  ```

- **Disable Firewalld Completely:**  
  Stops, disables, and masks firewalld.
  ```
  systemctl stop firewalld
  ```

  ```
  systemctl disable firewalld
  ```

  ```
  systemctl mask firewalld
  ```

- **Flush nftables Rules After Disabling Firewalld:**  
  Clears all nftables rules to remove any residual firewalld configurations.
  ```
  nft flush ruleset
  ```
