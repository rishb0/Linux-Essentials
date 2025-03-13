# **UFW COMMANDS**

---

## **1. UFW Status and Management Commands**

- **Check UFW status:**  
  Displays the current UFW status (active/inactive) and the list of rules if active.
  ```
  ufw status
  ```

- **Check UFW status with detailed output:**  
  Provides detailed information about UFW settings.
  ```
  ufw status verbose
  ```

- **Check UFW status with rule numbers:**  
  Lists active rules with numbers, useful for deleting specific rules.
  ```
  ufw status numbered
  ```

- **Enable UFW:**  
  Activates UFW (requires confirmation).
  ```
  ufw enable
  ```

- **Disable UFW:**  
  Deactivates UFW.
  ```
  ufw disable
  ```

- **Reset UFW (delete all rules):**  
  Clears all rules and resets UFW to its default settings.
  ```
  ufw reset
  ```

---

## **2. Allow Rules**

### Allow a Specific Port (TCP/UDP)

- **Allow TCP port 22 (SSH):**  
  Permits incoming SSH connections.
  ```
  ufw allow 22/tcp
  ```

- **Allow UDP port 53 (DNS):**  
  Permits incoming DNS queries.
  ```
  ufw allow 53/udp
  ```

- **Allow a port for both TCP and UDP (e.g., port 80):**  
  Permits web traffic for both protocols.
  ```
  ufw allow 80
  ```

### Allow a Port Range

- **Allow TCP ports 1000 to 2000:**  
  Permits TCP traffic on ports 1000 through 2000.
  ```
  ufw allow 1000:2000/tcp
  ```

- **Allow UDP ports 5000 to 5100:**  
  Permits UDP traffic on ports 5000 through 5100.
  ```
  ufw allow 5000:5100/udp
  ```

### Allow a Specific IP

- **Allow traffic from a specific IP address:**  
  Permits all traffic originating from the given IP.
  ```
  ufw allow from 192.168.1.100
  ```

### Allow a Specific IP to a Specific Port

- **Allow traffic from a specific IP to port 22 (SSH):**  
  Permits SSH connections only from the specified IP.
  ```
  ufw allow from 192.168.1.50 to any port 22 proto tcp
  ```

### Allow an IP Range (Subnet)

- **Allow traffic from an entire subnet:**  
  Permits traffic from the specified subnet.
  ```
  ufw allow from 192.168.1.0/24
  ```

### Allow a Port to a Specific IP

- **Allow traffic to a specific IP on port 22 (SSH):**  
  Permits SSH connections to the specified IP.
  ```
  ufw allow to 192.168.1.200 port 22 proto tcp
  ```

### Allow Traffic on a Specific Interface

- **Allow incoming traffic on port 22 using interface eth0:**  
  Permits SSH traffic on the eth0 interface.
  ```
  ufw allow in on eth0 to any port 22 proto tcp
  ```

---

## **3. Deny Rules (Silently Drop Traffic)**

### Deny a Specific Port

- **Deny TCP port 22 (SSH):**  
  Blocks incoming SSH connections.
  ```
  ufw deny 22/tcp
  ```

- **Deny UDP port 53 (DNS):**  
  Blocks incoming DNS queries.
  ```
  ufw deny 53/udp
  ```

### Deny a Port Range

- **Deny TCP ports 6000 to 7000:**  
  Blocks TCP traffic on ports 6000 through 7000.
  ```
  ufw deny 6000:7000/tcp
  ```

### Deny a Specific IP

- **Deny all traffic from a specific IP:**  
  Blocks all incoming traffic from the specified IP.
  ```
  ufw deny from 192.168.1.50
  ```

### Deny a Specific IP to a Specific Port

- **Deny traffic from a specific IP to port 22 (SSH):**  
  Blocks SSH traffic from the given IP.
  ```
  ufw deny from 192.168.1.52 to any port 22 proto tcp
  ```

### Deny a Subnet

