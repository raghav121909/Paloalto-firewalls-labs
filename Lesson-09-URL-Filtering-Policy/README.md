# Custom URL Category Blocking Lab

## STEP 1 — Create Custom URL Category

Navigated to:

Objects → Custom Objects → URL Category

Created a new URL category with the following configuration:

- Name: Block-Websites
- Type: URL List
- Added URLs:
  - youtube.com
  - *.youtube.com
  - facebook.com
  - *.facebook.com

Saved the configuration successfully.

---

## STEP 2 — Create Security Policy

Navigated to:

Policies → Security → Add

Configured:

### General

- Name: Block-URL-Lab

### Source

- Zone: trust

### Destination

- Zone: untrust

### Application

- any

### Service

- application-default

### URL Category

- Selected custom category: Block-Websites

### Action

- deny
- Enabled logging for visibility.

Saved the rule successfully.

---

## STEP 3 — Rule Order

Moved the Block-URL-Lab rule above the general internet allow rule to ensure proper rule processing.

---

## STEP 4 — Commit

Committed configuration changes successfully.

---

## Testing

From Ubuntu:

- Attempted to open youtube.com — access was blocked.
- Opened google.com — access worked normally.

---

## Status

Successfully created and applied a custom URL category and verified website blocking using Palo Alto firewall security policies.
