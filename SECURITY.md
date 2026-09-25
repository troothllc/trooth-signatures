# Security Policy

## Reporting a Vulnerability

Trooth, LLC welcomes responsible disclosure of security vulnerabilities affecting this repository, the API at `api.trooth.co` and the website `trooth.co`. We treat all reports with the seriousness they deserve and we do not pursue legal action against good-faith security researchers who comply with this policy.

This file is the repository-level summary. The governing document is the [Vulnerability Disclosure Policy](https://trooth.co/security/vulnerability-disclosure-policy) on trooth.co. Where this file and that policy differ, the policy applies.

### How to Report

Send your report to **security@trooth.co**. That is the address in [security.txt](https://trooth.co/.well-known/security.txt).

Trooth publishes no PGP key at any URL. If your report contains sensitive proof-of-concept material, send a first email without it and ask how to send it.

Include the following information where available:

- A description of the vulnerability and its potential impact
- Step-by-step reproduction instructions
- The affected repository, endpoint or document
- Any proof-of-concept code or screenshots
- Your name or handle (if you wish to be credited)
- Whether you have disclosed the vulnerability elsewhere

Reports written in English are processed fastest.

### Our Commitments

These are the commitments the Vulnerability Disclosure Policy makes:

- **Acknowledgment within three (3) business days.** We acknowledge receipt of every report.
- **Substantive response within ten (10) business days,** with our assessment and an expected remediation timeline.
- **Progress.** We keep you informed as we work toward a fix.
- **Coordinated disclosure.** We ask that you give us a reasonable opportunity to remediate a reported vulnerability before disclosing it publicly, and we will work with you in good faith to agree on a disclosure timeline.
- **Credit.** We are happy to credit you publicly once the issue is resolved, if you wish.

### Scope

In scope for this file:

- Any code in this repository. Today there is none: the repository holds a license, a contributing guide, this policy and a README.
- The signature-checking steps the README documents, where following them as written would lead a reader to accept a signature that does not match, or to reject a genuine one.

In scope under the Vulnerability Disclosure Policy rather than this file, reported to the same address:

- `trooth.co` and the API at `api.trooth.co`, including the two public key directories the README documents (`https://api.trooth.co/public/keys` and `https://trooth.co/api/verify/export-keys`).

Out of scope:

- Third-party services Trooth uses as sub-processors, and vendor-managed infrastructure (Cloudflare, GitHub, npm). Report to those providers under their own disclosure programs.
- Vulnerabilities in JavaScript, Node.js or OpenSSL themselves (report to the upstream maintainers)
- Volumetric denial-of-service attacks against any Trooth infrastructure
- Social engineering of Trooth personnel or customers, and physical attacks against Trooth facilities or staff
- Output from automated tools without a demonstrated impact, and missing security headers or best-practice recommendations without a concrete exploit

### Severity and Remediation Targets

Severity and remediation timelines are set by Trooth's published [Vulnerability Management Policy (POL-07)](https://trooth.co/trust/policies/POL-07-vulnerability-management-policy.pdf). This file does not restate them: an earlier version carried a table of targets that did not match that policy.

### Safe Harbor

As the Vulnerability Disclosure Policy states it: Trooth, LLC will not pursue legal action against security researchers who act in good faith and comply with the policy. Good faith means you make a reasonable effort to avoid privacy violations, degradation of service, and destruction or exfiltration of data; you do not access, modify, or retain customer data beyond the minimum necessary to demonstrate a vulnerability; and you give Trooth a reasonable opportunity to remediate before any public disclosure.

You must comply with all applicable laws.

### Reporting Channel

`security@trooth.co` is the one reporting address Trooth publishes, in this file, in `security.txt` and in the Vulnerability Disclosure Policy.

### Credit

The Vulnerability Disclosure Policy offers public credit once the issue is resolved, if you wish. Trooth publishes no separate list of researchers.

---

This file summarizes the [Vulnerability Disclosure Policy](https://trooth.co/security/vulnerability-disclosure-policy), which governs.

_Last reviewed: September 25, 2026._
