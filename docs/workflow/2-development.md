# Step 2: Development

Time to build. We prioritize a consistent local environment that mirrors production.

## 1. Local Environment

We use **Docker** and **Docker Compose** for local development. This ensures that what works on your machine works on the VPS. 

> **Important**: Before pushing code, always run:
> - `lint`
> - `unit tests`
> - `docker build`

## 2. Branching Strategy

We use a **Feature Branch Workflow**. Always branch from `main`.

**Naming Convention:**
- `feat/TICKET-ID-short-description` (New features)
- `fix/TICKET-ID-short-description` (Bug fixes)
- `chore/TICKET-ID-short-description` (Maintenance)
- `refactor/...`, `docs/...`, `test/...`

*Example*: `feat/EX-102-wallet-connect`

## 3. Saving Your Work (Commits)

We follow the **Conventional Commits** specification. This allows us to automate changelogs and versioning.

**Format**:
```text
type(scope): short description

Optional body explaining the "why".

Refs: ZOHO-TICKET-ID
```

**Example**:
```text
feat(auth): add wallet connect API

Refs: EX-102
```

**Valid Types**: `feat`, `fix`, `chore`, `refactor`, `docs`, `test`.
