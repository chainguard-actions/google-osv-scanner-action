<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action--osv-scanner-action/v2.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action--osv-scanner-action/v2.6.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action image is referenced by a mutable version tag (`v2.6.0`) rather than an immutable SHA digest. This means a supply-chain compromise of the image registry could silently replace the image. The reference `docker://ghcr.io/google/osv-scanner-action:v2.6.0` should be changed to use a SHA digest, e.g. `docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.6.0`.

Locations:

- `action.yml:27`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker container image reference in action.yml from `docker://ghcr.io/google/osv-scanner-action:v2.6.0` to `docker://ghcr.io/google/osv-scanner-action:v2.6.0@sha256:71ad04ab2f8798be47870f9b18817ad317c2f8f2f97aa6726ba10d5578bc174a`. The docker:// scheme and version tag are preserved; the SHA digest makes the reference immutable.

