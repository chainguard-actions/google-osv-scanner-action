<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action--osv-reporter-action/v2.5.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action--osv-reporter-action/v2.5.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action's `runs.image` references a mutable image tag (`v2.5.1`) instead of an immutable SHA digest. If the tag is moved or the registry is compromised, a different (potentially malicious) image could be pulled silently. Failing reference: `image: "docker://ghcr.io/google/osv-scanner-action:v2.5.1"`. It should be pinned to a full SHA256 digest, e.g. `image: "docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.5.1"`.

Locations:

- `action.yml:25`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from `docker://ghcr.io/google/osv-scanner-action:v2.5.1` to `docker://ghcr.io/google/osv-scanner-action:v2.5.1@sha256:dcd947131d8d11b8d0964de6590661fb921a4ecbd7b90a7cb21083acfc3fd8cc`. The tag is kept inline alongside the digest for readability, and the `docker://` scheme is preserved so GitHub Actions correctly treats this as a pre-built image rather than a local Dockerfile.

