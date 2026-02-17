# Implementing and Testing App-ID Application Filtering on Palo Alto Firewall


### STEP 1: Modify Security Rule

I navigated to:

Policies → Security → Trust-to-Internet

Updated the rule:

- Changed Application from `any` to `web-browsing`
- Service set to `application-default`

Committed the configuration successfully.

---

### STEP 2: Test from Ubuntu

Performed browser testing:

- Accessed google.com successfully
- youtube.com was blocked as expected

---

### STEP 3: Check Traffic Logs

Navigated to:

Monitor → Traffic

Verified:

- Allowed traffic showed `web-browsing`
- youtube traffic was blocked

---

## Status

Application-based filtering using App-ID has been successfully implemented and validated.
