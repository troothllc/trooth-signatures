# trust-verifier-sdk

Check a Trooth signature for yourself, with a public key and nothing else from Trooth.

Trooth operates the Trooth Network: one public, signed, machine-readable record per company, carrying its identity, products and demos, commercial terms, domain and marketing links, people, documents, security and privacy posture, AI practices, procurement terms and relationships. It is Trooth's only product and it is free.

DNS says where a company is. A TLS certificate says the connection is authentic. The Trooth Network says who the company is and what it does with your data.

**Trooth witnesses and dates facts. It does not score, rate, rank or certify anyone.** Trooth signs its own receipts and never signs on a company's behalf. So a valid Trooth signature tells you which key produced a set of bytes and that the bytes have not changed since. It does not tell you that anything written in them is true. Those are two different questions and this repository is only about the first.

## What is in this repository today

An Apache 2.0 licence, a contributing guide and a security policy. No library, no package, no code.

There is no `@trooth/verifier` on npm, and there is no `@trooth` scope. Trooth publishes one package, `trooth`, which is the command-line reader at [`troothllc/trooth-cli`](https://github.com/troothllc/trooth-cli). Anything that tells you to install `@trooth/verifier` is wrong, including every earlier version of this file.

The rest of this document is the verification this repository exists for, written so you can do it today with tools you already have. A library published here would run these steps and no others.

## The signing keys

Trooth signs with more than one key. Every signed artifact names the key that signed it, in `authority_key_id` or in `kid`, and the named key is looked up in the public key directory:

```
https://api.trooth.co/public/keys
```

No credential, no account. The same directory is rendered for people at [trooth.co/verify/keys](https://trooth.co/verify/keys).

The response carries a `keys` array and, alongside it, `active_kids`, a `note` and a disclaimer. `active_kid` names only one key and predates there being a second, so read `active_kids` when it is present. Each entry carries some of:

| Field | What it is |
|---|---|
| `kid` | The key id an artifact names. This is what you match on. |
| `public_key` | The Ed25519 public key. |
| `encoding` | How `public_key` is encoded. Read it. Do not guess. |
| `alg` | The algorithm. `Ed25519`. |
| `signs` | What this key signs. |
| `status` | `active`, or `revoked`. |
| `fingerprint` | A short value for eyeballing a key without comparing it character by character. |
| `created_at`, `revoked_at` | When the key came into use, and when it stopped. |

**Decode by the `encoding` field, always.** Trooth's keys do not agree with each other on encoding: one is hex and another is base64. A verifier that assumes one of them gets a signature failure that looks like tampering and is not.

A revoked key stays in the directory with `revoked_at` set, rather than disappearing. An artifact signed before that date is still a genuine artifact signed by that key; whether you still accept it is your policy, not Trooth's.

## Verifying a signed sign-off export

This is the path that works end to end today.

A buyer can download any sign-off from the Buyer workspace as a signed record. The file is the record in RFC 8785 canonical JSON, one line, exactly the bytes Trooth signed. The Ed25519 signature and the key id travel beside the file, never inside it: in a sidecar, and in the response headers `X-Trooth-Export-Signature`, `X-Trooth-Export-Kid`, `X-Trooth-Export-Alg`, `X-Trooth-Export-Signed-At` and `X-Trooth-Export-Keys`.

Save the file unchanged. One added newline and the signature no longer matches, which is the point of a detached signature over canonical bytes.

The public key for these exports is published separately from the record keys:

```
https://trooth.co/api/verify/export-keys
```

That response carries `keys`, `active_kids`, `alg`, `signs` and a `note`. Each key carries `kid`, `alg`, `public_key` (SPKI DER, base64), `encoding` (`spki-der-base64`), `public_key_pem` and `status`. The key id is derived from the key itself: the first 16 hex characters of SHA-256 over the SPKI DER, so it is the same id in every process and across deploys.

Take the key from that endpoint and not from the sidecar. One source should not supply both the document and the key it is checked against.

```bash
# 1. Fetch the directory and copy the public_key_pem of the key whose kid the
#    sidecar names into trooth-export-key.pem.
curl -s https://trooth.co/api/verify/export-keys

# 2. The signature is base64. Turn it back into the 64 raw bytes.
echo "<the signature>" | base64 -d > export.sig

# 3. Check it.
openssl pkeyutl -verify -pubin -inkey trooth-export-key.pem -rawin \
  -in trooth-signoff-<id>-<date>.json -sigfile export.sig
```

The same check in Node, using only the standard library:

```js
import { createPublicKey, verify } from "node:crypto";
import { readFileSync } from "node:fs";

// public_key from the directory, for the kid the sidecar names.
const pub = createPublicKey({
  key: Buffer.from(publicKeyBase64, "base64"),
  format: "der",
  type: "spki",
});

const sig = Buffer.from(signatureBase64, "base64"); // 64 bytes, or it is malformed
const ok = verify(null, readFileSync("trooth-signoff-<id>-<date>.json"), pub, sig);
```

Four outcomes, and they are worth keeping apart:

- **Valid.** These exact bytes were produced by the holder of that key and have not changed since.
- **Signature does not match.** Either the file changed after it was signed, by so much as one character of whitespace, or the signature belongs to a different file.
- **Malformed signature.** Not a well-formed Ed25519 signature, so there is nothing to check. Treat the file as unsigned.
- **Unknown key.** No published key has that id. It may have been made with a key Trooth has retired, or it may not be Trooth's. Nothing is asserted either way.

## What a valid signature proves, and what it does not

It proves the bytes and the signer. It does not prove the decision recorded in them was right, that the company is safe, or that any statement in the record is true.

Trooth's role here is a notary's. A notary stamps the act of signing and does not vouch for the document. Trooth's signature attests that a payload was recorded byte for byte at issuance, at the timestamp it carries. Assess the claims themselves the way you would for any credential whose issuer is a notary rather than an auditor. The crosswalk from verifiable-credential vocabulary to the Trooth field that plays each role is at [trooth.co/docs/verifiable-evidence](https://trooth.co/docs/verifiable-evidence).

## What you cannot check from public data yet

`trooth check <domain> --json` returns `receipt_signature` and `authority_key_id` for a listed company, and points at the key directory. The exact bytes that signature covers are not published, and the public JSON does not carry every field that goes into them, so a third party cannot reconstruct the signing input and re-run the check today.

That is a gap, it is stated here rather than left for you to discover, and closing it is what this repository is for: publishing the signing input, and the code that reproduces it, so the same rule applies to Trooth's own signatures as to everybody else's facts.

## Contributing

Contributions are licensed under Apache 2.0, the same as everything else here. Open an issue before a substantial change so the design can be argued about in the open rather than in a review.

## Security

Report a vulnerability through the [Vulnerability Disclosure Policy](https://trooth.co/security/vulnerability-disclosure-policy).

Nothing in this repository holds, reads or transmits a private key, and nothing here can issue a signature. Verification is public-key work only.

## Links

- The Network: [trooth.co/network](https://trooth.co/network)
- The signing keys: [trooth.co/verify/keys](https://trooth.co/verify/keys)
- Evidence formats and the notary semantics: [trooth.co/docs/verifiable-evidence](https://trooth.co/docs/verifiable-evidence)
- The command-line reader: [`troothllc/trooth-cli`](https://github.com/troothllc/trooth-cli), and [trooth.co/cli](https://trooth.co/cli)
- Developers: [trooth.co/developers](https://trooth.co/developers)
- Publish your own record, free: [trooth.co/get-started](https://trooth.co/get-started)
- Contact: [trooth.co/contact](https://trooth.co/contact)

## License

Apache License 2.0. See [LICENSE](LICENSE).

Trooth automates. Trooth never signs for you.
