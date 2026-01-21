# Lab - 03 Configure ethernet1/2 

## Objective
Configure the internal (Trust) interface on the Palo Alto firewall to build the LAN side of the network. This interface will act as the default gateway for internal hosts (Ubuntu) and enable controlled access to the internet.

## Prerequisites
- ethernet1/1 configured as **Untrust (ISP)** interface
- Untrust IP assigned via DHCP (VMware NAT)
- Firewall GUI and CLI access available

## What is a Trust Interface
A Trust interface connects internal resources such as:
- Employee PCs
- Servers
- Internal machines (Ubuntu client)

This interface represents the **internal, controlled, and trusted** side of the network.

### Real-World Flow
Employees → Trust → Firewall → Untrust → Internet

## Why a Separate Trust Interface is Required
Separating Trust and Untrust traffic:
- Enables proper security policy enforcement
- Improves logging and visibility
- Prevents internal attacks from spreading outward

Zones act as **security boundaries** in Palo Alto firewalls.

## IP Addressing Design
Private IP ranges (RFC1918) are used for internal networks:
- 10.0.0.0/8
- 172.16.0.0 – 172.31.0.0
- 192.168.0.0/16

### Selected Network
- Subnet: **192.168.10.0/24**
- Firewall (Gateway): **192.168.10.1**
- Ubuntu Client: **192.168.10.x**

## Why Firewall Acts as Gateway
Internal hosts send all non-local traffic to the default gateway.
The firewall then decides whether to:
- Allow or block traffic
- Perform NAT
- Log sessions

This makes traffic **visible, controllable, and secure**.

## Zone and Virtual Router Requirement
- **Zone** → Security decisions and policy enforcement
- **Virtual Router** → Routing and packet forwarding

Both are mandatory for Layer 3 interfaces.

## Configuration Performed

### Step 1 Create TRUST Zone
GUI Path:
Network → Zones → Add

Settings:
- Name: **trust**
- Type: **Layer3**

### Step 2 Configure ethernet1/2
GUI Path:
Network → Interfaces → ethernet1/2

#### Basic Tab
- Interface Type: Layer3
- Zone: trust
- Virtual Router: default

#### IPv4 Tab
Assigned Static IP: 192.168.10.1/24
This IP acts as the LAN gateway for internal hosts.

### Step 3 Commit
Committed the configuration to apply changes to the dataplane.


