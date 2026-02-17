# Lesson 4 QoS Configuration – Limiting Ubuntu Web Traffic

## Objective
In this lab, Quality of Service (QoS) was configured on the Palo Alto firewall to rate-limit Ubuntu web traffic (HTTP/HTTPS). The goal was to reduce bandwidth for specific applications while allowing other traffic to remain unaffected.

QoS was applied on the egress interface (ethernet1/1), since traffic exiting toward the internet is shaped at this point.

---

## Lab Environment
- Firewall: Palo Alto VM-Series
- Internal Host: Ubuntu VM
- External Network: VMware NAT (Internet simulation)

### Interface and Zone Setup
- ethernet1/2 → trust (internal network)
- ethernet1/1 → untrust (internet-facing)


## Pre-Configuration Verification
Before configuring QoS, connectivity was verified:

- Internet access confirmed from Ubuntu
- ping 8.8.8.8 successful
- curl http://neverssl.com successful

This ensured QoS testing would reflect actual bandwidth changes.


## Step 1 QoS Profile Creation

A QoS profile was created to define bandwidth shaping parameters.

GUI Path:
Network → QoS → Add Profile

Configuration:
- Profile Name: QOS-LAB
- Total Egress Bandwidth: 5 Mbps
- Class 1 Maximum Bandwidth: 1 Mbps

Purpose:
The QoS profile defines total interface bandwidth and sets limits for individual traffic classes.


## Step 2 Enable QoS on Egress Interface

QoS was enabled on ethernet1/1 since internet-bound traffic exits through this interface.

GUI Path:
Network → QoS → Add

Configuration:
- Interface: ethernet1/1
- QoS feature enabled
- Default Profile: QOS-LAB

Without enabling QoS on the interface, shaping policies are not enforced.


## Step 3 QoS Policy Rule Creation

A QoS policy was created to classify Ubuntu web traffic into a limited bandwidth class.

GUI Path:
Policies → QoS

Configuration:
- Rule Name: Ubuntu-Web-Limit
- Source Zone: trust
- Source Address: 192.168.10.10 (Ubuntu)
- Destination Zone: untrust
- Applications:
  - web-browsing
  - ssl
- QoS Class: Class 1

Rule placement was ensured above general policies for correct matching.


## Step 4 Commit
Configuration changes were committed to apply QoS policies to the dataplane.


## Step 5 Testing and Verification

Testing was performed from the Ubuntu system:

curl -I https://www.google.com
