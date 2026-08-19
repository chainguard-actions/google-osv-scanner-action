<!-- markdownlint-disable -->

# Hardening Report: google--osv-scanner-action/v2.3.8

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google--osv-scanner-action/v2.3.8** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Multiple `run:` blocks in osv-scanner-reusable-pr.yml directly interpolate GitHub Actions expressions inside shell commands, violating rule (a). In the 'Export results' step, `${{ inputs.matrix-property }}` is interpolated directly into `if [ -f ${{ inputs.matrix-property }}old-results.json ]` and `cat ${{ inputs.matrix-property }}old-results.json`, allowing a caller to inject arbitrary shell metacharacters. In the 'Print Code Scanning PR URL' step, `${{ github.server_url }}`, `${{ github.repository }}`, and `${{ github.event.pull_request.number }}` are interpolated directly into an `echo` command.

Locations:

- `.github/workflows/osv-scanner-reusable-pr.yml:97`
- `.github/workflows/osv-scanner-reusable-pr.yml:99`
- `.github/workflows/osv-scanner-reusable-pr.yml:103`
- `.github/workflows/osv-scanner-reusable-pr.yml:105`
- `.github/workflows/osv-scanner-reusable-pr.yml:131`

### script-injection (severity: high)

Multiple `run:` blocks in osv-scanner-reusable.yml directly interpolate GitHub Actions expressions inside shell commands, violating rule (a). In the 'Export results' step, `${{ inputs.matrix-property }}` is interpolated directly into `if [ -f ${{ inputs.matrix-property }}osv-results.json ]` and `cat ${{ inputs.matrix-property }}osv-results.json`. In the 'Print Code Scanning URL' step, `${{ github.server_url }}` and `${{ github.repository }}` are interpolated directly into an `echo` command.

Locations:

- `.github/workflows/osv-scanner-reusable.yml:82`
- `.github/workflows/osv-scanner-reusable.yml:84`
- `.github/workflows/osv-scanner-reusable.yml:109`

### github-env-injection (severity: high)

The 'Export results' steps write file contents to $GITHUB_OUTPUT using `cat ${{ inputs.matrix-property }}*-results.json >> "${GITHUB_OUTPUT}"`. The file path is constructed by directly interpolating `inputs.matrix-property` (a workflow_call input, attacker-controllable) without sanitization. A caller can supply a value containing newlines or special characters to inject arbitrary key=value pairs into GITHUB_OUTPUT, potentially overwriting outputs used by downstream steps.

Locations:

- `.github/workflows/osv-scanner-reusable-pr.yml:99`
- `.github/workflows/osv-scanner-reusable-pr.yml:103`
- `.github/workflows/osv-scanner-reusable.yml:84`

### unpinned-uses (severity: high)

The following `uses:` reference is pinned to a mutable version tag rather than a full 40-character commit SHA, making it vulnerable to supply-chain attacks if the tag is moved: `uses: actions/download-artifact@v8`. All other `uses:` references in the workflow files are correctly pinned to full SHAs. Additionally, both `osv-scanner-action/action.yml` and `osv-reporter-action/action.yml` use a mutable Docker image tag (`docker://ghcr.io/google/osv-scanner-action:v2.3.8`) instead of a SHA digest (e.g. `@sha256:<digest>`), which is equally vulnerable to supply-chain attacks.

Locations:

- `.github/workflows/osv-scanner-reusable.yml:60`
- `osv-scanner-action/action.yml:22`
- `osv-reporter-action/action.yml:20`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, github-env-injection, unpinned-uses

**Notes:**

Fixed all four findings: (1) script-injection in osv-scanner-reusable-pr.yml: moved inputs.matrix-property to MATRIX_PROPERTY env var in 'Export results' step; moved github.server_url, github.repository, github.event.pull_request.number to SERVER_URL, REPOSITORY, PR_NUMBER env vars in 'Print Code Scanning PR URL' step. (2) script-injection in osv-scanner-reusable.yml: moved inputs.matrix-property to MATRIX_PROPERTY env var in 'Export results' step; moved github.server_url and github.repository to SERVER_URL and REPOSITORY env vars in 'Print Code Scanning URL' step. (3) github-env-injection: addressed by the same MATRIX_PROPERTY env var fix — file path is now constructed from an env var rather than a directly interpolated expression. (4) unpinned-uses: pinned actions/download-artifact@v8 to SHA 3e5f45b2cfb9172054b4087a40e8e0b5a5461e7c; pinned Docker image in both osv-scanner-action/action.yml and osv-reporter-action/action.yml to docker://ghcr.io/google/osv-scanner-action:v2.3.8@sha256:48406c58197201fe55e56615ad9d414f85063da320e204d0b0ed460fb3908dba.

