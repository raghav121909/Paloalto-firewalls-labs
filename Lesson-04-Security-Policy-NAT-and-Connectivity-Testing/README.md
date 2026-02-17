# Lesson 3: Connecting Ubuntu to Palo Alto Firewall and Generating Traffic

## Lab Overview

In this lab, I successfully connected an Ubuntu virtual machine to a Palo Alto firewall and generated real network traffic through it. The objective was to understand firewall routing, security policies, NAT configuration, and monitoring live traffic logs.

---

## Network Architecture

The environment was configured as follows:

Internet (VMware NAT network)  
→ Palo Alto ethernet1/1 (untrust) – 192.168.1.9  
→ Palo Alto Firewall  
→ ethernet1/2 (trust) – 192.168.10.1  
→ Ubuntu VM

Traffic flow:

1. Ubuntu sends traffic to the firewall gateway.
2. Firewall routes traffic from trust zone to untrust zone.
3. NAT translates private IP addresses.
4. Internet responds back through firewall.
5. Firewall logs all traffic activity.

---

## Ubuntu Network Connection

I configured the Ubuntu VM to connect to the same virtual network as the firewall trust interface.

Steps performed:

- Powered OFF Ubuntu VM.
- Changed VMware network adapter to Host-only network (same LAN segment as ethernet1/2).
- Enabled "Connected" and "Connect at power on".
- Powered ON Ubuntu.

This ensured that Ubuntu traffic passes through the Palo Alto firewall instead of bypassing it.

---

## Static IP Configuration on Ubuntu

Since DHCP was not configured, I assigned a static IP address.

First, I identified the interface by:

ip a

##  Create Security Policy (ALLOW)

### Theory

Palo Alto firewall blocks traffic by default, so traffic must be explicitly allowed using a security policy.

### GUI Steps

1. Go to: Policies → Security → Add
2. Configure:

- Name: allow-trust-to-untrust
- Source Zone: trust
- Destination Zone: untrust
- Application: any
- Service: application-default
- Action: allow

3. Click OK.


## Create NAT Policy

### Theory

Private IP addresses (192.168.10.x) cannot access the Internet directly. NAT is required to translate private IPs into a public interface address.

### GUI Steps

1. Go to: Policies → NAT → Add

Original Packet:

- Source Zone: trust
- Destination Zone: untrust
- Source Address: any
- Destination Address: any

Translated Packet:

- Source Translation: Dynamic IP and Port
- Type: Interface Address
- Interface: ethernet1/1

2. Click OK.


## Commit Configuration

Commit the configuration and wait until it completes successfully.


## Final Testing

From Ubuntu, test Internet connectivity:

ping 8.8.8.8


