# Lab 02 - Interface Configuration 

## ethernet1/1

## Objective
Configure the ISP-facing (Untrust) interface on a Palo Alto firewall to establish outbound internet connectivity. This is the first and most critical configuration step before setting up internal networks.

## Lab Overview
The Untrust interface connects the firewall to the external network (VMware NAT). It represents the internet-facing side of the firewall and handles untrusted traffic.

All configurations were performed using the Palo Alto GUI, with verification done through the CLI.


## Configuration Performed

### 1. GUI Access
- Logged in to the Palo Alto firewall using the management IP via the web interface.

### 2. Zone Configuration
- Created a Layer 3 security zone named **untrust**
- This zone represents the ISP-facing network
- The zone will be used later in NAT and Security Policies

### 3. Interface Configuration
- Configured **ethernet1/1** as a Layer 3 interface
- Assigned the interface to the **untrust** zone
- Attached the interface to the **default virtual router**
- Enabled **DHCP Client** for IPv4 to automatically receive an IP address from VMware NAT (ISP side)

### 4. Commit
- Committed the configuration to apply all changes on the firewall

## Verification
- Verified from the GUI that **ethernet1/1** was up and received an IP address
- Accessed the firewall CLI using SSH
- Confirmed interface status and DHCP assignment
- Successfully tested internet connectivity by pinging **8.8.8.8**

## Commands Used
show interface all
show interface ethernet1/1
show dhcp client state
ping host 8.8.8.8

