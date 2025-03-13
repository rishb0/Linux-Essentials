# **Firewalld COMMANDS**

This guide provides a quick reference to essential firewalld commands with a one-line explanation preceding every command. It covers service management, zones, services, ports, rich rules, NAT, and more.

---

## **1. Firewalld Service Management**

- **Check if firewalld is running:**  
  Displays the current status of the firewalld service.
  ```
  systemctl status firewalld
  ```

- **Start firewalld:**  
  Starts the firewalld service.
  ```
  systemctl start firewalld
  ```

- **Stop firewalld:**  
  Stops the firewalld service.
  ```
  systemctl stop firewalld
  ```

- **Restart firewalld:**  
  Restarts the firewalld service.
  ```
  systemctl restart firewalld
  ```

- **Enable firewalld at startup:**  
  Configures firewalld to start automatically on system boot.
  ```
  systemctl enable firewalld
  ```

- **Disable firewalld at startup:**  
  Prevents firewalld from starting on system boot.
  ```
  systemctl disable firewalld
  ```

- **Check firewalld state:**  
  Displays the runtime state of firewalld.
  ```
  firewall-cmd --state
  ```

---

## **2. Installation and Package Information**

- **Check if firewalld is installed:**  
  Lists installed packages related to firewalld.
  ```
  rpm -qa | grep firewalld
  ```

- **Get detailed package information:**  
  Displays detailed information about the firewalld package.
  ```
  rpm -qi firewalld
  ```

- **Install firewalld (if not installed):**  
  Installs firewalld using the yum package manager.
  ```
  yum install firewalld -y
  ```

---

## **3. Zones Management**

- **List all available zones:**  
  Displays a list of all firewalld zones.
  ```
  firewall-cmd --get-zones
  ```

- **Show active zones and assigned interfaces:**  
  Lists current active zones with their associated interfaces.
  ```
  firewall-cmd --get-active-zones
  ```

- **Get the default zone:**  
  Displays the default zone used by firewalld.
  ```
  firewall-cmd --get-default-zone
  ```

- **Set a new default zone (permanent):**  
  Changes the default zone to "work" permanently and reloads firewalld.
  ```
  firewall-cmd --set-default-zone=work --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **Assign an interface to a zone (permanent):**  
  Assigns the interface eth0 to the "home" zone permanently.
  ```
  firewall-cmd --zone=home --change-interface=eth0 --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **Remove an interface from a zone (permanent):**  
  Removes the interface eth0 from the "home" zone permanently.
  ```
  firewall-cmd --zone=home --remove-interface=eth0 --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **List all rules in a zone:**  
  Displays all firewall rules configured in the "public" zone.
  ```
  firewall-cmd --zone=public --list-all
  ```

---

## **4. Managing Services**

- **List all available services:**  
  Displays a list of services that firewalld can manage.
  ```
  firewall-cmd --get-services
  ```

- **List allowed services in a zone:**  
  Shows services allowed in the "public" zone.
  ```
  firewall-cmd --zone=public --list-services
  ```

- **Allow a service in a zone (permanent):**  
  Adds the "http" service to the "public" zone permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --add-service=http --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **Remove a service from a zone (permanent):**  
  Removes the "http" service from the "public" zone permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --remove-service=http --permanent
  ```
  ```
  firewall-cmd --reload
  ```

---

## **5. Managing Ports**

- **Open a specific port (permanent):**  
  Opens TCP port 8080 in the "public" zone permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --add-port=8080/tcp --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **Close a specific port (permanent):**  
  Closes TCP port 8080 in the "public" zone permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --remove-port=8080/tcp --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **List all active ports in a zone:**  
  Displays the open ports in the "public" zone.
  ```
  firewall-cmd --zone=public --list-ports
  ```

---

## **6. Managing Rich Rules (Advanced Filtering)**

- **Block an IP permanently:**  
  Adds a rich rule to reject traffic from the IP 192.168.1.100 permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.1.100" reject' --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **Allow a specific IP (permanent):**  
  Adds a rich rule to accept traffic from the IP 192.168.1.100 permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.1.100" accept' --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **List all rich rules:**  
  Displays all rich rules currently in effect.
  ```
  firewall-cmd --list-rich-rules
  ```

- **Remove a rich rule (permanent):**  
  Removes the specified rich rule and reloads firewalld.
  ```
  firewall-cmd --zone=public --remove-rich-rule='rule family="ipv4" source address="192.168.1.100" reject' --permanent
  ```
  ```
  firewall-cmd --reload
  ```

---

## **7. Masquerading and Forwarding (NAT & Routing)**

- **Enable IP masquerading (permanent):**  
  Enables masquerading in the "public" zone permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --add-masquerade --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **Disable IP masquerading (permanent):**  
  Removes masquerading in the "public" zone permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --remove-masquerade --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **Set up port forwarding (permanent):**  
  Configures port forwarding from port 8080 to port 80 in the "public" zone permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --add-forward-port=port=8080:proto=tcp:toport=80 --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **List all active firewalld rules in all zones:**  
  Displays all configured rules across all zones, useful for troubleshooting.
  ```
  firewall-cmd --list-all-zones
  ```

- **List all active interfaces:**  
  Shows which interfaces are currently assigned to zones.
  ```
  firewall-cmd --list-interfaces
  ```

---

## **8. Saving and Restoring Rules**

- **Save runtime changes permanently:**  
  Transfers any runtime changes to the permanent configuration.
  ```
  firewall-cmd --runtime-to-permanent
  ```

- **Reset firewalld to defaults:**  
  Resets zones and rules to default settings, then reloads firewalld.
  ```
  firewall-cmd --reset-default-zone
  ```
  ```
  firewall-cmd --reload
  ```
  ```
  firewall-cmd --complete-reload
  ```

---

## **9. Debugging and Logs**

- **Check logs for dropped packets:**  
  Searches system logs for firewalld-related entries.
  ```
  journalctl -xe | grep firewalld
  ```

- **Enable logging for denied packets:**  
  Configures firewalld to log all denied packets.
  ```
  firewall-cmd --set-log-denied=all
  ```

---

## **10. Additional Useful Commands**

- **List all active firewalld rules across all zones:**  
  Displays all zones with their full configuration, helping with troubleshooting.
  ```
  firewall-cmd --list-all-zones
  ```

- **Remove a specific port from a zone (permanent):**  
  Removes a single port (e.g., TCP port 8080) from the "public" zone permanently and reloads firewalld.
  ```
  firewall-cmd --zone=public --remove-port=8080/tcp --permanent
  ```
  ```
  firewall-cmd --reload
  ```

- **List all active ports in a zone:**  
  Quickly lists only the open ports in the "public" zone.
  ```
  firewall-cmd --zone=public --list-ports
  ```

- **Reload firewalld without flushing rules:**  
  Applies configuration changes without resetting current rules.
  ```
  firewall-cmd --reload
  ```

- **List predefined application profiles:**  
  Displays the available services that firewalld can manage.
  ```
  firewall-cmd --get-services
  ```

- **Check rule order for conflicts:**  
  Displays all configurations across zones for comprehensive review.
  ```
  firewall-cmd --list-all-zones
  ```

---
