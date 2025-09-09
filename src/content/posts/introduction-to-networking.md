---
title: "Introduction to Networking"
published: 2025-09-04
draft: false
toc: true
description: "Learn the fundamental hardware components and protocols that power network communication, plus essential Linux commands for network troubleshooting."
series: 'Basic'
tags: ['networking', 'tutorial']
---


## OSI Model
The OSI (Open Systems Interconnection) model is a conceptual framework used to understand and implement network protocols in seven layers. Each layer serves a specific function and communicates with the layers directly above and below it.

1. **Physical Layer**: The actual wires and signals
Example: Ethernet cable carrying electrical signals, fiber optics, Wi-Fi radio waves

2. **Data Link Layer**: Device-to-device communication on same network
Example: Your laptop talking to your Wi-Fi router, MAC addresses, switches

3. **Network Layer**: Finding paths across different networks
Example: GPS for data - router, NAT, IP addressing

4. **Transport Layer**: Reliable delivery and error checking
Example: TCP ensures your email arrives complete and in order

5. **Session Layer**: Managing conversations between apps
Example: Keeping your video call connected for 30 minutes

6. **Presentation Layer**: Data formatting and encryption
Example: Converting HTTPS encrypted data into readable text

7. **Application Layer**: The programs you actually use
Example: Your web browser, email client, or messaging app


## Hardware components

### Switch
Between the router and the computers, there is a switch. It knows the addresses of the devices on the local network (LAN). It manages data traffic between them. It operates at the data link layer (Layer 2) of the OSI model.

### Router
The router connects the local network to the internet. It forwards data packets between different networks. Its uses a routing table to determine the best path for forwarding the packets. It operates at the network layer (Layer 3) of the OSI model.

### DHCP Server
The DHCP (Dynamic Host Configuration Protocol) server assigns IP addresses to devices on the local network. It ensures that each device has a unique IP address. The DHCP server is often integrated into the router. It operates at the application layer (Layer 7) of the OSI model.

### Firewall
A firewall monitors and controls incoming and outgoing network traffic based on predetermined security rules. It establishes a barrier between a trusted internal network and untrusted external networks, such as the internet. Firewalls can be hardware-based, software-based, or a combination of both.

## Protocols

### IP addresses
An IP address (Internet Protocol address) is a unique numerical label assigned to every device connected to a network. It serves two main functions: identifying the device and providing the location of the host in the network. There is two kind of IP addresses:

- IPv4: 32-bit, 4 blocks (0-255) allowing for approximately 4.3 billion unique addresses (e.g., 192.168.1.1).
- IPv6: 128-bit, 8 blocks (0 - FFFF) allowing for a vastly larger number of unique addresses (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334).

Mask: A subnet mask is used to divide an IP address into network and host portions. It defines the boundary of your network. Example:


255.255.255.0
|   |   |   |
|   |   |   +-- Host part (0-255)
|---|---|---+------ Network part (192.168.1) or (10.0.0)

0.0.0.0/0 means "all IP addresses". The first 4 numbers are the IP address, the /0 is the mask.

255 in this exemple could be 0, 128, 192, 224, 240, 248, 252, 254 or 255. If it was 255, it would mean "all devices in this network". For 128 it would be "first half of the devices in this network", for exemple : 

Takes an IP like 192.168.1.100 and says "192.168.1 is your neighborhood, 100 is your house number."

The last address in a subnet is called the broadcast address. It is used to send data to all devices on the subnet. For a subnet with a mask of 255.255.255.0, the broadcast address would be 192.168.1.255.

Three notation :
- Binary: 11111111.11111111.11111111.00000000
- Decimal: 255.255.255.0
- CIDR: /24

Exemple calculation :
11111111.11111111.11111110.00000000

23 >> 1
9 >> 0

2^(32-23) - 2 = 510 - 2 = 508 hosts

32 Total length of ip address
-2 2 reserved (network and broadcast address)

128 - 64 - 32 - 16 - 8 - 4 - 2 - 1

#### Ports
Ports are like doors on a computer that allow different types of network traffic to enter and exit. They are represented by a number between 0 and 65535. Some ports are reserved for specific services:

- 80: HTTP (web traffic)
- 443: HTTPS (secure web traffic)
- 22: SSH (secure shell for remote access)
- 25: SMTP (sending email)
- 53: DNS (domain name system)

