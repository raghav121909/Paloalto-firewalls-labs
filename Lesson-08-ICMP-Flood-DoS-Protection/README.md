# Lesson 8 DoS Protection Lab – ICMP Flood Simulation (Safe Educational Lab)

## Objective
In this lab, a controlled ICMP flood simulation was performed to test Palo Alto firewall DoS protection capabilities. High ICMP traffic was generated from an internal Ubuntu system to verify that the firewall detects excessive traffic and mitigates the flood by dropping packets.

This lab was conducted in a safe and isolated environment for educational purposes only.

---

## Lab Architecture

Ubuntu (Traffic Generator) → Palo Alto Firewall → Target (Firewall Interface or Test VM)

---

## Lab Goals
- Generate high ICMP traffic in a controlled environment
- Trigger ICMP flood detection
- Verify automatic mitigation through packet dropping

---

## Lab Environment
- Firewall: Palo Alto VM-Series
- Traffic Generator: Ubuntu Linux
- Zones:
  - trust (internal network)
  - untrust (external network)

---

## Step 1 Configure DoS Protection Profile

A Zone Protection Profile was created to enable ICMP flood protection.

GUI Path:
Network → Network Profiles → Zone Protection

Configuration:
- Profile Name: DOS-LAB
- Flood Protection Enabled
- ICMP Flood Protection: Enabled

Threshold Settings (Lab Values):
- Activate Rate: 200 packets/sec
- Maximum Rate: 400 packets/sec
- Action: Drop

Low threshold values were used to easily trigger detection within a virtual lab environment.

---

## Step 2 Attach Protection Profile to Zone

GUI Path:
Network → Zones

Configuration:
- Edited internal zone (trust)
- Applied Zone Protection Profile: DOS-LAB

Commit was performed to activate protection.

---

## Step 3 Generate Controlled ICMP Traffic

Controlled traffic generation was performed using Ubuntu.

### Install Traffic Tool

sudo apt install hping3
