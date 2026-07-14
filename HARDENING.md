<!-- markdownlint-disable -->

# Hardening Report: KSXGitHub--github-actions-deploy-aur/v4.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **KSXGitHub--github-actions-deploy-aur/v4.2.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses actions/checkout@v4, which is pinned to a mutable tag rather than a full 40-character commit SHA. This means the action could be silently updated or replaced by a supply-chain attacker without changing the workflow file. It should be pinned to a specific commit SHA (e.g., actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4).

Locations:

- `.github/workflows/lint.yml:19`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned actions/checkout@v4 to its full commit SHA (34e114876b0b11c390a56381ad16ebd13914f8d5) in .github/workflows/lint.yml, preserving the tag as a comment. No other findings were present.