- **Deny traffic from an entire subnet:**  
  Blocks traffic originating from the specified subnet.
  ```
  ufw deny from 10.10.10.0/24
  ```

### Deny Traffic to a Specific IP

- **Deny traffic to a specific IP on port 22 (SSH):**  
  Blocks SSH traffic directed to the specified IP.
  ```
  ufw deny to 192.168.1.44 port 22 proto tcp
  ```

---

## **4. Reject Rules (Block with "Connection Refused")**

- **Reject TCP port 3389:**  
  Blocks and rejects remote desktop connections with an active refusal.
  ```
  ufw reject 3389/tcp
  ```

- **Reject traffic from a specific IP to port 22 (SSH):**  
  Blocks SSH traffic from the specified IP, sending a refusal response.
  ```
  ufw reject from 192.168.1.45 to any port 22 proto tcp
  ```

- **Reject traffic to a specific IP on port 22 (SSH):**  
  Blocks SSH traffic directed to a specific IP with a rejection.
  ```
  ufw reject to 192.168.1.33 port 22 proto tcp
  ```

---

## **5. Limit Rules (Rate-Limiting for Brute-Force Protection)**

- **Limit SSH connections:**  
  Applies rate limiting to SSH connections to prevent brute-force attacks.
  ```
  ufw limit ssh
  ```

- **Limit a custom port (e.g., 443/TCP):**  
  Applies rate limiting to TCP traffic on port 443.
  ```
  ufw limit 443/tcp
  ```

- **Limit traffic from a specific IP to port 22 (SSH):**  
  Applies rate limiting on SSH from the specified IP.
  ```
  ufw limit from 192.168.1.50 to any port 22 proto tcp
  ```

---

## **6. Route Rules (For Forwarded Traffic / NAT)**

- **Allow routed traffic on a specific interface:**  
  Permits routed traffic on eth1 (incoming) and eth0 (outgoing) for web services.
  ```
  ufw route allow in on eth1 out on eth0 to any port 80 proto tcp
  ```

- **Deny routed traffic to a specific IP:**  
  Blocks forwarded traffic directed to the specified IP address.
  ```
  ufw route deny in on eth1 out on eth0 to 192.168.2.100
  ```

---

## **7. Deleting Rules**

### Delete Rule by Number

- **List numbered rules:**  
  Shows active rules with their corresponding numbers.
  ```
  ufw status numbered
  ```

- **Delete a rule by its number:**  
  Deletes the rule corresponding to number 3.
  ```
  ufw delete 3
  ```

### Delete Rule by Specification

- **Delete an allowed port range rule:**  
  Deletes the rule that allows TCP ports 90 through 99.
  ```
  ufw delete allow 90:99/tcp
  ```

- **Delete a specific allow rule:**  
  Deletes the rule allowing traffic from a specific IP to port 22.
  ```
  ufw delete allow from 192.168.1.28 to any port 22 proto tcp
  ```

---

## **8. Logging and Monitoring**

- **Enable logging:**  
  Turns on UFW logging of firewall activity.
  ```
  ufw logging on
  ```

- **Enable high-level logging:**  
  Sets UFW logging detail to high.
  ```
  ufw logging high
  ```

- **Disable logging:**  
  Turns off UFW logging.
  ```
  ufw logging off
  ```

- **View UFW logs in real time:**  
  Tails the UFW log file for live monitoring.
  ```
  tail -f /var/log/ufw.log
  ```

- **Check UFW logs using journalctl:**  
  Displays recent UFW-related log entries.
  ```
  journalctl -xe | grep UFW
  ```

---

## **9. Advanced: Forwarding, NAT, and Routing**

- **Enable IP masquerading (NAT):**  
  Edit `/etc/ufw/before.rules` and add the following to enable NAT on a specific subnet using interface eth0.
  ```
  *nat
  :POSTROUTING ACCEPT [0:0]
  -A POSTROUTING -s 192.168.1.0/24 -o eth0 -j MASQUERADE
  COMMIT
  ```

