<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.5.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action/v2.5.1** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): The 'Print Code Scanning PR URL' run: block directly interpolates GitHub Actions expressions into a shell echo command without routing through env vars: `echo "${{ github.server_url }}/${{ github.repository }}/security/code-scanning?query=pr%3A${{ github.event.pull_request.number }}"`. The expressions ${{ github.server_url }}, ${{ github.repository }}, and ${{ github.event.pull_request.number }} are substituted by the Actions template engine before the shell sees the string, enabling script injection if any value contains shell metacharacters.

Locations:

- `.github/workflows/osv-scanner-reusable-pr.yml:163`

### script-injection (severity: high)

Sub-rule (a): The 'Print Code Scanning URL' run: block directly interpolates GitHub Actions expressions into a shell echo command: `echo "${{ github.server_url }}/${{ github.repository }}/security/code-scanning?query=is%3Aopen+branch%3A${GITHUB_REF_NAME}+tool%3Aosv-scanner"`. The expressions ${{ github.server_url }} and ${{ github.repository }} are substituted by the Actions template engine before the shell sees the string, enabling script injection if any value contains shell metacharacters.

Locations:

- `.github/workflows/osv-scanner-reusable.yml:143`

### unpinned-uses (severity: high)

Both docker action files reference the container image `docker://ghcr.io/google/osv-scanner-action:v2.5.1` using a mutable version tag instead of an immutable SHA digest (e.g. `@sha256:<64-hex-char-digest>`). A tag can be silently repointed to a different image, enabling supply-chain attacks. The image reference must be pinned to a SHA digest.

Locations:

- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:24`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, unpinned-uses

**Notes:**

Fixed 3 findings: (1) Script injection in .github/workflows/osv-scanner-reusable-pr.yml line 163 - moved github.server_url, github.repository, and github.event.pull_request.number into env vars SERVER_URL, REPOSITORY, PR_NUMBER; (2) Script injection in .github/workflows/osv-scanner-reusable.yml line 143 - moved github.server_url and github.repository into env vars SERVER_URL, REPOSITORY; (3) Unpinned container image docker://ghcr.io/google/osv-scanner-action:v2.5.1 in both osv-reporter-action/action.yml and osv-scanner-action/action.yml pinned to @sha256:dcd947131d8d11b8d0964de6590661fb921a4ecbd7b90a7cb21083acfc3fd8cc while preserving the docker:// scheme and v2.5.1 tag inline.

