# Cloud Auditing & Log Integrity

This directory contains the configuration and security policies used to establish an immutable audit trail for the entire AWS infrastructure.

## Mechanism Overview

### 1. Multi-Region Tracking
AWS CloudTrail is configured as a Multi-Region trail (`internee-organization-audit-trail`). This ensures that any unauthorized action or resource creation in an unused or distant AWS region is instantly captured and centralized, eliminating blind spots.

### 2. Log File Integrity Validation
To prevent log tampering by malicious actors or compromised internal accounts, **Log File Integrity Validation** is enabled. 
* **How it works:** CloudTrail automatically generates a cryptographic digest file every hour. 
* **The Math:** This digest file contains the cryptographic hashes (MD5) of the log files delivered during that hour and is digitally signed by AWS using RSA public key encryption.
* **The Security Impact:** If an attacker attempts to alter, modify, or delete a log file to hide their tracks, the calculated hash will not match the digital signature in the digest file, immediately triggering a high-severity alert.

## Storage Security
Logs are securely streamed to a dedicated S3 bucket (`internee-secure-audit-logs-ahmad1`). Access is governed via a strict bucket policy (`bucket-policy.json`) that restricts write permissions exclusively to the AWS CloudTrail service principal.
