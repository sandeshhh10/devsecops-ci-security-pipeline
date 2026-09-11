# DevSecOps CI/CD Security Pipeline

A security-focused CI/CD pipeline built with **GitHub Actions** that automates application testing, static code analysis, dependency vulnerability scanning, Docker image security scanning, and security gates.

The pipeline integrates security checks directly into the software delivery process, helping detect vulnerabilities before insecure code or container images are deployed.

---

## Architecture

```text
Developer
   |
   | git push / pull request
   ↓
GitHub Repository
   |
   ↓
GitHub Actions
   |
   ├── Python Setup
   ├── Dependency Install
   ├── Unit Tests
   ├── pip-audit
   ├── Semgrep SAST
   ├── Docker Build
   └── Trivy Container Scan
           |
           ↓
      Security Gate
        /        \
     PASS        FAIL
```

### Pipeline Flow

1. A developer pushes code or creates a pull request.
2. GitHub Actions automatically triggers the CI/CD pipeline.
3. The required Python environment and dependencies are configured.
4. Unit tests are executed using **Pytest**.
5. **pip-audit** scans project dependencies for known vulnerabilities.
6. **Semgrep** performs Static Application Security Testing (SAST).
7. A Docker image is built from the application.
8. **Trivy** scans the Docker image for known vulnerabilities.
9. Security checks return exit codes that determine whether the pipeline passes or fails the security gate.

---

## Technologies

```text
Python
Flask
Git
GitHub
GitHub Actions
Docker
Semgrep
pip-audit
Trivy
Pytest
```

---

## Security Checks

| Check | Purpose |
|---|---|
| **Pytest** | Application and unit testing |
| **pip-audit** | Dependency vulnerability detection |
| **Semgrep** | Static code security analysis (SAST) |
| **Trivy** | Docker container vulnerability scanning |
| **Exit Codes** | Enforces automated security gates |

---

## Security Pipeline

The project follows a **shift-left security** approach by integrating security validation directly into CI/CD.

```text
          Code Commit
               |
               ↓
        GitHub Actions
               |
      ┌────────┴────────┐
      ↓                 ↓
 Application        Security
   Testing           Analysis
      |                 |
   Pytest          ┌────┴───────────────┐
                   ↓        ↓          ↓
               pip-audit  Semgrep    Trivy
                   |        |          |
                   └────────┴──────────┘
                            |
                            ↓
                     Security Gate
                       /       \
                    PASS       FAIL
                     |           |
                     ↓           ↓
                 Continue    Stop Pipeline
```

---

## Project Structure

```text
devsecops-ci-security-pipeline/
│
├── .github/
│   └── workflows/
│       └── ci-security.yml
│
├── app/
│   └── ...
│
├── tests/
│   └── ...
│
├── Dockerfile
├── requirements.txt
├── README.md
└── ...
```

---

## How to Run Locally

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd devsecops-ci-security-pipeline
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it on Windows:

```powershell
venv\Scripts\activate
```

On Linux/macOS:

```bash
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run tests

```bash
pytest
```

### 5. Run dependency security scanning

```bash
pip-audit -r requirements.txt
```

### 6. Run Semgrep

```bash
semgrep --config=auto .
```

### 7. Build the Docker image

```bash
docker build -t devsecops-app .
```

### 8. Scan the Docker image with Trivy

```bash
trivy image devsecops-app
```

---

## CI/CD Security Gates

The pipeline uses tool exit codes to automatically determine whether a security check passes or fails.

```text
Security Check
      |
      ↓
Exit Code = 0
      |
      ↓
   PASS
      |
      ↓
Continue Pipeline
```

```text
Security Check
      |
      ↓
Non-Zero Exit Code
      |
      ↓
   FAIL
      |
      ↓
Stop Pipeline
```

This ensures that detected security issues can prevent an unsafe build from progressing through the pipeline.

---

## Skills Demonstrated

```text
CI/CD
DevSecOps
Git/GitHub
GitHub Actions
Python
Linux
Docker
SAST
Dependency Scanning
Container Security
Vulnerability Management
Security Automation
```

---

## Key DevSecOps Concepts

This project demonstrates practical implementation of:

- **Continuous Integration and Continuous Delivery**
- **Shift-Left Security**
- **Static Application Security Testing (SAST)**
- **Software Dependency Scanning**
- **Container Security**
- **Automated Security Gates**
- **Security Automation**
- **Vulnerability Management**
- **Security Integration within CI/CD**

---

## Objective

The primary objective of this project is to demonstrate how security can be integrated into a modern CI/CD pipeline rather than being treated as a separate stage after development.

By automating testing and vulnerability detection with GitHub Actions, the pipeline provides continuous security validation throughout the software development lifecycle.

---

## Author

Sandesh GC
