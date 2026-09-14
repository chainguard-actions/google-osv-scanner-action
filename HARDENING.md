<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action/v2.6.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both Docker action files reference the container image 'docker://ghcr.io/google/osv-scanner-action:v2.6.0' using a mutable version tag (':v2.6.0') instead of an immutable SHA digest. This means the image content could change without notice, enabling supply-chain attacks. Each image reference should be pinned to a full SHA256 digest, e.g. 'docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.6.0'.

Locations:

- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:25`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the container image 'ghcr.io/google/osv-scanner-action:v2.6.0' to its immutable SHA256 digest in both osv-reporter-action/action.yml (line 24) and osv-scanner-action/action.yml (line 25). The image references now use the format 'docker://ghcr.io/google/osv-scanner-action:v2.6.0@sha256:71ad04ab2f8798be47870f9b18817ad317c2f8f2f97aa6726ba10d5578bc174a', preserving the docker:// scheme, the human-readable tag, and adding the immutable digest.

