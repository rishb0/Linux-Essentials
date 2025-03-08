# Service Management in Linux

## Key Points of a Linux Service

- **Background Process:** Runs in the background without user intervention, unlike typical applications.
- **System Management:** Manages essential functions like networking, storage, logging, etc.
- **Controlled by Init Systems:** Managed by an init system like `systemd`, `upstart`, or `SysVinit`, which controls the starting, stopping, and restarting of services.
- **Configuration and Logs:** Usually have configuration files in `/etc` and log files in `/var/log`.

## Managing Services Using SysVinit (`/etc/init.d/`)

SysVinit is an older service management system used in Debian-based and other older Linux distributions.

### Checking Available Init Scripts
```bash
cd /etc/init.d/
ls -lh /etc/init.d/
```

### Viewing an Init Script
```bash
cat /etc/init.d/<service-name>
```
Example:
```bash
cat /etc/init.d/apache2
```

### Checking the Status of a Service
```bash
/etc/init.d/apache2 status
```

### Starting or Stopping a Service
```bash
/etc/init.d/apache2 start
/etc/init.d/apache2 stop
```

### Restarting a Service
```bash
/etc/init.d/apache2 restart
```

### Reloading a Service
```bash
/etc/init.d/apache2 force-reload
```

## Managing Services in Modern Linux Distributions

### Using the `service` Command (Legacy Systems)
For older Linux distributions that use `init.d` or `SysVinit` instead of `systemd`:

#### Checking Service Status
```bash
service <service_name> status
```
Example:
```bash
service apache2 status
```

#### Starting a Service
```bash
service <service_name> start
```
Example:
```bash
service apache2 start
```

#### Stopping a Service
```bash
service <service_name> stop
```
Example:
```bash
service apache2 stop
```

#### Restarting a Service
```bash
service <service_name> restart
```
Example:
```bash
service apache2 restart
```

#### Reloading Configuration Without Restart
```bash
service apache2 reload
```

## Managing Services with `systemctl` (Modern Systems)

`systemctl` is used in modern Linux distributions (Debian 8+, Ubuntu 15.04+, CentOS 7+, RHEL 7+).

### Installing a Service (Example: HTTPD)
```bash
yum install httpd*
```

### Checking Service Status
```bash
systemctl status <service_name>
```
Example:
```bash
systemctl status apache2
```

### Starting and Stopping Services
```bash
systemctl start <service_name>
systemctl stop <service_name>
```

### Restarting a Service
```bash
systemctl restart <service_name>
```

### Reloading a Service
```bash
systemctl reload <service_name>
```

### Enabling and Disabling Services at Boot
```bash
systemctl enable <service_name>
```
```bash
systemctl disable <service_name>
```

### Checking if a Service is Enabled
```bash
systemctl is-enabled <service_name>
```

### Listing Services
```bash
systemctl list-units --type=service --state=running
systemctl list-units --type=service --state=failed
```

### Masking and Unmasking Services
Masking prevents a service from running:
```bash
systemctl mask <service_name>
```
Unmasking re-enables a service:
```bash
systemctl unmask <service_name>
```

### Viewing Logs for a Service
```bash
journalctl -u <service_name>
```
Example:
```bash
journalctl -u httpd.service
```

#### Viewing Logs from the Last Hour
```bash
journalctl -u httpd.service --since "1 hour ago"
```

#### Live Logs (Useful for Debugging)
```bash
journalctl -u httpd.service -f
```

### System Power Management with `systemctl`

#### Reboot the System
```bash
systemctl reboot
```

#### Shut Down the System
```bash
systemctl poweroff
```

#### Suspend the System
```bash
systemctl suspend
```

#### Hibernate the System
```bash
systemctl hibernate
```

## SysVinit vs. Systemd (`systemctl`)
Modern Linux distributions use `systemd`, replacing `SysVinit`. Instead of `/etc/init.d/`, use:

```bash
systemctl start apache2
systemctl stop apache2
systemctl restart apache2
systemctl status apache2
systemctl enable apache2
systemctl disable apache2
```


