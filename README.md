# @trooth/verifier

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![OpenSSF Best Practices](https://img.shields.io/badge/OpenSSF-Best%20Practices-blue)](https://bestpractices.dev/)
[![npm version](https://img.shields.io/npm/v/@trooth/verifier.svg)](https://www.npmjs.com/package/@trooth/verifier)

> **Independently verify any Trooth Trust Receipt without trusting Trooth.**

`@trooth/verifier` is the open-source library for verifying the cryptographic authenticity, integrity, and timestamp of any Trust Receipt issued by Trooth. The library implements standard Ed25519 signature verification and RFC 3161 Time-Stamp Authority verification against Trooth's published public keys.

You do not need to trust Trooth's infrastructure. You verify the math.

---

## Why this exists

Trooth, LLC (https://trooth.co) issues cryptographically signed Trust Receipts for compliance scans, vendor attestations, and audit chain entries. Each Receipt contains:

- The subject of the receipt (vendor identifier, scan identifier, audit entry hash)
- A timestamp anchored to an RFC 3161 Time-Stamp Authority
- Trooth's Ed25519 signature over the receipt content
- The published Trooth public key identifier used for the signature

This library lets any consumer of a Trust Receipt verify that:

1. The receipt was signed by Trooth (signature is valid against Trooth's published public key)
2. The receipt has not been tampered with since issuance (signed content hash matches)
3. The receipt's timestamp is real (RFC 3161 TSA token is valid)
4. The receipt has not expired (if expiration is set)

If all four checks pass, the receipt is genuine. If any fails, the receipt is rejected.

---

## Installation

```bash
npm install @trooth/verifier
```

Or with pnpm or yarn:

```bash
pnpm add @trooth/verifier
yarn add @trooth/verifier
```

---

## Quick start

```typescript
import { verifyTrustReceipt } from "@trooth/verifier";

// A Trust Receipt obtained from a Trooth API response or downloaded receipt
const receipt = {
  subject: "vendor:acme-ai-2026",
  issuedAt: "2026-06-08T12:00:00Z",
  contentHash: "sha256:abc123...",
  signature: "ed25519:def456...",
  keyId: "trooth-prod-2026",
  timestamp: "RFC3161:...",
};

const result = await verifyTrustReceipt(receipt);

if (result.valid) {
  console.log("Receipt is valid. Issued at:", result.verifiedTimestamp);
} else {
  console.error("Receipt is invalid:", result.reason);
}
```

---

## What this library does

- ✅ Verifies Ed25519 signatures against Trooth's published public keys
- ✅ Validates RFC 3161 timestamp tokens against trusted Time-Stamp Authorities
- ✅ Compares the receipt's content hash to the signed content
- ✅ Checks expiration if present
- ✅ Returns a structured result with detailed failure reasons

## What this library does NOT do

- ❌ Issue Trust Receipts (only Trooth's servers can do that with the private signing key)
- ❌ Reveal Trooth's internal scoring, scanning, or audit logic
- ❌ Contact Trooth's servers (verification is offline; only the public key is needed)
- ❌ Replace the Trooth platform (this library is for verification only)

---

## Public key distribution

Trooth's current and historical public keys are distributed in three ways:

1. **Bundled with this library.** The most recently published public keys are included in `src/public-keys.ts` for offline verification. Update the library to receive new keys.
2. **Hosted at `https://trooth.co/.well-known/trust-receipt-keys.json`.** Use this if your application has network access and you want automatic key rotation handling.
3. **DNS TXT records on `_trooth-keys.trooth.co`.** DNSSEC-validated key distribution for high-assurance environments.

This library defaults to bundled keys. To use the hosted endpoint, pass `{ keySource: "https" }` to the verifier.

---

## API reference

### `verifyTrustReceipt(receipt, options?)`

The primary verification function.

```typescript
async function verifyTrustReceipt(
  receipt: TrustReceipt,
  options?: VerifyOptions
): Promise<VerifyResult>;
```

**Parameters**

- `receipt`: A Trust Receipt object conforming to the schema in `docs/trust-receipt-format.md`.
- `options` (optional):
  - `keySource`: `"bundled"` (default) or `"https"`.
  - `clockSkewSeconds`: Acceptable clock skew (default 300).
  - `acceptExpired`: Set `true` to verify expired receipts (default `false`).

**Returns**

```typescript
{
  valid: boolean;
  reason?: string;          // Set when valid is false
  verifiedTimestamp?: Date; // Set when valid is true
  keyId?: string;
  subject?: string;
}
```

### `verifyTrustReceiptBatch(receipts, options?)`

Verifies an array of receipts in parallel. Useful when verifying an audit chain.

### `parseTrustReceipt(input)`

Parses a Trust Receipt from a JSON string, a buffer, or a base64-encoded string. Returns a typed `TrustReceipt` object or throws if malformed.

---

## Security

If you discover a vulnerability in this library, please refer to `SECURITY.md` for the responsible disclosure process. **Do not open a public issue for security vulnerabilities.**

This library implements only verification (public-key cryptographic operations). It does not handle private keys, sign data, or perform any operation that could result in unauthorized issuance of receipts. The attack surface is therefore limited to:

- Incorrect signature verification logic (mitigated by reliance on platform-provided crypto libraries)
- Incorrect timestamp validation logic
- Failure to detect tampering (mitigated by comprehensive test coverage)

The library has been designed to meet the **OpenSSF Best Practices Badge** criteria including secure development, vulnerability disclosure, public release notes, and CI-enforced testing.

---

## Contributing

See `CONTRIBUTING.md`. Pull requests welcome. Trooth, LLC reviews each PR for security and correctness before merging.

This project follows the **Contributor Covenant 2.1** Code of Conduct. See `CODE_OF_CONDUCT.md`.

---

## License

Apache License 2.0. See `LICENSE` for the full text.

Copyright (c) 2026 Trooth, LLC. All rights reserved.

---

## About Trooth

Trooth is the cryptographic compliance protocol platform. Trooth issues verifiable Trust Receipts so that any party can independently confirm that an AI vendor, software supplier, or service provider has been scanned, attested, and continuously monitored against published standards.

Learn more at **https://trooth.co**.

The Trooth platform is closed source and proprietary. This verifier library, however, is open source so that any consumer of a Trust Receipt can independently verify it without trusting Trooth.

This is by design. Trust, but verify.
