# Software: testing and CI

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Document owner: Software quality coordinator.
Created: 2026-11-04 (simulated source date).
Last updated: 2026-11-09 (simulated source date).
Review status: AI-drafted; reviewed by Evan Agor for accuracy and realism and approved for the synthetic evaluation corpus.

This is synthetic evaluation content. Pipeline names and quality gates are fictional Cedar Works examples, not executable configuration for this documentation repository. Dates are simulated source metadata, not Git commit timestamps.

## Choose tests that prove behavior

Continuous integration (`CI`) checks proposed changes before merge. Local testing gives faster feedback, but both should prove behavior rather than repeat implementation details. A useful regression test fails when the reported defect is present and passes when the intended behavior is restored.

Use unit tests for isolated logic, integration tests for interactions with the database or another component, and end-to-end (`E2E`) tests for critical user journeys. For a progress update, unit tests might check state transitions, integration tests should verify persistence and ownership, and an E2E test can confirm the employee sees the saved result after reloading. Keep E2E coverage focused on important journeys rather than duplicating every unit case.

## Prepare an isolated test environment

Install the locked dependencies and run the configuration check using the commands in [backend development](backend-development.md). Use the application's documented test runner; this sample corpus does not define a new runner or promise that a command exists in every service.

Test databases contain synthetic fixtures and must be separate from local working databases, shared environments, and production. In this sample pipeline, `TEST_DATABASE_URL` identifies the disposable test database; the test setup refuses to proceed if its destination matches a configured shared or production endpoint. Do not fall back to `DATABASE_URL` when test configuration is missing. The database hostname and credentials come from the isolated runner environment, not from committed production settings.

Use fixed fixture inputs and controlled clocks where time affects behavior. External services use contract-aware fakes for routine tests. A test that needs a real integration runs only against an explicitly approved test endpoint with test-only credentials. Do not copy employee records or real access tokens into fixtures, snapshots, or CI artifacts.

## Understand the required CI jobs

The following identifiers are sample job names used in Cedar Works pipeline discussions. Their implementations belong in the relevant application repository, not in this document repository.

| Job name | Required evidence |
| --- | --- |
| `lint_and_format` | Repository style checks and configured static analysis pass |
| `unit_tests` | Fast isolated behavior tests pass |
| `integration_tests` | Database and service integration tests pass in isolation |
| `migration_check` | Migration consistency and clean-database application checks pass |
| `security_scan` | Dependency and secret checks have no unresolved release-blocking findings |
| `build_artifact` | A versioned deployable artifact is produced and tied to the commit SHA |

Required jobs run against the proposed merge result as well as the branch where the hosting setup supports that gate. A skipped or canceled required job is not a successful check. The PR must have a successful pipeline for its current head, and the release artifact must have successful verification for the exact merged commit it contains.

## Verify migrations and API contracts

For a schema change, run the full integration suite against the migrated schema. CI applies all migrations to a clean PostgreSQL 17 database, then rolls the newest migration back and forward once, as required by [Databases](databases.md). If reversal fails, stop and resolve the migration design; do not mark the job successful or substitute a production rollback attempt.

API tests cover success, malformed input, missing authentication, denied access, and important boundary cases. Check status codes, response shape, and side effects. Use multiple synthetic identities when ownership or membership affects authorization, and keep fixtures aligned with the [API contract](apis.md). Diagnostics may include a sanitized `request_id`, never an access-token value.

## Investigate failed or flaky pipelines

Start with the first meaningful failure and compare the tested commit and environment with the local reproduction. Preserve the failing job identifier and sanitized log excerpt. Retry only after identifying a transient runner or service problem, or when gathering evidence about an intermittent failure; repeated retries are not a fix.

A flaky test has inconsistent outcomes for the same code and controlled inputs. Assign an owner and investigate shared state, clock dependence, concurrency, and uncontrolled network calls. Do not quietly disable a required test to merge. Any proposed quarantine needs reviewer approval and an equivalent reliable check for the affected behavior before merge; otherwise the PR remains blocked.

CI logs and reports are treated as potentially sensitive artifacts. Follow the [secure coding guidance](secure-coding-and-secrets.md) for redaction and access. A successful pipeline is necessary evidence, but the [code review](git-workflow-and-code-review.md) and release approvals are still required.
