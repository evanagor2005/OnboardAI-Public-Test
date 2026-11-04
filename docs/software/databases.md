# Databases

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Created: 2026-10-28 (simulated source date).
Last updated: 2026-11-02 (simulated source date).

This synthetic guide describes Cedar Works development practices. It is not a real company's policy or a production runbook. Dates are simulated source metadata, not Git commit timestamps.

## Use a separate local database

Cedar Works services use PostgreSQL for relational application data. Match the major PostgreSQL version declared by the service's development setup so local behavior resembles CI. Start the database with the repository's documented Compose command, and keep its data volume separate from other projects.

Use a local-only database name and credentials from the ignored environment file created from the safe example. Never copy production credentials or customer data into a developer machine. When a connection fails, check the service name, port, database name, and environment variable names before changing shared settings.

## Keep schema conventions predictable

Represent durable application facts with relational tables, explicit foreign keys, and constraints for invariants the database can enforce. Use clear singular table names and descriptive column names. Store timestamps consistently in UTC and use the database's native date, timestamp, boolean, and numeric types rather than encoding them in free-form text.

Add an index when a measured query pattern needs it, especially for foreign keys used in joins and fields used by frequent lookups. Indexes take storage and make writes more expensive, so review query plans and existing indexes before adding another one. Avoid duplicating a value that can be derived safely from a stable relationship.

## Change schema through migrations

Create a migration with the service's migration framework and commit it with the code that depends on the new schema. Keep each migration focused and give it a name that describes the schema change. Do not edit a migration that has already been applied in a shared environment; create a follow-up migration instead.

Prefer additive changes that can be deployed safely: add a nullable column or new table, deploy code that can work with both forms, backfill in bounded batches when needed, then add stricter constraints in a later migration. Review generated SQL for table rewrites, locks, large index builds, and destructive operations. A migration that removes or renames data needs an explicit compatibility and retention plan.

## Review and apply migrations

Run the migration framework's pending-change check and apply migrations to the local database before opening a merge request. Run the affected unit and integration tests against the migrated schema. Review the migration together with model or query changes, and ask a database reviewer about long-running operations or data transformations.

CI applies migrations to a clean database and checks that the service can start against the resulting schema. Production changes follow the reviewed release process and are applied in dependency order. Keep the application compatible with the previous schema during a rolling release; remove compatibility code only after all instances have moved forward.

## Reset local data safely

Use fixtures or generated sample records for repeatable local work. If a local schema becomes inconsistent, stop the service and follow the repository's documented reset procedure for its own database volume. Confirm the selected database and environment before deleting local data. Never point a reset or test command at a shared or production database.

## Backups and recovery

The platform team takes encrypted backups every six hours of persistent service databases and retains them according to the environment's recovery schedule. Backups contain sensitive operational data and are available only to authorized operators. Request a restore through the platform team's documented incident process; do not download a production backup for ordinary feature development.

After a migration that changes the shape or interpretation of stored data, coordinate the release with the platform team so recovery remains possible. A database backup is useful only if its contents can be restored into a compatible environment.

## Knowledge check

Why should a migration be additive during a rolling release? Which checks should run before a migration is reviewed? What should a developer use instead of a production backup for local testing?
