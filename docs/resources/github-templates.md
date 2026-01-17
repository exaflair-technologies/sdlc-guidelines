# GitHub Configuration Templates

Reference these templates when setting up new repositories.

## 1. Social Enforcer Workflow

Use this to remind people about the review rules.

**File**: `.github/workflows/compliance.yml`

```yaml
name: Exaflair Compliance
on: pull_request

jobs:
  policy-check:
    runs-on: ubuntu-latest
    steps:
      - name: Check Reviews
        uses: actions/github-script@v6
        with:
          script: |
            const reviews = await github.rest.pulls.listReviews({
              owner: context.repo.owner,
              repo: context.repo.repo,
              pull_number: context.issue.number,
            });
            const approved = reviews.data.some(r => r.state === 'APPROVED');
            if (!approved) core.setFailed('BLOCKED: Independent review required');
```

## 2. Unified Deploy Workflow

Use this for production deployment.

**File**: `.github/workflows/deploy.yml`

```yaml
name: Production Deploy
on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: [self-hosted, production]

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Security Scan
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: fs
          severity: CRITICAL
          exit-code: 0

      - name: Build and Deploy
        run: |
          echo "Deploying to Exaflair Production"
          docker compose build --pull
          docker compose up -d
          docker system prune -f
```
