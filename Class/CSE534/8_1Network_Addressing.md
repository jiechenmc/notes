---
layout: post
title: Network Addressing
tags:
  - networks
---
First level - Autonomous Systems (AS) - Google, Stony, Comcast
Second Level - Within the AS

AS is a system/company/org that get assigned addresses

# TCAM

- Heavily Parallelized 
- Can address 0, 1, X (don't care)

Say you are routing 1011. The checks will happen in parallel.

![[TCAM]]

# Network Layer: IP

Creates a new header (with TTL - 1) before sending the packet to the next hop.

IPv6 removes the checksum field because transport check it anyway.

# NAT

![[NAT]]

Can see information from the upper layers to indefinite who the packet is sent to


# IPv6 Tunneling in IPv4

IPv6 datagrams carried as payload in IPv4 among IPv4 routers. Nowadays, most routers support dual stack so no need for tunneling.