<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.3.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **google--osv-scanner-action/v2.3.2** was hardened automatically. 1 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The docker action image reference uses a mutable version tag (`v2.3.2`) instead of an immutable SHA digest. This means the image could be silently replaced with a different (potentially malicious) version. The reference `docker://ghcr.io/google/osv-scanner-action:v2.3.2` should be pinned to a SHA digest, e.g. `docker://ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest>`.

Locations:

- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:26`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the container image `ghcr.io/google/osv-scanner-action:v2.3.2` to its immutable SHA digest `sha256:ade1325102b76c3e4e46e6fac7990048f1c1f8ea105e0798340e2b003cd7c328` in both `osv-reporter-action/action.yml` (line 24) and `osv-scanner-action/action.yml` (line 26). The mutable `v2.3.2` tag is preserved as a comment outside the YAML string for readability.

### Iteration 2

**Fixes applied:** script-injection, unpinned-uses

**Notes:**

Fixed 3 findings across 2 files:
1. osv-scanner-reusable-pr.yml: Moved ${{ github.server_url }}, ${{ github.repository }}, and ${{ github.event.pull_request.number }} out of the 'Print Code Scanning PR URL' run block into env vars (SERVER_URL, REPOSITORY, PR_NUMBER), referencing them as plain shell variables.
2. osv-scanner-reusable.yml: Moved ${{ github.server_url }}, ${{ github.repository }}, and ${{ github.ref_name }} out of the 'Print Code Scanning URL' run block into env vars (SERVER_URL, REPOSITORY, REF_NAME), referencing them as plain shell variables.
3. osv-scanner-reusable.yml: Pinned actions/download-artifact@v7 to full commit SHA 37930b1c2abaa49bbe596cd826c3c89aef350131 with a # v7 comment.

