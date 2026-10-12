<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action--osv-reporter-action/v2.7.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action--osv-reporter-action/v2.7.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action image reference uses a mutable version tag instead of an immutable SHA digest. `image: "docker://ghcr.io/google/osv-scanner-action:v2.7.0"` should be pinned to a full SHA256 digest (e.g. `image: "docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.7.0"`) to prevent supply-chain attacks where the tag is silently moved to a different image.

Locations:

- `action.yml:25`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker container image in action.yml from the mutable tag `docker://ghcr.io/google/osv-scanner-action:v2.7.0` to the immutable digest `docker://ghcr.io/google/osv-scanner-action:v2.7.0@sha256:d54770fe0b09493894e76a02aaed9f51a0513fa57c5186452a755d257b0068a6`. The `docker://` scheme and inline tag are preserved as required.

