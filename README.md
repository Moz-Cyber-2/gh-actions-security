# Security GitHub Actions

Reusable GitHub Actions workflows for DevSecOps pipelines.

## Available Reusable Workflows

| Workflow | Tool | Trigger |
|---|---|---|
| `secrets-scan-pr.yaml` | TruffleHog | `workflow_call` |
| `secrets-clean-history.yaml` | git-filter-repo + TruffleHog | `workflow_call` |
| `reusable-container-scan.yml` | Trivy | `workflow_call` |
| `reusable-sast.yml` | Semgrep | `workflow_call` |

## Usage

### Secrets Scan (TruffleHog)
```yaml
jobs:
  secrets:
    uses: DEMO_ORG/security-gh-actions/.github/workflows/secrets-scan-pr.yaml@main
    permissions:
      contents: read
      pull-requests: write
```

### SAST (Semgrep)
```yaml
jobs:
  sast:
    uses: DEMO_ORG/security-gh-actions/.github/workflows/reusable-sast.yml@main
    permissions:
      contents: read
      security-events: write
    with:
      config: "p/owasp-top-ten p/nodejs p/secrets"
      fail_on_findings: true
```

### Container Image Scan (Trivy)
```yaml
jobs:
  container-scan:
    uses: DEMO_ORG/security-gh-actions/.github/workflows/reusable-container-scan.yml@main
    permissions:
      contents: read
      security-events: write
    with:
      image_tarball_artifact: docker-image
      image_name: my-app
      severity: "HIGH,CRITICAL"
      fail_on_findings: true
```
