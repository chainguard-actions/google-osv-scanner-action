<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action--osv-reporter-action/v2.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action--osv-reporter-action/v2.6.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The Docker action references a mutable image tag instead of an immutable SHA digest. `image: "docker://ghcr.io/google/osv-scanner-action:v2.6.0"` uses the tag `v2.6.0`, which can be silently repointed to a different (potentially malicious) image. It should be pinned to a full SHA256 digest, e.g. `image: "ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.6.0"`.

Locations:

- `action.yml:24`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from `docker://ghcr.io/google/osv-scanner-action:v2.6.0` to `docker://ghcr.io/google/osv-scanner-action:v2.6.0@sha256:71ad04ab2f8798be47870f9b18817ad317c2f8f2f97aa6726ba10d5578bc174a`, preserving the docker:// scheme and the tag inline for readability.

