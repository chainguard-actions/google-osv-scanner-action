<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action/v2.5.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both docker-based action files reference the container image `docker://ghcr.io/google/osv-scanner-action:v2.5.0` using a mutable version tag instead of an immutable SHA digest. If the tag is moved to a different image, the action will silently execute different code, enabling a supply-chain attack. The image reference should use a SHA digest, e.g. `docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest> # v2.5.0`.

Locations:

- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:26`

### script-injection (severity: high)

Sub-rule (a): GitHub Actions expressions are interpolated directly inside `run:` shell command strings. In `osv-scanner-reusable-pr.yml`, the 'Print Code Scanning PR URL' step embeds `${{ github.server_url }}`, `${{ github.repository }}`, and `${{ github.event.pull_request.number }}` directly in an `echo` command. In `osv-scanner-reusable.yml`, the 'Print Code Scanning URL' step embeds `${{ github.server_url }}` and `${{ github.repository }}` directly in an `echo` command. Any `${{ ... }}` expression inside a `run:` block is subject to YAML template substitution before the shell processes it, making it a script-injection vector regardless of which context it reads from. These values should be passed via `env:` variables and referenced as `$ENV_VAR` in the shell script instead.

Locations:

- `.github/workflows/osv-scanner-reusable-pr.yml:155`
- `.github/workflows/osv-scanner-reusable.yml:131`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, script-injection

**Notes:**

Fixed two categories of findings:

1. **unpinned-uses** (both action.yml files): Pinned `docker://ghcr.io/google/osv-scanner-action:v2.5.0` to its immutable SHA256 digest `sha256:4cc9d6b5a6bb3a81c38c8d1610f6855512ddd1ba5af77083a856f171dbd0d463` in both `osv-reporter-action/action.yml` and `osv-scanner-action/action.yml`. The `docker://` scheme and `:v2.5.0` tag are preserved inline.

2. **script-injection** (both reusable workflow files):
   - In `osv-scanner-reusable-pr.yml` (line 155): Moved `${{ github.server_url }}`, `${{ github.repository }}`, and `${{ github.event.pull_request.number }}` out of the `run:` block into an `env:` block as `SERVER_URL`, `REPOSITORY`, and `PR_NUMBER`, then referenced them as shell variables.
   - In `osv-scanner-reusable.yml` (line 131): Moved `${{ github.server_url }}` and `${{ github.repository }}` out of the `run:` block into the existing `env:` block as `SERVER_URL` and `REPOSITORY`, then referenced them as shell variables. `GITHUB_REF_NAME` was already correctly placed in `env:`.

