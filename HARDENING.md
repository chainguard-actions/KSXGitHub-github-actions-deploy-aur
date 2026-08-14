<!-- markdownlint-disable -->

# Hardening Report: KSXGitHub--github-actions-deploy-aur/v4.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **KSXGitHub--github-actions-deploy-aur/v4.1.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### suspicious-run-content (severity: high)

eval-dynamic: build.sh evaluates a user-controlled input as shell code via `eval "$post_process"`. The variable `post_process` is assigned directly from `$INPUT_POST_PROCESS`, which is the `post_process` action input supplied by the calling workflow. This allows any caller to execute arbitrary shell commands inside the Docker container by setting `post_process` to a malicious command string.

Locations:

- `build.sh:88`

## Iteration Notes

### Iteration 1

**Fixes applied:** suspicious-run-content

**Notes:**

Replaced `eval "$post_process"` in build.sh (line 88) with a safer approach: write the post_process commands to a temporary script file using `printf '%s\n'`, then execute it with `bash`. This eliminates the use of `eval` on user-controlled input while preserving the intended post-processing functionality. The temporary script file is cleaned up after execution.

