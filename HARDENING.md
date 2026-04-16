# Hardening Report: google--osv-scanner-action/v2.3.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `c40cfe5fa14e08549b1b988e7e5a26da4816abf0`

**Test Policy SHA:** `f2e7d85641cde4267138117189b8eba7ba2bfbde`

Action **google--osv-scanner-action/v2.3.5** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both Docker action files reference the container image `docker://ghcr.io/google/osv-scanner-action:v2.3.5` using a mutable version tag (`:v2.3.5`) instead of an immutable SHA digest. If the image at that tag is replaced or compromised, the action will silently execute the new content. The image reference should be pinned to a full SHA256 digest, e.g. `docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.3.5`.

Locations:

- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:26`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the container image `ghcr.io/google/osv-scanner-action:v2.3.5` to its immutable SHA256 digest in both action files:
- `osv-reporter-action/action.yml` (line 24): replaced `:v2.3.5` tag with `@sha256:512bc221cb77a33325bc92cf45c0c8a45f2689be8593dc4e541058590f4ce09f # v2.3.5`
- `osv-scanner-action/action.yml` (line 26): replaced `:v2.3.5` tag with `@sha256:512bc221cb77a33325bc92cf45c0c8a45f2689be8593dc4e541058590f4ce09f # v2.3.5`

The `# v2.3.5` comment is placed outside the YAML string quotes to preserve readability while ensuring the image reference is immutable.

