<!-- markdownlint-disable -->

# Hardening Report: golangci--golangci-lint-action/v6.5.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **golangci--golangci-lint-action/v6.5.2** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references in workflow files are pinned to mutable tags rather than full 40-character SHA commit hashes, making them vulnerable to supply-chain attacks. Failing references in .github/workflows/test.yml: `actions/checkout@v4`, `actions/setup-go@v5`. Failing references in .github/workflows/codeql.yaml: `actions/checkout@v4`, `github/codeql-action/init@v3`, `github/codeql-action/analyze@v3`.

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:17`
- `.github/workflows/test.yml:57`
- `.github/workflows/test.yml:58`
- `.github/workflows/test.yml:80`
- `.github/workflows/test.yml:81`
- `.github/workflows/test.yml:103`
- `.github/workflows/test.yml:104`
- `.github/workflows/codeql.yaml:20`
- `.github/workflows/codeql.yaml:33`
- `.github/workflows/codeql.yaml:39`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the `build` job has no job-level `permissions:` key. Without explicit permissions, the job inherits the default (potentially write) token permissions. Only the `test`, `test-go-install`, and `test-go-mod` jobs define job-level permissions; the `build` job does not.

Locations:

- `.github/workflows/test.yml:1`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and its only job (`codeQL`) has no job-level `permissions:` key. Without explicit permissions, the job inherits the default (potentially write) token permissions.

Locations:

- `.github/workflows/codeql.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings across both workflow files:

1. **unpinned-uses** (.github/workflows/test.yml and .github/workflows/codeql.yaml): Pinned all `uses:` references to full 40-character SHA hashes with tag comments preserved:
   - `actions/checkout@v4` → SHA `11d5960a326750d5838078e36cf38b85af677262`
   - `actions/setup-go@v5` → SHA `40f1582b2485089dde7abd97c1529aa768e1baff`
   - `github/codeql-action/init@v3` → SHA `4187e74d05793876e9989daffde9c3e66b4acd07`
   - `github/codeql-action/analyze@v3` → SHA `4187e74d05793876e9989daffde9c3e66b4acd07`

2. **missing-permissions** (test.yml): Added `permissions: {}` at the workflow top level and `permissions: contents: read` to the `build` job.

3. **missing-permissions** (codeql.yaml): Added `permissions: {}` at the workflow top level and job-level permissions (`actions: read`, `contents: read`, `security-events: write`) to the `codeQL` job — the minimum required for CodeQL scanning.