They are used in addition to IP addresses to direct traffic to the correct application or service on a device. For example, when you visit a website, your computer connects to the server's IP address on port 80 (HTTP), example: 75.2.70.75:80

### TCP
A connection-oriented protocol that ensures reliable data transmission between devices. It establishes a connection before data is sent and guarantees that all packets arrive in order and without errors. It is used for applications where reliability is crucial, such as web browsing (HTTP/HTTPS), email (SMTP), and file transfers (FTP).

### UDP
A connectionless protocol that does not guarantee reliable data transmission. It sends packets without establishing a connection and does not ensure that packets arrive in order or without errors. It is used for applications where speed is more important than reliability, such as video streaming, online gaming, and voice over IP (VoIP).

### HTTP/HTTPS
HTTP (Hypertext Transfer Protocol) is the foundation of data communication on the web. It defines how messages are formatted and transmitted, and how web servers and browsers should respond to various commands.

### FTP
FTP (File Transfer Protocol) is a standard network protocol used to transfer files between a client and a server over a TCP-based network, such as the internet. FTP operates at the application layer (Layer 7) of the OSI model.

### MAC address
A MAC (Media Access Control) address is a unique identifier assigned to a network interface controller (NIC) for use as a network address in communications within a network segment. MAC addresses are used in the data link layer (Layer 2) of the OSI model.

### ICMP
ICMP (Internet Control Message Protocol) is used for error messages and operational information. For example, the `ping` command uses ICMP to test the reachability of a host on an IP network. It operates at the network layer (Layer 3) of the OSI model.

### DORA
DORA stands for Discover, Offer, Request, Acknowledge. It is the process used by the DHCP (Dynamic Host Configuration Protocol) to assign IP addresses to devices on a network.

## WAN and LAN
- WAN (Wide Area Network): A WAN is a telecommunications network that extends over a large geographical area, often a country or continent. The internet is the largest example of a WAN.
- LAN (Local Area Network): A LAN is a network that connects computers and devices in a limited geographical area, such as a home, school, or office building. LANs are typically faster and more secure than WANs.

### NAT 
NAT is about translating private IPs to public IPs so devices on a private network can access the internet.

- Private IP ranges (RFC1918):
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16

- How NAT works:
  - Your laptop has a private IP, e.g., 192.168.1.10.
  - You want to reach 8.8.8.8 (Google DNS).
  - The NAT device (usually a router) replaces your private IP with its public IP for outgoing packets.
  - When responses come back, NAT translates it back to your private IP.

NAT is why multiple devices in your home can share a single public IP.


## Configruration files

### /etc/hosts
The `/etc/hosts` file is a simple text file that maps hostnames to IP addresses

networks
### /etc/resolv.conf
The `/etc/resolv.conf` file is used to configure DNS (Domain Name System) settings on a Linux system. It specifies the DNS servers that the system should use to resolve domain names into IP addresses.

### /etc/network/interfaces
The `/etc/network/interfaces` file is used to configure network interfaces on Debian-based Linux distributions.

### /etc/hostname
The `/etc/hostname` file contains the hostname of the system. The hostname is a human-readable label that is used to identify the system on a network.


## Commands


### sudo /etc/init.d/networking restart
Restart the networking service to apply changes made to network configuration files.

### ping
The `ping` command is used to test the reachability of a host on an IP network. 

```bash
ping 8.8.8.8  # Ping Google's public DNS server
ping example.com  # Ping a domain name
```

### ip
The `ip` command is used to show and manipulate routing, devices, policy routing, and tunnels.

```bash
ip addr show          # Show all IP addresses
ip link show          # Show all network interfaces
ip route show         # Show the routing table  
```

### traceroute
The `traceroute` command is used to trace the path that packets take from your computer to a destination host.

```bash
traceroute example.com  # Trace the route to example.com
```

### dhclient
The `dhclient` command is a DHCP client that is used to obtain an IP address and other network configuration parameters from a DHCP server.

```bash
sudo dhclient -v # Request an IP address with verbose output
```

### nmap
The `nmap` command is a network scanning tool used to discover hosts and services on a computer network.

```bash
nmap google.com # Scan google.com for open ports 

```
