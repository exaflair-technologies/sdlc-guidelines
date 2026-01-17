# Coding Practices

We write code to be read by others.

## Golden Rules

- **Readable > Clever**: If it requires a paragraph to explain, rewrite the code.
- **Small & Focused**: Functions should do one thing well.
- **Explicit Error Handling**: Don't fail silently.
- **No Dead Code**: If it's not used, delete it. Don't comment it out.

## Cloud Native Principles

We follow the [12-Factor App](https://12factor.net) methodology:
- **Config**: Store in environment variables, never code.
- **Stateless**: Services should scale horizontally without state issues.
- **Logs**: Treat logs as event streams.

## Quality & Security Gates

- **Linting**: Husky pre-commit hooks are mandatory. Use the repo's config.
- **Dependency Checks**: Dependabot watches for updates.
- **Container Scan**: Trivy scans our Docker images for vulnerabilities.

## Testing

- **New Features**: Must have unit tests.
- **Bug Fixes**: Should have a regression test to prevent recurrence.
- **CI**: Never skip failing tests. Fix the code or fix the test.
