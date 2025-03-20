---
layout: post
title: Network Forwarding
tags:
  - networks
---
# Forwarding

## Virtual Circuits

- Connection Orientated
- Reservation Based

Packets is forwarded along the circuit using tag.

## Packet Switching

- Best Effort
- Packets have no history or state

Store and forward.

## Internet Routing

For any given destination, find the next hop address. This next hop address is stored in a routing table that maps each destination to the next hop. At runtime, lookup the table and forward it to the next hop.

## Forwarding Fabric

There's several input and output ports. Each port is a different network address.

![[PacketSwitching.excalidraw]]

## Net Neutrality

Essentially enforces that packets be sent FIFO without any prioritization. 

## Forwarding Process

1. A frame enters the router's input interface
	- If the packet is corrupt, throw it out
2. Reads the destination IP
	- If the packet is meant for local router, then strip the network header and pass the packet to the higher layer
3. Otherwise, packet is routed and if the TTL > 1, routing proceeds
4. If ok, router looks at its own routing table for most specific prefix match for destination IP.