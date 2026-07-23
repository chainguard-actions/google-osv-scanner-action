<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.3.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action/v2.3.2** was hardened automatically. 5 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): Direct expression interpolation in a run: block. The 'Print Code Scanning PR URL' step echoes ${{ github.server_url }}, ${{ github.repository }}, and ${{ github.event.pull_request.number }} directly inside a shell run: command. These GitHub Actions expressions are substituted by the template engine before the shell sees them, allowing an attacker-controlled value (e.g. a crafted repository name or PR number) to inject shell metacharacters. Offending line: echo "${{ github.server_url }}/${{ github.repository }}/security/code-scanning?query=pr%3A${{ github.event.pull_request.number }}"

Locations:

- `.github/workflows/osv-scanner-reusable-pr.yml:122`

### script-injection (severity: high)

Sub-rule (a): Direct expression interpolation in a run: block. The 'Print Code Scanning URL' step echoes ${{ github.server_url }}, ${{ github.repository }}, and ${{ github.ref_name }} directly inside a shell run: command. These GitHub Actions expressions are substituted by the template engine before the shell sees them, allowing an attacker-controlled value (e.g. a crafted branch name or repository name) to inject shell metacharacters. Offending line: echo "${{ github.server_url }}/${{ github.repository }}/security/code-scanning?query=is%3Aopen+branch%3A${{ github.ref_name }}+tool%3Aosv-scanner"

Locations:

- `.github/workflows/osv-scanner-reusable.yml:108`

### unpinned-uses (severity: high)

The following uses: reference is pinned to a mutable version tag rather than a full 40-character commit SHA, making it vulnerable to supply-chain attacks if the tag is moved: 'actions/download-artifact@v7'.

Locations:

- `.github/workflows/osv-scanner-reusable.yml:68`

### unpinned-uses (severity: high)

The runs.image: field references a Docker image using a mutable version tag instead of an immutable SHA digest, making it vulnerable to supply-chain attacks if the tag is overwritten. Failing reference: image: "docker://ghcr.io/google/osv-scanner-action:v2.3.2". It should use a SHA digest, e.g. ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest>.

Locations:

- `osv-reporter-action/action.yml:25`

### unpinned-uses (severity: high)

The runs.image: field references a Docker image using a mutable version tag instead of an immutable SHA digest, making it vulnerable to supply-chain attacks if the tag is overwritten. Failing reference: image: "docker://ghcr.io/google/osv-scanner-action:v2.3.2". It should use a SHA digest, e.g. ghcr.io/google/osv-scanner-action@sha256:<64-hex-char-digest>.

Locations:

- `osv-scanner-action/action.yml:28`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, unpinned-uses

**Notes:**

Fixed 5 findings across 4 files:
1. osv-scanner-reusable-pr.yml (line 122): Moved ${{ github.server_url }}, ${{ github.repository }}, and ${{ github.event.pull_request.number }} out of the run: block into an env: block (SERVER_URL, REPOSITORY, PR_NUMBER), referencing them as plain shell variables.
2. osv-scanner-reusable.yml (line 108): Moved ${{ github.server_url }}, ${{ github.repository }}, and ${{ github.ref_name }} out of the run: block into an env: block (SERVER_URL, REPOSITORY, REF_NAME), referencing them as plain shell variables.
3. osv-scanner-reusable.yml (line 68): Pinned actions/download-artifact@v7 to full SHA actions/download-artifact@37930b1c2abaa49bbe596cd826c3c89aef350131 # v7.
4. osv-reporter-action/action.yml (line 25): Pinned docker://ghcr.io/google/osv-scanner-action:v2.3.2 to docker://ghcr.io/google/osv-scanner-action:v2.3.2@sha256:ade1325102b76c3e4e46e6fac7990048f1c1f8ea105e0798340e2b003cd7c328.
5. osv-scanner-action/action.yml (line 28): Pinned docker://ghcr.io/google/osv-scanner-action:v2.3.2 to docker://ghcr.io/google/osv-scanner-action:v2.3.2@sha256:ade1325102b76c3e4e46e6fac7990048f1c1f8ea105e0798340e2b003cd7c328.

