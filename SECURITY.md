# Security Policy

## Reporting a Vulnerability

Trooth, LLC welcomes responsible disclosure of security vulnerabilities affecting this library, the Trooth Operating System backend (`api.trooth.co`), the Trooth website (`trooth.co`), and the Trooth mobile applications. We treat all reports with the seriousness they deserve and we do not pursue legal action against good-faith security researchers who comply with this policy.

### How to Report

Send your report to **security@trooth.co**. Use PGP encryption if your report contains sensitive proof-of-concept material. Our PGP public key fingerprint is published at `https://trooth.co/security/pgp`.

Include the following information where available:

- A description of the vulnerability and its potential impact
- Step-by-step reproduction instructions
- The affected version of `@trooth/verifier`
- Any proof-of-concept code or screenshots
- Your name or handle (if you wish to be credited)
- Whether you have disclosed the vulnerability elsewhere

### Our Commitments

- **Acknowledgment within three (3) business days.** We will acknowledge receipt of your report and assign a tracking identifier.
- **Substantive response within ten (10) business days.** We will provide an initial assessment of the report, the expected timeline for remediation, and any clarifying questions.
- **Coordinated disclosure.** We will work with you on the timing of any public disclosure. Our standard window is ninety (90) days from acknowledgment, with extensions where the complexity of the fix requires it.
- **Credit.** We will credit reporters who request acknowledgment in our security advisories unless the reporter prefers to remain anonymous.

### Scope

In scope:

- This library `@trooth/verifier` and any code in this repository
- The Trust Receipt format specification documented in `docs/trust-receipt-format.md`
- The Trooth-published public-key distribution mechanism documented in this repository

Out of scope:

- The Trooth Operating System backend (`api.trooth.co`) and other Trooth proprietary services (report through the channel above, but they are subject to separate scope)
- Vendor-managed infrastructure (Cloudflare, GitHub, npm). Report to those vendors directly.
- Vulnerabilities in JavaScript or Node.js standard libraries (report to the upstream maintainers)
- Denial-of-service testing of any Trooth infrastructure without prior written authorization

### Severity and Remediation Targets

We classify and remediate vulnerabilities consistent with our published Vulnerability Management Policy:

| Severity | CVSS Range | Remediation Target |
|----------|------------|--------------------|
| Critical | 9.0-10.0 (or on CISA KEV) | Within 72 hours |
| High     | 7.0-8.9                  | Within 14 days    |
| Medium   | 4.0-6.9                  | Within 60 days    |
| Low      | 0.1-3.9                  | Within 180 days   |

### Safe Harbor

Trooth, LLC commits to the following safe harbor for security researchers acting in good faith and consistent with this policy:

- We will not initiate or support legal action against you for accessing or interacting with our systems for the limited purpose of identifying vulnerabilities.
- We will not initiate or support legal action against you for accessing data necessary to identify or reproduce a vulnerability, provided that you do not access, modify, exfiltrate, retain, or share more data than is necessary for that purpose.
- If a third party initiates legal action against you for research conducted under this policy, we will make it known that your activities were conducted in compliance with this policy.

You must comply with all applicable laws. You must not access, modify, exfiltrate, retain, or share customer data, and you must not disrupt the availability or integrity of services for customers.

### Out-of-Band Channel

If `security@trooth.co` is unreachable or appears to be compromised, send the report to **dandre@trooth.co** with the subject line `SECURITY OUT-OF-BAND`.

### Hall of Fame

Researchers who report valid vulnerabilities and who consent to public credit are listed at `https://trooth.co/security/hall-of-fame`.

---

This policy is governed by the **Trooth, LLC Vulnerability Management Policy** and **Incident Response Policy**. It is reviewed at least annually and upon any material change to the Company's products or threat environment.

_Last reviewed: June 8, 2026._
