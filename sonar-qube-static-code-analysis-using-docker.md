# SonarQube Static Code Analysis for SolrLens (Practical Guide)

### This document describes how **SonarQube static code analysis** was performed on the **SolrLens full-stack TypeScript (MERN-style) application** using **Docker**.

The focus is on **practical execution only**:
- SonarQube setup
- Authentication
- Running the scan
- Viewing results on the SonarQube UI

---

### 1. Tech Stack Overview (Analyzed Project)

#### Frontend
- React 18 + TypeScript
- Vite (SWC)
- Tailwind CSS + shadcn/ui
- TanStack Query
- React Hook Form + Zod
- Recharts
- React Router DOM

#### Backend
- Node.js 22
- Express.js
- TypeScript
- Axios
- dotenv

#### Infrastructure
- Docker (multi-stage builds)
- Docker Compose
- GitHub Container Registry (GHCR)
- SonarQube (Dockerized)

---

### 2. SonarQube Setup (Docker)

#### Create Docker Compose File: `docker-compose-sonar.yml`

From the `docker` directory or `root` directory:
```yaml
version: "3.8"

services:
  sonarqube:
    image: sonarqube:community
    container_name: sonarqube
    ports:
      - "9000:9000"
    environment:
      - SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true
    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_extensions:/opt/sonarqube/extensions
      - sonarqube_logs:/opt/sonarqube/logs
    restart: unless-stopped

volumes:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_logs:
```

Start SonarQube

```bash

docker compose -f docker-compose-sonar.yml up -d

```

Verify the container is running:

```bash

docker ps

```
SonarQube will be available at:
```bash
http://localhost:9000
```
Default Login
```pgsql

Username: admin
Password: admin
```
### 3. SonarQube Authentication (Token-Based)
SonarQube does not support username/password authentication for scanners.
A user token is required.

- Generate Token

- Login to SonarQube UI

- Go to My Account → Security

- Generate a new token (example name: local-scan)

- Copy the token to text editor you need use it to run (shown only once)

### 4. Sonar Project Configuration

Create a sonar-project.properties file in the project root:

properties
```bash
sonar.projectKey=solarlens
sonar.projectName=SolrLens
sonar.projectVersion=1.0

sonar.sources=.
sonar.exclusions=node_modules/**,dist/**,build/**

sonar.sourceEncoding=UTF-8
```
⚠️ Security Note
Do NOT store sonar.token in this file.
Tokens are injected via environment variables.

### 5. Running SonarQube Scan

Replace the Token with $SONAR_TOKEN

```bash
sonar-scanner \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=$SONAR_TOKEN
```
If the scan starts successfully, you will see logs like:

```pgsql

INFO: Analyzing on SonarQube server
INFO: Analysis successful
INFO: EXECUTION SUCCESS
```

### 6. Viewing Results
Open the SonarQube dashboard:
```
http://localhost:9000
```
Navigate to:

nginx

- Projects → SolrLens
  
- Available Analysis Results

<img width="1286" height="489" alt="Screenshot from 2026-01-17 19-02-15" src="https://github.com/user-attachments/assets/98b312fa-e3f3-45f9-992e-baa2141cd85a" />


- Code Smells

- Bugs

- Security Hotspots

- Maintainability Rating

- Reliability Rating

- Security Rating

- Technical Debt


