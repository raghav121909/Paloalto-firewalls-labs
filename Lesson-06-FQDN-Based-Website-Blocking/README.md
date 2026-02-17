# LAB: Block a Website using Palo Alto Firewall (Without License)

## Goal

Blocked access to google.com from Ubuntu so that the website does not open and the firewall denies the traffic successfully.


## Concept

Websites use domain names (for example, google.com), but firewalls operate using IP addresses. Palo Alto firewall resolves domain names (FQDN) into IP addresses and applies security policies based on those IPs.

This was implemented using:

- Address Object (FQDN)
- Security Policy

## STEP 1: Create FQDN Address Object

Navigated to:

Objects → Addresses

Created a new address object with:

- Name: block-google
- Type: FQDN
- FQDN: google.com

The firewall automatically resolved the IP addresses for google.com.


## STEP 2: Create Block Security Policy

Navigated to:

Policies → Security → Add

Configured:

### General

- Name: Block-Google
- Action: Deny

### Source

- Source Zone: trust
- Source Address: ubuntu IP or any

### Destination

- Destination Zone: untrust
- Destination Address: block-google

### Application

- any

### Service

- application-default

### Actions

- Action: Deny
- Logging enabled at session end

Moved the Block-Google rule above the allow internet rule to ensure correct rule processing order.


## STEP 3: Commit Configuration

Committed the configuration successfully.

---

## STEP 4: Testing from Ubuntu

Opened browser and attempted to access:

https://www.google.com

Result:

- Website did not load
- Access was blocked as expected


## STEP 5: Verification in Firewall Logs

Navigated to:

Monitor → Traffic

Applied filter:

- Action = deny

Verified:

- Application showed ssl or web-browsing
- Destination matched google.com IP
- Rule matched Block-Google

## Status

Successfully configured and verified FQDN-based website blocking using Palo Alto firewall security policies.
