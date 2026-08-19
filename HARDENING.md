<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.3.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action/v2.3.5** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): A run: block in the 'Print Code Scanning PR URL' step directly interpolates GitHub Actions expressions into a shell command string. The line `echo "${{ github.server_url }}/${{ github.repository }}/security/code-scanning?query=pr%3A${{ github.event.pull_request.number }}"` embeds ${{ github.server_url }}, ${{ github.repository }}, and ${{ github.event.pull_request.number }} directly inside a run: shell command. These values are substituted by the template engine before the shell ever sees them, enabling script injection if any value contains shell metacharacters.

Locations:

- `.github/workflows/osv-scanner-reusable-pr.yml:119`

### script-injection (severity: high)

Sub-rule (a): A run: block in the 'Print Code Scanning URL' step directly interpolates GitHub Actions expressions into a shell command string. The line `echo "${{ github.server_url }}/${{ github.repository }}/security/code-scanning?..."` embeds ${{ github.server_url }} and ${{ github.repository }} directly inside a run: shell command. These values are substituted by the template engine before the shell ever sees them, enabling script injection if any value contains shell metacharacters. The safe pattern is to route these through env: vars and reference them as $GITHUB_SERVER_URL / $GITHUB_REPOSITORY instead.

Locations:

- `.github/workflows/osv-scanner-reusable.yml:92`

### unpinned-uses (severity: high)

One or more uses: references and/or docker image references are not pinned to a full 40-character SHA commit hash or SHA digest, making them vulnerable to supply-chain attacks via tag mutation. Failing references: (1) `uses: actions/download-artifact@v7` — uses a mutable version tag instead of a SHA. (2) `image: "docker://ghcr.io/google/osv-scanner-action:v2.3.5"` in osv-reporter-action/action.yml — uses a mutable image tag instead of a SHA digest (e.g. @sha256:<digest>). (3) `image: "docker://ghcr.io/google/osv-scanner-action:v2.3.5"` in osv-scanner-action/action.yml — uses a mutable image tag instead of a SHA digest.

Locations:

- `.github/workflows/osv-scanner-reusable.yml:65`
- `osv-reporter-action/action.yml:24`
- `osv-scanner-action/action.yml:24`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, unpinned-uses

**Notes:**

Fixed 5 issues across 4 files: (1) Pinned actions/download-artifact@v7 to SHA 37930b1c2abaa49bbe596cd826c3c89aef350131 in osv-scanner-reusable.yml. (2) Pinned docker://ghcr.io/google/osv-scanner-action:v2.3.5 to sha256:512bc221cb77a33325bc92cf45c0c8a45f2689be8593dc4e541058590f4ce09f in both osv-reporter-action/action.yml and osv-scanner-action/action.yml (preserving docker:// scheme and tag). (3) Fixed script injection in osv-scanner-reusable.yml 'Print Code Scanning URL' step by moving github.server_url and github.repository into env vars SERVER_URL and REPOSITORY. (4) Fixed script injection in osv-scanner-reusable-pr.yml 'Print Code Scanning PR URL' step by moving github.server_url, github.repository, and github.event.pull_request.number into env vars SERVER_URL, REPOSITORY, and PR_NUMBER.

