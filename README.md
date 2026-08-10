# domops-ci-cd-tests

Repo to store my reusable CI/CD tests for my projects.

## CI/CD Test Workflows

A collection of reusable GitHub Actions workflow files for automated testing. Copy the relevant files into any project's `.github/workflows/` folder and adjust the project-specific values.

---

### unit-tests.yml
Runs Python unit tests using **pytest** and **moto**. Tests application logic in isolation — no real AWS services are called. moto intercepts boto3 calls and fakes them locally.

### security-tests.yml
Three security scans running in parallel:
- **Gitleaks** — scans the full git history for accidentally committed secrets or credentials
- **Trivy** — scans code, dependencies, and IaC for known CVEs and misconfigurations
- **Semgrep** — static analysis that flags security anti-patterns across your code

### integration-tests.yml
Runs end-to-end tests using **LocalStack** (local AWS mock) and a **PostgreSQL** service container. Tests the full application flow without spinning up real AWS resources or incurring cloud costs.

### quality.yml
Runs **SonarCloud** analysis after tests complete. Tracks code coverage, bugs, and code smells over time. Acts as a quality gate on pull requests to main.
