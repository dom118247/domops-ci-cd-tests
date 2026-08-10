## CI/CD Test Workflows

A set of GitHub Actions workflow files I've put together to reuse across my projects. 
Rather than rewriting the same testing setup every time, I store them here and drop 
them into whatever I'm building.

---

### unit-tests.yml
Runs my Python unit tests using pytest and moto. Moto fakes out the AWS services 
so I can test my Lambda logic without touching real infrastructure or racking up a bill.

### security-tests.yml
Three security scans I run on every push:
- **Gitleaks** — catches any secrets or credentials I may have accidentally committed
- **Trivy** — checks my dependencies and IaC for known vulnerabilities
- **Semgrep** — scans my code for security anti-patterns

### integration-tests.yml
Tests the full application flow using LocalStack as a local AWS mock and a PostgreSQL 
container for the database. Lets me test end-to-end without deploying anything real.

### quality.yml
Runs SonarCloud after tests complete to track code coverage, bugs, and code quality 
over time. Mainly here to make sure I'm not letting standards slip as projects grow.
