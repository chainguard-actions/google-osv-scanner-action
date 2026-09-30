<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action/v2.6.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both docker action files reference the container image `docker://ghcr.io/google/osv-scanner-action:v2.6.0` using a mutable version tag (`v2.6.0`) instead of an immutable SHA digest. A tag can be silently moved to point to a different (potentially malicious) image, enabling supply-chain attacks. The image reference should use a SHA digest, e.g. `docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.6.0`.

Locations:

- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:27`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the container image `ghcr.io/google/osv-scanner-action:v2.6.0` to its immutable SHA digest `sha256:71ad04ab2f8798be47870f9b18817ad317c2f8f2f97aa6726ba10d5578bc174a` in both:
- `osv-reporter-action/action.yml` (line 24)
- `osv-scanner-action/action.yml` (line 27)

The `docker://` scheme is preserved, the tag `v2.6.0` is kept inline for readability, and the digest is appended in the format `docker://ghcr.io/google/osv-scanner-action:v2.6.0@sha256:<digest>`.

