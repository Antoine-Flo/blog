---
title: "Introduction to Networking"
published: 2025-09-04
draft: false
toc: true
description: "Learn the fundamental hardware components and protocols that power network communication, plus essential Linux commands for network troubleshooting."
series: 'Basic'
tags: ['networking', 'tutorial']
---


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

### MAC address
A MAC (Media Access Control) address is a unique identifier assigned to a network interface controller (NIC) for use as a network address in communications within a network segment. MAC addresses are used in the data link layer (Layer 2) of the OSI model.

## IP address

## Commands

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

ip dhcp               # Request an IP address from a DHCP server
```

### dhclient
The `dhclient` command is a DHCP client that is used to obtain an IP address and other network configuration parameters from a DHCP server.

```bash
sudo dhclient -v # Request an IP address with verbose output
```

192.168.1.133

192.168.1.116

0c:04:cb:1f:00:00