# Gitleaks Secrets Scanning for SolrLens

This document explains how **Gitleaks** was used to scan the **SolrLens full-stack TypeScript application** for **hardcoded secrets** such as API keys, tokens, passwords, and credentials.

The focus is on **practical execution only**:
- Gitleaks setup using Docker
- Scanning the source code
- Viewing scan results

---

### 1. Tooling Used

- Gitleaks (Docker)
- Git repository (SolrLens)
- Docker

---

### 2. Gitleaks Setup Using Docker

Gitleaks does **not require a server or UI**.  
It runs as a **CLI-based scanner**.

Pull Gitleaks Image

```bash
docker pull zricethezav/gitleaks:latest
```
### 3. Run Gitleaks Scan on SolrLens
Navigate to the root of the SolrLens repository.

Scan Working Directory
```bash
docker run --rm \
  -v "$(pwd):/repo" \
  zricethezav/gitleaks:latest detect \
  --source="/repo" \
  --report-format=json \
  --report-path="/repo/gitleaks-report.json"
```
This scans:

All tracked files

All source code

Configuration files

### 4. Scan Git History (Optional but Recommended)

To scan entire Git history:

```bash
docker run --rm \
  -v "$(pwd):/repo" \
  zricethezav/gitleaks:latest detect \
  --source="/repo" \
  --log-opts="--all" \
  --report-format=json \
  --report-path="/repo/gitleaks-history-report.json"
```
### 5. View Results
After execution, reports are generated in the project root:

```text

gitleaks-report.json
gitleaks-history-report.json
Result Types
Detected secrets (if any)
```
File path

Line number

Rule ID

Severity

If no secrets are found, Gitleaks exits successfully.

### 6. Handling Findings
If secrets are detected:

Remove secrets from code

Rotate exposed credentials

Add sensitive files to .gitignore

Use environment variables or secret managers

### 7. Best Practices Followed
Secrets scanning performed locally using Docker

No secrets committed to Git

JSON report generated for auditability

Tool aligned with DevSecOps practices

