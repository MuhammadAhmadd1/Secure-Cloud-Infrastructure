# Edge Layer Defense & Web Application Firewall (WAF)

This directory documents the Layer 7 network security defense implemented to protect downstream application interfaces against automated web exploits and malicious payload manipulation.

## Implemented Architecture

* **Web ACL Name:** `internee-edge-protection`
* **Default Behavior:** `Allow` (Pass-through for legitimate traffic patterns).
* **Inspection Scope:** Layer 7 HTTP/HTTPS incoming requests (headers, query strings, URI parameters, and body payloads).

## Prioritized Core Managed Rule Groups

Instead of creating highly complex, fragile regex-based firewall rules from scratch, we have deployed two foundational rule sets curated and maintained by the AWS Threat Research Team:

1. **AWS Core Rule Set (CRS) (`AWSManagedRulesCommonRuleSet`):** 
   * *Strategic Priority:* Provides complete baseline protection against a wide cross-section of the OWASP Top 10 vulnerabilities. It targets common attack methodologies such as Cross-Site Scripting (XSS), Local File Inclusion (LFI), path traversal vectors, and remote script injection.
2. **SQL Database Rule Set (`AWSManagedRulesSQLiRuleSet`):**
   * *Strategic Priority:* Mitigates database reconnaissance and unauthorized extraction techniques. It continuously scans request streams for signatures of SQL Injection (SQLi), where attackers attempt to bypass system logic by injecting database commands via input text forms or API strings.
