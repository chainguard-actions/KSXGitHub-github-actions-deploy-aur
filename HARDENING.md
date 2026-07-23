<!-- markdownlint-disable -->

# Hardening Report: KSXGitHub--github-actions-deploy-aur/v4.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **KSXGitHub--github-actions-deploy-aur/v4.2.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/checkout@v4`, which is a mutable tag reference rather than a pinned full-length SHA commit hash. If the tag is moved (e.g. by a supply-chain compromise of the upstream action), the workflow will silently execute different code. Replace with the full 40-character commit SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/lint.yml:18`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced `actions/checkout@v4` with `actions/checkout@11d5960a326750d5838078e36cf38b85af677262 # v4` in `.github/workflows/lint.yml` to pin the action to an immutable commit SHA, preventing supply-chain attacks via mutable tag references.

