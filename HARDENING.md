<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.5.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action/v2.5.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both Docker-based action files reference the container image 'docker://ghcr.io/google/osv-scanner-action:v2.5.1' using a mutable version tag (v2.5.1) instead of an immutable SHA digest. This means the image could be silently replaced with a different (potentially malicious) version without any change to the action files, creating a supply-chain attack risk. The image reference should be pinned to a SHA digest, e.g. 'docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.5.1'.

Locations:

- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:26`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the container image 'ghcr.io/google/osv-scanner-action:v2.5.1' to its immutable SHA digest in both osv-reporter-action/action.yml (line 24) and osv-scanner-action/action.yml (line 26). The docker:// scheme is preserved, the v2.5.1 tag is retained inline, and the digest 'sha256:dcd947131d8d11b8d0964de6590661fb921a4ecbd7b90a7cb21083acfc3fd8cc' is appended. Both references now use the format: 'docker://ghcr.io/google/osv-scanner-action:v2.5.1@sha256:dcd947131d8d11b8d0964de6590661fb921a4ecbd7b90a7cb21083acfc3fd8cc'.

