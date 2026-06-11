<!-- markdownlint-disable -->

# Hardening Report: KSXGitHub--github-actions-deploy-aur/v4.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **KSXGitHub--github-actions-deploy-aur/v4.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### suspicious-run-content (severity: high)

Sub-check: eval-dynamic. In build.sh, the variable `post_process` is assigned directly from the user-controlled environment variable `$INPUT_POST_PROCESS` (which maps to the `post_process` action input), and then executed via `eval "$post_process"`. This allows any caller of the action to supply arbitrary shell commands that will be executed in the runner environment with full privileges. An attacker controlling the `post_process` input can run any command, exfiltrate secrets, or compromise the runner.

Locations:

- `build.sh:87`

## Iteration Notes

### Iteration 1

**Fixes applied:** suspicious-run-content

**Notes:**

Replaced `eval "$post_process"` in build.sh (line 87) with a safer pattern: the post_process commands are written to a temporary script file (mktemp with restricted 700 permissions), executed via `bash -- "$_post_process_script"`, and then removed. This eliminates the eval-dynamic risk while preserving the post_process functionality. The `bash --` form ensures the script path is not misinterpreted as a flag even if mktemp produces an unusual path.

