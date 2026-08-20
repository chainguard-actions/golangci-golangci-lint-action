<!-- markdownlint-disable -->

# Hardening Report: golangci--golangci-lint-action/v9.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **golangci--golangci-lint-action/v9.2.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in both workflow files use mutable version tags instead of full 40-character SHA commit hashes, making them vulnerable to supply-chain attacks. In test.yml: `actions/setup-node@v6`, `actions/checkout@v6`, `actions/setup-go@v6` (repeated across multiple jobs). In codeql.yaml: `actions/checkout@v6`, `github/codeql-action/init@v4`, `github/codeql-action/analyze@v4`. None of the 20 `uses:` references are pinned to a full commit SHA.

Locations:

- `.github/workflows/test.yml:19`
- `.github/workflows/test.yml:21`
- `.github/workflows/codeql.yaml:22`
- `.github/workflows/codeql.yaml:31`
- `.github/workflows/codeql.yaml:38`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 20 `uses:` references in both workflow files to full 40-character commit SHAs:
- `actions/checkout@v6` → `actions/checkout@d23441a48e516b6c34aea4fa41551a30e30af803 # v6` (used 7 times across both files)
- `actions/setup-node@v6` → `actions/setup-node@249970729cb0ef3589644e2896645e5dc5ba9c38 # v6` (used 7 times in test.yml)
- `actions/setup-go@v6` → `actions/setup-go@924ae3a1cded613372ab5595356fb5720e22ba16 # v6` (used 5 times in test.yml)
- `github/codeql-action/init@v4` → `github/codeql-action/init@ff2f1c621b7f889edc0d3c761ac2e6a3f8cdb0dd # v4` (1 time in codeql.yaml)
- `github/codeql-action/analyze@v4` → `github/codeql-action/analyze@ff2f1c621b7f889edc0d3c761ac2e6a3f8cdb0dd # v4` (1 time in codeql.yaml)
All SHAs were resolved via lookup_action_sha. Version tags are preserved as inline comments for readability.

