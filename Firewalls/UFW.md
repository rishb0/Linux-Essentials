# UFW Complete Guide
---

## 1. UFW Status and Management Commands

- Check UFW status:
```
ufw status
```
  Displays the current UFW status (active/inactive) and the list of rules if active.

- Check UFW status with detailed output:
```
ufw status verbose
```
  Provides detailed information about UFW settings.

- Check UFW status with rule numbers:
```
ufw status numbered
```
  Lists active rules with numbers, useful for deleting specific rules.

- Enable UFW:
```
ufw enable
```
  Activates UFW (requires confirmation).

- Disable UFW:
```
ufw disable
```
  Deactivates UFW.

- Reset UFW (delete all rules):
```
ufw reset
```
  Clears all rules and resets UFW to its default settings.

---

## 2. Allow Rules

### Allow a Specific Port (TCP/UDP)

- Allow TCP port 22 (SSH):
```
ufw allow 22/tcp
```

- Allow UDP port 53 (DNS):
```
ufw allow 53/udp
```

- Allow a port for both TCP and UDP (e.g., port 80):
```
ufw allow 80
```

### Allow a Port Range

- Allow TCP ports 1000 to 2000:
```
ufw allow 1000:2000/tcp
```

- Allow UDP ports 5000 to 5100:
```
ufw allow 5000:5100/udp
```

### Allow a Specific IP

- Allow traffic from a specific IP address:
```
ufw allow from 192.168.1.100
```

### Allow a Specific IP to a Specific Port

- Allow traffic from a specific IP to any port 22 using TCP:
```
ufw allow from 192.168.1.50 to any port 22 proto tcp
```

### Allow an IP Range (Subnet)

- Allow traffic from an entire subnet:
```
ufw allow from 192.168.1.0/24
```

### Allow a Port to a Specific IP

- Allow traffic to a specific IP address on port 22 using TCP:
```
ufw allow to 192.168.1.200 port 22 proto tcp
```

### Allow Traffic on a Specific Interface

- Allow incoming traffic on port 22 using interface eth0:
```
ufw allow in on eth0 to any port 22 proto tcp
```

---

## 3. Deny Rules (Silently Drop Traffic)

### Deny a Specific Port

- Deny TCP port 22:
```
ufw deny 22/tcp
```

- Deny UDP port 53:
```
ufw deny 53/udp
```

### Deny a Port Range

- Deny TCP ports 6000 to 7000:
```
ufw deny 6000:7000/tcp
```

### Deny a Specific IP

- Deny all traffic from a specific IP:
```
ufw deny from 192.168.1.50
```

### Deny a Specific IP to a Specific Port

- Deny traffic from a specific IP to port 22 using TCP:
```
ufw deny from 192.168.1.52 to any port 22 proto tcp
```

### Deny a Subnet

- Deny traffic from an entire subnet:
```
ufw deny from 10.10.10.0/24
```

### Deny Traffic to a Specific IP

- Deny traffic to a specific IP on port 22 using TCP:
```
ufw deny to 192.168.1.44 port 22 proto tcp
```

---

## 4. Reject Rules (Block Traffic with "Connection Refused" Response)

- Reject TCP port 3389:
```
ufw reject 3389/tcp
```

- Reject traffic from a specific IP to port 22 using TCP:
```
ufw reject from 192.168.1.45 to any port 22 proto tcp
```

- Reject traffic to a specific IP on port 22 using TCP:
```
ufw reject to 192.168.1.33 port 22 proto tcp
```

---

## 5. Limit Rules (Rate-Limiting for Brute-Force Protection)

- Limit SSH to prevent brute force attacks:
```
ufw limit ssh
```

- Limit a custom port (e.g., 443/TCP):
```
ufw limit 443/tcp
```

- Limit a specific IP to port 22 using TCP:
```
ufw limit from 192.168.1.50 to any port 22 proto tcp
```

---

