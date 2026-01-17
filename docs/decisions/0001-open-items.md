# Open Roadmap Items

- **Status**: Active
- **Date**: 2026-01-08

## Pending Decisions [TBD]

- [ ] **Assign CI Pipeline Ownership**: We need to define who exactly owns the maintenance of our CI pipelines.

## Next Steps

Once the above is finalized, we need to execute:
- [ ] **Self-Hosted Runner**: Setup the GitHub Actions runner on the Hostinger VPS.
- **Why**: To deploy code securely to our environment.
- [ ] **Automations**: Configure `GitHub -> Zoho` and `Zoho -> Slack` integrations.
- **Why**: To reduce manual status reporting.
- [ ] **Branch Protection**: Enable GitHub protected branches.
- **Blocker**: currently requires a GitHub Team/Pro plan update or is limited in Free plan (using Social Block Rule for now).