- **Enable IP forwarding:**  
  Enables IP forwarding by appending the setting to UFW's sysctl configuration.
  ```
  echo "net/ipv4/ip_forward=1" >> /etc/ufw/sysctl.conf
  ```

- **Reload UFW to Apply Changes:**  
  Reloads UFW without resetting or flushing current rules.
  ```
  ufw reload
  ```

---

## **10. Resetting and Troubleshooting**

- **Reset UFW (Delete all rules and restore defaults):**  
  Resets UFW to its original state by deleting custom rules.
  ```
  ufw reset
  ```

- **Disable UFW:**  
  Deactivates UFW.
  ```
  ufw disable
  ```

- **Enable UFW:**  
  Activates UFW.
  ```
  ufw enable
  ```

- **Check which backend UFW is using (iptables or nftables):**  
  Displays the alternative for iptables.
  ```
  update-alternatives --display iptables
  ```

---

## **11. Additional Useful Commands**

- **View UFW raw rules (verbose mode):**  
  Shows the actual iptables/nftables rules behind UFW for detailed inspection.
  ```
  ufw show raw
  ```

- **Check Listening Ports & Open Services:**  
  Verifies which ports and services are actively in use on your system.
  ```
  netstat -tulnp | grep LISTEN
  ```
  or
  ```
  ss -tulnp
  ```

- **Reload UFW Without Flushing Rules:**  
  Applies changes in UFW without resetting existing rules.
  ```
  ufw reload
  ```

- **List Predefined Application Profiles:**  
  Displays the available UFW application profiles.
  ```
  ufw app list
  ```

- **View Details of a Specific Application Profile:**  
  Shows detailed information about the "Apache" profile.
  ```
  ufw app info "Apache"
  ```

- **Check UFW Rule Order for Conflicts:**  
  Displays added UFW rules in order to help prevent conflicts.
  ```
  ufw show added
  ```

---

## **12. Installation and Basic Setup**

- **Update Package Lists:**  
  Updates your system's package list.
  ```
  apt update
  ```

- **Install UFW:**  
  Installs UFW on your system.
  ```
  apt install ufw
  ```

- **Check UFW Version:**  
  Displays UFW version information.
  ```
  ufw version
  ```

- **Show Added Rules:**  
  Displays currently added UFW rules.
  ```
  ufw show added
  ```

- **Allow Specific Services and Ports:**

  - **Allow SSH:**
    ```
    ufw allow ssh
    ```
  
  - **Allow a custom TCP port (e.g., 8088):**
    ```
    ufw allow 8088/tcp
    ```
  
  - **Allow HTTPS:**
    ```
    ufw allow https
    ```
  
  - **Allow Telnet:**
    ```
    ufw allow telnet
    ```
  
  - **Allow SMTP:**
    ```
    ufw allow smtp
    ```
  
  - **Allow POP3:**
    ```
    ufw allow pop3
    ```

- **Check UFW Service Status:**  
  Displays the status of the UFW service.
  ```
  systemctl status ufw.service
  ```

- **Enable UFW Service on Boot:**  
  Ensures that UFW starts automatically on system boot.
  ```
  systemctl enable ufw.service
  ```

- **Start UFW Service:**  
  Starts the UFW service.
  ```
  systemctl start ufw.service
  ```

- **Show Numbered Rules:**  
  Lists active rules with assigned numbers.
  ```
  ufw status numbered
  ```

- **Delete Specific Rules by Number:**  
  Deletes the rule corresponding to rule number 12.
  ```
  ufw delete 12
  ```
  Delete another rule (e.g., rule number 24):
  ```
  ufw delete 24
  ```

- **Delete Rules by Full Specification:**  
  Deletes the rule allowing TCP ports 90 to 99.
  ```
  ufw delete allow 90:99/tcp
  ```
  Deletes the rule allowing from 192.168.1.28 to port 22.
  ```
  ufw delete allow from 192.168.1.28 to any port 22 proto tcp
  ```

- **List Available Applications:**  
  Displays predefined application profiles.
  ```
  ufw app list
  ```

---
