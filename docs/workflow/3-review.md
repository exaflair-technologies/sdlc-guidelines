# Step 3: Code Review

Code review is our primary quality gate. It’s where we catch bugs, share knowledge, and ensure maintainability.

## The Process

1. **Open a Pull Request (PR)** against `main`.
2. **Fill the Checklist**: Verify you’ve self-reviewed your code.
3. **Request a Review**: Tag a peer or code owner.

## The "Social Block" Rule

> **Context**: We currently use GitHub Free, so we cannot enforce all branch protection rules programmatically. We rely on **Social Enforcement**.

**Do NOT click Merge if:**
- ❌ CI checks are failing.
- ❌ You do not have at least one independent approval.

**Process Breach**: Merging without these checks is considered a serious violation of our engineering guidelines.

## For Reviewers

Your goal is to verify:
- **Quality**: Is the code readable and efficient?
- **Correctness**: Does it meet the Acceptance Criteria?
- **Safety**: Are there security risks?

**SLA**: Please aim to review PRs within **24 working hours**. Unblocking peers is high priority.
