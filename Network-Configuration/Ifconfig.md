# Interface Configuration (ifconfig)

Interface configuration refers to the setup and management of network interfaces on a device such as a router, switch, or computer.

## Display Network Interface
- This command is used to display all network interfaces, including both active and inactive ones.

```bash
ifconfig -a
```

- This command displays detailed information about a specific network interface.

```bash
ifconfig emp0s3
```

## Assign an IP Address
- Assign an IP address temporarily to the network interface.

```bash
ifconfig emp0s3 192.168.0.40
```

- Manually assign an IP address and subnet mask to the network interface.

```bash
ifconfig emp0s3 192.168.0.41 netmask 255.255.255.0
```

- Assign an IP address with a subnet mask in CIDR notation.

```bash
ifconfig emp0s3 192.168.0.42/20
```

- Disable the network interface.

```bash
ifconfig emp0s3 down
```

- Enable the network interface.

```bash
ifconfig emp0s3 up
```

- Create and assign an IP address to a virtual (alias) network interface.

```bash
ifconfig emp0s3:1 192.168.0.42
```

## Enable/Disable Network Interface
- Enable a network interface.

```bash
ifup emp0s3
```

- Disable a network interface, stopping all network communication.

```bash
ifdown emp0s3
```

## View Network Information
- Display detailed information about all network interfaces and their assigned IP addresses.

```bash
ip addr show
```

- Assign a new IP address to the network interface.

```bash
ip addr add 192.168.0.40/24 dev emp0s3
```

- Disable the network interface.

```bash
ip link set emp0s3 down
```

- Enable the network interface.

```bash
ip link set emp0s3 up
```

## Routing Table Management
- Display and manipulate the routing table in Linux.

```bash
ip route
```

- Manually add a new route to a specific network.

```bash
ip route add 192.168.0.64/24 via 192.168.1.1 dev emp0s3
```

- Delete a specific route.

```bash
ip route del 192.168.0.0/24
```

- Set the default gateway.

```bash
ip route add default via 192.168.1.1 dev emp0s3
```

- Display routing table entries for a specific network interface.

```bash
ip route show dev emp0s3
```

- Remove/flush all routes from the main routing table.

```bash
ip route flush table main
```

## Ping Command
- Test network connectivity between two devices.

```bash
ping 8.8.8.8
```

- Send only 2 packets.

```bash
ping 8.8.8.8 -c 2
```

- Send a 65,500-byte packet (default is 56 bytes).

```bash
ping 192.168.1.1 -s 65500
```

- Send 4 large ICMP packets (65,500 bytes each) from a specific network interface.

```bash
ping -I emp0s3 192.168.1.1 -s 65500 -c 4
```

- Send 2 large ICMP packets (65,500 bytes each) from a specific network interface.

```bash
ping 192.168.1.1 -c 2 -s 65500 -I emp0s3 -p 42
```

- Ping with a 10-second interval, sending only 2 packets.

```bash
ping 192.168.1.1 -i 10 -c 2
```

- Ping using IPv6.

```bash
ping -6 armourinfosec.com
```

- Send a flood of ICMP echo request packets with the maximum packet size.

```bash
ping 192.168.1.1 -f -s 65500
```

## Traceroute Command
- Track the path that packets take to reach a destination.

### Install traceroute

For RHEL/CentOS:

```bash
yum install traceroute 
```

For Debian/Ubuntu:

```bash
apt install traceroute
```

- Trace the path that network packets take.

```bash
traceroute 8.8.8.8
```

- Trace the route packets take using TCP packets.

```bash
tcptraceroute 8.8.8.8
```

## Tracepath Command
Tracepath is a network diagnostic tool similar to traceroute, but it does not require root privileges and automatically detects the Maximum Transmission Unit (MTU) along the route.

### Install iputils and iputils-tracepath

For RHEL/CentOS:

```bash
yum install iputils iputils-tracepath  
```

For Debian/Ubuntu:

```bash
apt install iputils-tracepath          
```

- Run tracepath to check the network route.

```bash
tracepath 8.8.8.8
