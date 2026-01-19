---
layout: default
title: 4. Deployment
parent: Delivery Workflow
nav_order: 4
---

# Step 4: Deployment & Release

Features are only valuable when they reach the user.

## The Pipeline

We use **GitHub Actions** with self-hosted runners on our Hostinger VPS.

| Event | Actions |
|-------|---------|
| **Push to PR** | Lint, Test, Security Scan (Trivy) |
| **Merge to Main** | Build, Deploy to Production, Cleanup |

## Environments

- **Production**: Live application, updated from `main`.
- **Staging**: (Planned) Mirror of production for final verification.

## Release Process

We follow [Semantic Versioning](https://semver.org/) (`MAJOR.MINOR.PATCH`).

1. **Trigger**: Code is merged to `main` and deployed.
2. **Tagging**: Create a GitHub release tag (e.g., `v1.2.0`) with release notes.
3. **Closure**: Mark related Zoho tickets as **Done**.

## Hotfixes

Critical production bug?
1. Branch from `main`: `fix/high-priority-bug`.
2. Fix, PR, and get **one approval**.
3. Merge to trigger immediate deployment.
4. Increment the `PATCH` version.

## Rollback

If a deployment fails:
1. Revert the merge commit.
2. The pipeline will automatically redeploy the previous stable state.
3. Post an incident note in the relevant Zoho ticket.
