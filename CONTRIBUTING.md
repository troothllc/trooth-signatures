# Contributing to @trooth/verifier

Thank you for your interest in contributing to this library. This document sets out how to report issues, propose changes, and submit pull requests. By participating, you agree to abide by the **Code of Conduct** (`CODE_OF_CONDUCT.md`) and the project's Apache License 2.0 (`LICENSE`).

---

## Code of Conduct

This project follows the Contributor Covenant 2.1. See `CODE_OF_CONDUCT.md`. Reports of unacceptable behavior may be made to **conduct@trooth.co**.

---

## Reporting Bugs

If the bug is a security vulnerability, follow the disclosure process in `SECURITY.md`. **Do not open a public issue for security vulnerabilities.**

For non-security bugs:

1. Search the issue tracker to confirm the bug has not already been reported.
2. Open a new issue using the **Bug Report** template.
3. Include:
   - Version of `@trooth/verifier` (commit SHA or release tag)
   - Node.js version and operating system
   - A minimal reproduction (ideally a failing test case)
   - Expected vs actual behavior
   - Any relevant error output (with secrets and personal data redacted)

We will respond within five (5) business days.

---

## Proposing Features

1. Search the issue tracker for prior consideration.
2. Open a new issue using the **Feature Proposal** template.
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

1. Fork the repository and create a feature branch off of `main`. Branch name should be descriptive (for example, `fix/timestamp-clock-skew`).
2. Ensure the change is the smallest reasonable unit of work.
3. Add or update tests covering the change.
4. Run the test suite locally and confirm it passes.
5. Run the linter and type checker locally and confirm both are clean.
6. Sign your commits (`git commit -S`). The project requires signed commits on the production branch.
7. Reference any related issue in the pull request description (for example, `Fixes #123`).

Pull request expectations:

- **Commits.** Clear, imperative commit messages (`Add foo`, not `Added foo`).
- **Tests.** Include automated tests sufficient to demonstrate the change and prevent regression.
- **Documentation.** Update README, in-repository documentation, and code comments where the public interface or behavior changes.
- **Security.** Do not commit secrets. Run the project's secret scanner locally.
- **License.** By submitting a pull request you license your contribution under the project's Apache License 2.0.

Review process:

- A reviewer will respond within five (5) business days.
- Reviewers may request changes, ask questions, or merge.
- Once approved and CI is green, a maintainer will merge the pull request.

---

## Development Setup

```bash
git clone https://github.com/trooth-llc/trust-verifier-sdk.git
cd trust-verifier-sdk
npm install
npm test
```

Required tooling:

- Node.js 20 LTS or later
- TypeScript 5.x (installed as a dev dependency)

---

## Style and Conventions

- **Code formatting.** Prettier (run with `npm run format`).
- **Type safety.** TypeScript strict mode enforced.
- **Naming.** Descriptive identifiers, no abbreviations.
- **Comments.** Explain why, not what. Code should be self-evident on what.
- **Crypto.** Use platform-provided primitives only. No custom cryptographic implementations.

---

## Dependencies

When introducing a new dependency:

1. Confirm the license is Apache 2.0, MIT, BSD, or ISC.
2. Confirm the dependency is actively maintained.
3. Confirm the dependency has no known unresolved Critical or High vulnerabilities.
4. Pin to a specific version in `package-lock.json`.
5. Document the rationale in the pull request.

This library minimizes dependencies on principle. Cryptographic operations rely on Node's built-in `crypto` module and the platform-provided Web Crypto API.

---

## Releases and Versioning

Releases follow semantic versioning (`MAJOR.MINOR.PATCH`):

- **MAJOR** for breaking changes to the public API
- **MINOR** for new functionality preserving backward compatibility
- **PATCH** for backward-compatible bug fixes

A change log is maintained in `CHANGELOG.md`. Update the change log under `## Unreleased` when your change ships observable behavior.

---

## Communication

- **Issues** for bugs, feature proposals, and tracked work
- **Discussions** for open-ended technical conversation
- **security@trooth.co** for vulnerability disclosure (see `SECURITY.md`)
- **conduct@trooth.co** for Code of Conduct reports

Trooth, LLC reserves the right to remove or modify any contribution that does not comply with this document or the Apache License 2.0.

---

_Last reviewed: June 8, 2026._
