---
name: vibe-to-production
description: Audit an application's production readiness using the Vibe to Production checklist. Inspect the actual codebase, configuration, tests, and deployment setup. Classify each applicable check as Done, Missing, or Can't verify, with supporting evidence and clear explanations. Prioritize security, data loss, exposed secrets, and cost risks. Provide a ranked remediation plan, and never make changes without the user's explicit approval. Use before launching an app or whenever production readiness needs to be assessed.
---

# Vibe Code Launch Check

## Turn your AI coding assistant into a production-readiness auditor

The checklist in [CHECKLIST.md](CHECKLIST.md) describes what to review. The audit instructions below explain **how an AI coding assistant should inspect your actual application and report its findings**.

Don't just ask your AI to say whether your app looks ready. Ask it to inspect the evidence.

## How to Run the Audit

Give the instructions below to your AI coding assistant while it has access to your project's codebase.

## Audit instructions

Audit the application against the production-readiness checklist in this repository.

### 1. Inspect the actual project

Review the available source code, configuration, tests, deployment files, and relevant Git history before reporting findings.

Look for evidence such as:

- Test files and test configuration.
- CI/CD configuration, including `.github/workflows/`.
- Environment variable handling and secret-management practices.
- API routes, middleware, and server-side authorization.
- Dependency manifests and lockfiles.
- Database configuration, migrations, and backup-related code.
- Error pages and loading, empty, and failure states.
- `robots.txt`, sitemap files, structured data, and metadata.
- Logging, analytics, monitoring, and error-reporting integrations.
- AI model calls, evaluations, and failure handling.

Inspect file contents and relevant implementation details. A filename, dependency, or configuration entry alone does not prove that a feature works.

### 2. Assign an honest status to every applicable item

Use only these statuses:

- **Done** — You found sufficient evidence that the item is implemented. Cite the file, configuration, code path, or test that supports the finding.
- **Missing** — You inspected the relevant area and found that the required implementation is absent or inadequate. Explain what is missing.
- **Can't verify** — The evidence is unavailable, incomplete, or depends on an external service or an operational process you cannot inspect.

Do not mark an item Done simply because a file exists, a package is installed, a test is named, or the user assumes a control is enabled.

### 3. Separate implementation from verification

Distinguish between code that appears to implement a control and evidence that the control works.

For example, a backup script does not prove that backups are running successfully, and a test file does not prove that tests pass.

Run safe, relevant checks when authorized and supported by the environment. Report which commands ran, whether they passed, and any checks that could not be performed.

### 4. Prioritize high-risk findings

Begin the report with the highest-risk issues, especially:

- Exposed secrets and compromised credentials.
- Missing authentication or authorization.
- Unprotected public endpoints.
- Missing backups or untested restores.
- Missing rollback procedures.
- Uncontrolled paid API usage.

Never print secret values, tokens, passwords, private keys, or other credentials in the report. Identify the affected location and credential type without revealing the value.

Checking Git history does not itself prove that every exposed key has been rotated. Rotation must be confirmed through appropriate evidence or by the responsible operator.

### 5. Handle external dependencies honestly

Some controls cannot be confirmed from source code alone, including:

- Billing limits and provider dashboards.
- Live DNS, domain ownership, and certificate status.
- Production backup schedules and restore results.
- External monitoring and alert delivery.
- Production deployment configuration.
- Operational credential rotation.

Mark these Can't verify unless sufficient evidence is available. Tell the user what needs to be confirmed and how to verify it.

### 6. Skip irrelevant checks

Do not penalize an application for controls that genuinely do not apply.

Examples:

- Skip AI-specific checks if the application does not call an AI model.
- Skip password-reset and email-verification checks if the application has no relevant authentication flow.
- Skip transactional email authentication if the application does not send email.
- Adapt SEO checks for applications that are intentionally private or not publicly indexed.

Explain why an item was skipped rather than silently treating it as complete.

### 7. Do not make changes during the audit

The initial task is inspection and reporting only.

Do not modify files, install dependencies, rotate keys, change infrastructure, deploy code, delete data, or alter production settings as part of the audit.

After presenting the findings, offer a prioritized remediation plan. Wait for the user's explicit approval before making fixes.

---

## Required Audit Report Format

Start with a one-line verdict, such as:

**Verdict: Not ready — 3 high-risk gaps and 5 items requiring verification.**

The numbers must reflect actual findings, not estimates.

Organize the report into the following sections.

### 1. High-Risk Findings

| Check | Status | Evidence and explanation |
|---|---|---|
| Spend limits and billing alerts | Can't verify | Provider billing settings were not accessible. |
| Database backups | Missing | No backup implementation or configuration was found in the inspected scope. |
| Restore testing | Can't verify | No evidence of a successful restore test was available. |
| Rollback plan | Done | Documented deployment rollback procedure found at `path/to/file`. |
| Git history secret scan | Done | The specified history scan completed; describe its scope and limitations. |
| Key rotation | Can't verify | Rotation status requires confirmation from the relevant provider or operator. |
| Rate limiting | Missing | Inspected public endpoints lack an effective rate-limiting control. |
| Endpoint authorization | Missing | Identify the affected routes and the missing server-side checks. |

*These are example rows illustrating the format, not findings about your application.*

### 2. Testing and Deployment

Report each applicable item with its status, evidence, and any relevant test results.

### 3. Monitoring and Observability

Report logging, alerting, error tracking, performance monitoring, uptime monitoring, and analytics.

### 4. Infrastructure and Performance

Report domain and SSL configuration, email authentication, image optimization, caching, and environment separation.

### 5. AI-Specific Checks

If the application uses AI, report evaluations, prompt-injection testing, failure handling, token limits, and relevant safety controls. Otherwise, state that the section was skipped because no model integration was found in the inspected scope.

### 6. Users, Privacy, and Accessibility

Report accessibility, privacy documentation, consent requirements, account deletion, and applicable authentication flows.

### 7. User Experience and Launch Polish

Report error states, loading states, metadata, SEO, device testing, slow-network testing, and documentation.

### 8. Top Three Things to Fix First

Rank the three most important next steps by severity and impact.

For each one, include:

1. The identified issue.
2. Why it matters.
3. The recommended fix.
4. The relevant files or external settings involved, if known.

If fewer than three issues are confirmed, list the remaining highest-priority items requiring verification instead of inventing gaps.

### 9. Recommended Next Steps

Offer to fix the missing items in risk order, beginning with security exposures and data-loss risks.

**Do not start making changes until the user explicitly approves the remediation plan.**

---

## How to Use This With Your AI Coding Tool

1. Add the production-readiness checklist and audit instructions to your repository.
2. Open your project in your preferred AI coding assistant.
3. Ask it to run the Vibe Code Launch Check against the actual codebase.
4. Review the evidence and the Can't verify items.
5. Approve a remediation plan before allowing changes.
6. Run the audit again after implementing fixes.

The quality of the report depends on the files, tools, permissions, and operational evidence available to the auditor. No automated checklist can guarantee that an application is secure or production-ready.
