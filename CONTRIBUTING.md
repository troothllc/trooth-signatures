# Contributing to trooth-signatures

Thank you for your interest in contributing to this repository. This document sets out how to report issues, propose changes, and submit pull requests. By participating, you agree to abide by the **Code of Conduct** and the project's Apache License 2.0 (`LICENSE`).

This repository holds no code today: a license, this guide, a security policy and a README that documents how to check a Trooth signature with OpenSSL or Node.js. There is no package and no `@trooth/verifier` on npm. Until code lands here, a pull request is a documentation change.

---

## Code of Conduct

This project follows the Contributor Covenant 2.1, through the organization's `CODE_OF_CONDUCT.md` in [troothllc/.github](https://github.com/troothllc/.github). Reports of unacceptable behavior may be made to **hello@trooth.co**.

---

## Reporting Bugs

If the bug is a security vulnerability, follow the disclosure process in `SECURITY.md`. **Do not open a public issue for security vulnerabilities.**

For non-security bugs, including a step in the README that does not work as written:

1. Search the issue tracker to confirm the bug has not already been reported.
2. Open a new issue using the **Bug report** template.
3. Include:
   - The commit SHA of the README you followed
   - Your OpenSSL or Node.js version and operating system
   - A minimal reproduction
   - Expected vs actual behavior
   - Any relevant error output (with secrets and personal data redacted)

---

## Proposing Features

1. Search the issue tracker for prior consideration.
2. Open a new issue using the **Feature request** template.
3. Describe:
   - The problem the feature would address
   - The intended use case
   - A proposed solution at a high level
   - Alternatives considered
   - Trade-offs (security, performance, complexity)

Substantive features warrant a short design discussion in the issue before implementation.

---

## Submitting Pull Requests

Before opening a pull request:

1. Fork the repository and create a feature branch off of `main`. Branch name should be descriptive (for example, `docs/key-directory-fields`).
2. Ensure the change is the smallest reasonable unit of work.
3. If the change adds code, add tests covering it.
4. If you changed a command or code sample in the README, run it and confirm it works as written.
5. Sign your commits (`git commit -S`).
6. Reference any related issue in the pull request description (for example, `Fixes #123`).

Pull request expectations:

- **Commits.** Clear, imperative commit messages (`Add foo`, not `Added foo`).
- **Tests.** Where the change adds code, include automated tests sufficient to demonstrate the change and prevent regression.
- **Documentation.** Update the README, in-repository documentation, and code comments where the public interface or behavior changes.
- **Security.** Do not commit secrets or private keys.
- **License.** By submitting a pull request you license your contribution under the project's Apache License 2.0.

Review process:

- Reviewers may request changes, ask questions, or merge.
- There is no CI in this repository yet. Once a pull request is approved, a maintainer will merge it.

---

## Development Setup

```bash
git clone https://github.com/troothllc/trooth-signatures.git
cd trooth-signatures
```

There is no `package.json`, so there is nothing to install or test yet.

Tooling the README's steps use:

- OpenSSL 3.0 or later (the `-rawin` option first appeared in 3.0)
- Node.js, for the standard-library example

---

## Style and Conventions

For code added to this repository:

- **Naming.** Descriptive identifiers, no abbreviations.
- **Comments.** Explain why, not what. Code should be self-evident on what.
- **Crypto.** Use platform-provided primitives only. No custom cryptographic implementations.

---

## Dependencies

When introducing a new dependency:

1. Confirm the license is Apache 2.0, MIT, BSD, or ISC.
2. Confirm the dependency is actively maintained.
3. Confirm the dependency has no known unresolved Critical or High vulnerabilities.
4. Pin to a specific version in the lockfile.
5. Document the rationale in the pull request.

The README's steps need nothing beyond OpenSSL and Node's built-in `crypto` module, and code added here should keep to platform-provided cryptography in the same way.

---

## Releases and Versioning

There are no releases and no `CHANGELOG.md` yet. A release from this repository follows semantic versioning (`MAJOR.MINOR.PATCH`):

- **MAJOR** for breaking changes to the public API
- **MINOR** for new functionality preserving backward compatibility
- **PATCH** for backward-compatible bug fixes

---

## Communication

- **Issues** for bugs, feature proposals, and questions
- **security@trooth.co** for vulnerability disclosure (see `SECURITY.md`)
- **hello@trooth.co** for Code of Conduct reports

Trooth, LLC reserves the right to remove or modify any contribution that does not comply with this document or the Apache License 2.0.

---

_Last reviewed: September 25, 2026._
