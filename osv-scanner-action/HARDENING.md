<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action--osv-scanner-action/v2.5.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action--osv-scanner-action/v2.5.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action's `runs.image` field references a mutable image tag (`v2.5.1`) instead of an immutable SHA digest. This means the image pulled at runtime could change without notice, enabling a supply-chain attack. The reference `docker://ghcr.io/google/osv-scanner-action:v2.5.1` should be replaced with a SHA-pinned form such as `docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.5.1`.

Locations:

- `action.yml:30`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker container image in action.yml from the mutable tag `docker://ghcr.io/google/osv-scanner-action:v2.5.1` to the immutable digest form `docker://ghcr.io/google/osv-scanner-action:v2.5.1@sha256:dcd947131d8d11b8d0964de6590661fb921a4ecbd7b90a7cb21083acfc3fd8cc`. The `docker://` scheme is preserved as required for Docker container actions, and the tag is kept inline alongside the digest.