## 6. Route Rules (For Forwarded Traffic / NAT)

- Allow routed traffic on a specific interface:
```
ufw route allow in on eth1 out on eth0 to any port 80 proto tcp
```

- Deny routed traffic to a specific IP:
```
ufw route deny in on eth1 out on eth0 to 192.168.2.100
```

---

## 7. Deleting Rules

### Delete Rule by Number

- First, check numbered rules:
```
ufw status numbered
```
- Then delete a rule by its number:
```
ufw delete 3
```
*(This deletes rule number 3 as shown in numbered status.)*

### Delete Rule by Specification

- Delete an allowed port rule:
```
ufw delete allow 90:99/tcp
```
- Delete a specific allow rule:
```
ufw delete allow from 192.168.1.28 to any port 22 proto tcp
```

---

## 8. Logging and Monitoring

- Enable logging:
```
ufw logging on
```
- Enable high-level logging:
```
ufw logging high
```
- Disable logging:
```
ufw logging off
```
- View UFW logs in real time:
```
tail -f /var/log/ufw.log
```
- Check UFW logs with journalctl:
```
journalctl -xe | grep UFW
```

---

## 9. Advanced: Forwarding, NAT, and Routing

- Enable IP masquerading (NAT) by editing /etc/ufw/before.rules. Add the following rules:
  ```
  *nat
  :POSTROUTING ACCEPT [0:0]
  -A POSTROUTING -s 192.168.1.0/24 -o eth0 -j MASQUERADE
  COMMIT
  ```
- Enable forwarding:
  ```
  echo "net/ipv4/ip_forward=1" >> /etc/ufw/sysctl.conf
  ```
  ```
  ufw reload
  ```

---

## 10. Resetting and Troubleshooting

- Reset UFW (delete all rules and restore defaults):
```
ufw reset
```
- Disable UFW:
```
ufw disable
```
- Enable UFW:
```
ufw enable
```
- Check which backend UFW is using (iptables or nftables):
```
update-alternatives --display iptables
```

---

## Additional UFW Actions

| Action           | Description                                                         |
|------------------|---------------------------------------------------------------------|
| allow            | Permits traffic through the firewall                                |
| deny             | Blocks traffic and silently drops packets                           |
| reject           | Blocks traffic and sends a "connection refused" message to the sender |
| limit            | Permits traffic but rate-limits repeated connections (brute-force protection) |
| route            | Applies firewall rules to forwarded (routed) packets                  |
| logging on/off   | Enables or disables logging of firewall activity                      |

---

## 11. Installation and Basic Setup

- Update Package Lists:
```
apt update
```
- Install UFW:
```
apt install ufw
```
- Check UFW version:
```
ufw version
```
- Check UFW status:
```
ufw status
```
- Enable UFW:
```
ufw enable
```
- Show added rules:
```
ufw show added
```
- Allow Specific Services and Ports:
  - Allow SSH:
    ```
    ufw allow ssh
    ```
  - Allow specific TCP and UDP ports:
    ```
    ufw allow 8088/tcp
    ```
    ```
    ufw allow https
    ```
    ```
    ufw allow telnet
    ```
    ```  
    ufw allow smtp
    ```
    ```
    ufw allow pop3
    ```
- Show added rules again:
```
ufw show added
```
- Managing UFW Service:
  - Check UFW service status:
    ```
    systemctl status ufw.service
    ```
  - Enable UFW service on boot:
    ```
    systemctl enable ufw.service
    ```
  - Start UFW service:
    ```
    systemctl start ufw.service
    ```
- Show numbered rules:
```
ufw status numbered
```
- Delete specific rules by number:
```
ufw delete 12
```
ufw delete 24
```
- Delete rules by full specification:
```
ufw delete allow 90:99/tcp
```
ufw delete allow from 192.168.1.28 to any port 22 proto tcp
```
- List available applications:
```
ufw app list
```
