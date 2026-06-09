# Hardening Report: google--osv-scanner-action/v2.3.8

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **google--osv-scanner-action/v2.3.8** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both docker action files reference the container image `docker://ghcr.io/google/osv-scanner-action:v2.3.8` using a mutable version tag instead of an immutable SHA digest. This means the image could be replaced with a different (potentially malicious) version without changing the action configuration, creating a supply-chain risk. The image reference should use a SHA digest, e.g. `docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest>`.

Failing references:
- `osv-reporter-action/action.yml` line 25: `image: "docker://ghcr.io/google/osv-scanner-action:v2.3.8"`
- `osv-scanner-action/action.yml` line 27: `image: "docker://ghcr.io/google/osv-scanner-action:v2.3.8"`

Locations:

- `osv-reporter-action/action.yml:25`
- `osv-scanner-action/action.yml:27`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the container image `ghcr.io/google/osv-scanner-action:v2.3.8` to its immutable SHA digest `sha256:48406c58197201fe55e56615ad9d414f85063da320e204d0b0ed460fb3908dba` in both:
- `osv-reporter-action/action.yml` (line 25)
- `osv-scanner-action/action.yml` (line 27)

The version tag `v2.3.8` is preserved as a comment outside the YAML string quotes for readability.

