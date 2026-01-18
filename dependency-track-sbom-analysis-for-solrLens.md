# Dependency-Track SBOM Analysis for SolrLens

This document explains how **Dependency-Track** was used to generate and analyze an **SBOM (Software Bill of Materials)** for the **SolrLens full-stack TypeScript application**.

The focus is on **practical execution only**:
- Dependency-Track setup using Docker
- Project creation
- SBOM generation
- SBOM upload
- Viewing vulnerability results

---

#### 1. Tooling Used

- Dependency-Track (Dockerized)
- CycloneDX SBOM format
- Node.js (Frontend + Backend)
- npm
- Docker & Docker Compose

---

### 2. Dependency-Track Setup Using Docker Compose

#### Docker Compose File: `docker-compose-dependency-track.yml`

```yaml
version: "3.8"

services:
  dependency-track:
    image: dependencytrack/apiserver:latest
    container_name: dependency-track
    ports:
      - "8081:8080"
    volumes:
      - dtrack-data:/data
    restart: unless-stopped

volumes:
  dtrack-data:
```
Start Dependency-Track
```bash

docker compose -f docker-compose-dependency-track.yml up -d
```
Verify container:

```bash
docker ps
```
Access UI:

- http://localhost:8081

Default Login

```pgsql
Username: admin
Password: admin
```
(Change password on first login)

### 3. Create Project in Dependency-Track

- Login to Dependency-Track UI

- Navigate to Projects → Create Project

Enter:

Name: SolrLens

Version: 1.0

Save the project

### 4. Generate SBOM for SolrLens (CycloneDX)
#### Dependency-Track requires an SBOM, not raw source code.

Install CycloneDX Tool (Local)
```bash
npm install --save-dev @cyclonedx/cyclonedx-npm
```
Generate SBOM (Root of Project)
```bash
npx cyclonedx-npm \
  --output-format json \
  --output-file bom.json
```
This generates:

```pgsql
bom.json
```
⚠️ Do NOT commit bom.json if it contains internal dependency data.

### 5. Upload SBOM to Dependency-Track
Upload via UI (Simple & Practical)

- Open Projects → SolrLens

- Click Upload BOM

- Select bom.json

- Upload

Dependency-Track will start processing immediately.

### 6. View Analysis Results

Navigate to:

- nginx

- Projects → SolrLens

You can now view:

- Vulnerable dependencies

- Severity (Critical / High / Medium / Low)

- Affected packages

- CVE references

- License risks

### 7. What Dependency-Track Analyzes

- npm dependencies (frontend + backend)

- Transitive dependencies

- Known CVEs

- License compliance risks

- Dependency freshness

