<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.7.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action/v2.7.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both Docker action sub-actions reference the container image `ghcr.io/google/osv-scanner-action` using a mutable version tag (`v2.7.0`) instead of an immutable SHA digest. If the tag is moved to a different image (e.g., via a supply-chain compromise), the action will silently execute the new, potentially malicious image. The `image:` field should use a SHA digest, e.g. `docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.7.0`.

Failing references:
- `osv-reporter-action/action.yml`: `image: "docker://ghcr.io/google/osv-scanner-action:v2.7.0"`
- `osv-scanner-action/action.yml`: `image: "docker://ghcr.io/google/osv-scanner-action:v2.7.0"`

Locations:

- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:26`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the container image `ghcr.io/google/osv-scanner-action:v2.7.0` to its immutable SHA digest in both sub-action files:
- `osv-reporter-action/action.yml` line 24: image now references `docker://ghcr.io/google/osv-scanner-action:v2.7.0@sha256:d54770fe0b09493894e76a02aaed9f51a0513fa57c5186452a755d257b0068a6`
- `osv-scanner-action/action.yml` line 26: same pinned image reference applied

The `docker://` scheme is preserved, the version tag is kept inline for readability, and the SHA digest makes the reference immutable against tag-moving attacks.

