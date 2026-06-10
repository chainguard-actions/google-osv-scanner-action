<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.3.8

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **google--osv-scanner-action/v2.3.8** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both Docker action files reference the container image `docker://ghcr.io/google/osv-scanner-action:v2.3.8` using a mutable version tag (`:v2.3.8`) instead of an immutable SHA digest. A mutable tag can be silently updated to point to a different (potentially malicious) image, enabling supply-chain attacks. The image reference should use a SHA digest, e.g. `docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest>`.

Locations:

- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:24`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable tag reference `docker://ghcr.io/google/osv-scanner-action:v2.3.8` with the immutable SHA digest `docker://ghcr.io/google/osv-scanner-action@sha256:48406c58197201fe55e56615ad9d414f85063da320e204d0b0ed460fb3908dba` in both:
- osv-reporter-action/action.yml (line 24)
- osv-scanner-action/action.yml (line 24)

The original tag is preserved as a comment `# v2.3.8` outside the YAML string quotes for readability.

