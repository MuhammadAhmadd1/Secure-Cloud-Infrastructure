# Identity Security & Hardening

This directory contains the customer-managed IAM policy used to enforce strict behavioral boundaries and structural guardrails for administrative users.

## Policy Overview: `Internee-Restricted-Admin-Policy`

* **Explicit Boundaries:** Allows standard operations across core engineering services (EC2 management, reading S3 data).
* **MFA Enforcement:** Implements a strict `Deny` mechanism. Critical actions like deleting policies or stopping the corporate audit trail (`cloudtrail:StopLogging`) are strictly blocked unless a hardware or virtual Multi-Factor Authentication token is explicitly active on the session.
