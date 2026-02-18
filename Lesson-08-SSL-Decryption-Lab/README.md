# SSL Decryption Configuration Lab

## STEP 1 — Create Decryption Certificate

Navigated to:

Device → Certificate Management → Certificates

Generated a new certificate with the following configuration:

- Certificate Name: SSL-Decrypt-Cert
- Common Name: firewall.local
- Signed By: Self-Signed
- Certificate Authority enabled

After creation:

- Selected the certificate
- Opened Certificate Attributes
- Enabled Forward Trust Certificate

This allows the firewall to use the certificate for SSL decryption.

---

## STEP 2 — Export Certificate

Selected the certificate and exported it:

- Format: Base64
- Saved the certificate file locally.

---

## STEP 3 — Install Certificate on Ubuntu

On Ubuntu (Firefox browser):

- Navigated to Settings → Privacy & Security → Certificates → View Certificates
- Imported the downloaded certificate
- Enabled trust option: Trust this CA to identify websites

This step ensured SSL warnings would not appear during decryption.

---

## STEP 4 — Create Decryption Policy

Navigated to:

Policies → Decryption → Add

Configured:

### General

- Name: SSL-Decryption-Lab

### Source

- Zone: trust

### Destination

- Zone: untrust

### Action

- Decrypt

### Type

- SSL Forward Proxy

Clicked OK to save the rule.

---

## STEP 5 — Rule Order

Moved the decryption rule to the top to ensure it is processed before other rules.

---

## STEP 6 — Commit

Committed configuration changes successfully.

---

## STEP 7 — Testing and Verification

From Ubuntu:

- Opened https://google.com successfully.

Verification on firewall:

- Navigated to Monitor → Traffic Logs
- Confirmed decrypted traffic was visible.

---

## Status

SSL forward proxy decryption has been successfully configured, certificate installed on Ubuntu, and decrypted traffic verified through firewall monitoring.
