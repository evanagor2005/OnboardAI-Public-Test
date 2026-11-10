# Software: deployment and releases

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Document owner: Platform release coordinator.
Created: 2026-11-05 (simulated source date).
Last updated: 2026-11-09 (simulated source date).
Review status: AI-drafted; reviewed by Evan Agor for accuracy and realism and approved for the synthetic evaluation corpus.

This is synthetic evaluation content. Environments, release windows, and artifact names are fictional Cedar Works examples, not production deployment instructions. Dates are simulated source metadata, not Git commit timestamps.

## Promote a verified artifact

Cedar Works separates local development, CI, staging, and production. Staging uses synthetic records and test integrations. Production settings and credentials are injected through the approved deployment system; they are not copied into a build or a developer's `.env` file.

CI produces an immutable artifact for a specific merged commit SHA. The release record includes that SHA, the artifact digest, successful pipeline evidence, migration requirements, and the previous known-good artifact. A container reference called `latest` is insufficient evidence because its contents can change. Promote the artifact verified in staging rather than rebuilding it with potentially different dependencies for production.

Application configuration is tracked separately from the artifact. Sample configuration names include `APP_ENV`, `DATABASE_URL`, and `RELEASE_SHA`; these names are examples, not instructions to add settings to an existing service. The release owner confirms configuration compatibility without placing secret values in the release record.

## Verify staging and approve production

The release owner deploys the candidate to staging and checks startup, health probes, authentication, a representative read, and a reversible write using synthetic data. Verify authorization failures as well as successful requests. Check dependency connectivity, background work, and sanitized logs for unexpected errors. Record results against the exact artifact digest.

Before production, a second engineer reviews the release record and confirms that required [code reviews](git-workflow-and-code-review.md), [CI gates](testing-and-ci.md), and client-owner checks are complete. The release owner identifies who will deploy, who will observe service health, and who can approve mitigation if something fails. Missing evidence or an unclear recovery path blocks the release.

## Use the Tuesday release window

The sample production release window is Tuesday from 14:00 to 16:00 in America/Denver. Announce the planned services, expected impact, and responsible contacts before the window. The release owner can postpone a release when an incident is active, a required dependency is unhealthy, or there is insufficient observation time remaining.

All production migrations run during this Tuesday window and in dependency order, consistent with [Databases](databases.md). Review long-running operations and schema compatibility before starting. Do not begin a migration near the end of the window if it cannot finish and be verified safely. A release with no schema change still needs the normal verification and approval steps.

## Apply compatible schema changes

Use expand-and-contract changes for existing data: add the new structure, deploy compatible code that writes both forms, backfill in batches of at most 10,000 rows, switch reads, and remove the old structure in a later release. Confirm that old and new application versions can coexist during a rolling deployment. Never edit an already-applied shared migration.

Record required database-reviewer approvals for destructive changes and migrations expected to exceed one minute. Confirm successful CI reversal testing, but do not treat that test as permission to reverse production migrations automatically. A production rollback may be unsafe after new data has been written, even when a clean test database allowed reversal.

## Observe the rollout and recover safely

Deploy progressively where supported, checking each stage before expanding. Compare request failure rate, latency, background-job failures, and database behavior with the pre-release baseline. Verify the expected `RELEASE_SHA` in the restricted operational view. Pause if health probes fail, a critical journey breaks, or monitoring shows a sustained regression.

The release owner coordinates mitigation with the [incident response process](incident-response-and-on-call.md). Redeploy the previous artifact only when it remains compatible with the current schema and configuration. Otherwise, choose a reviewed forward fix or another documented mitigation. Do not drop new columns, erase records, or restore a backup merely to make an older application start.

Only authorized platform operators perform a database restore. The sample backup policy is hourly encrypted backups retained for 35 days, with a restore drill on the first Monday of each month. A restore decision must assess lost writes, application compatibility, and recovery evidence; a backup schedule alone does not guarantee a successful recovery.

## Emergency fixes and release closure

For an urgent incident, the incident commander and release owner may approve an application-only hotfix outside the regular window after review, CI, and compatibility verification. This exception does not authorize a production migration outside Tuesday's window. If recovery needs a schema change, escalate the constraint and use another safe mitigation until the migration can be scheduled.

Observe a completed rollout for at least 30 minutes and through a representative background-job cycle, whichever takes longer. Record the deployed artifact, start and finish times, verification results, and any follow-up actions. Publish a brief change notice with safe user-facing impact information. A merged PR or a completed deployment job alone does not establish release success.

## Knowledge check

Why is an immutable artifact digest needed? When may production migrations run? What must be checked before redeploying the previous application version?
