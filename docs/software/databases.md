# Databases

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Created: 2026-10-28 (simulated source date).
Last updated: 2026-11-05 (simulated source date).

This synthetic guide describes Cedar Works development practices. It is not a real company's policy or a production runbook. Dates are simulated source metadata, not Git commit timestamps.

## Use a separate local database

Cedar Works services use PostgreSQL 17 for relational application data. Earlier PostgreSQL versions are no longer supported for new development. Start the database with the repository's documented Compose command, and give it its own named data volume so it never shares data with another project.

Copy the safe example environment file to an ignored `.env` file and use the local-only database name and credentials it provides. Never copy production credentials or customer data onto a developer machine. When a connection fails, check the service name, port, database name, and environment variable names before asking for help in the team's database channel.

## Keep schema conventions predictable

Represent durable application facts with relational tables, explicit foreign keys, and constraints for every invariant the database can enforce. Use plural snake_case table names and descriptive column names. Store every timestamp as `timestamptz` in UTC, and use native date, boolean, and numeric types rather than encoding values in text.

Every foreign key must have an index. Add other indexes only for a measured query pattern, and include the query plan in the merge request that adds them. Application queries must list their columns explicitly; `SELECT *` is not allowed in application code.

## Change schema through migrations

Create a migration with the service's migration framework and commit it in the same merge request as the code that depends on it. Each migration must make exactly one logical change and have a name that describes it. Never edit a migration that has been applied in any shared environment; create a follow-up migration instead.

Use the expand-and-contract pattern for every change that affects existing data: add the new column or table, deploy code that writes both forms, backfill in batches of at most 10,000 rows, switch reads to the new form, and remove the old form only in a later release. Any migration that drops or renames a column requires approval from a database reviewer before merging.

## Review and apply migrations

Run the migration framework's pending-change check and apply migrations to your local database before opening a merge request. Run the full integration test suite, not only the affected tests, against the migrated schema. A second engineer must review every migration, and a database reviewer must also approve any migration expected to run longer than one minute.

CI applies all migrations to a clean database and then rolls the newest migration back and forward once to prove it is reversible. Production migrations run only during the weekly Tuesday release window and are applied in dependency order.

## Reset local data safely

Use the repository's seed command to create repeatable sample records for local work. If your local schema becomes inconsistent, stop the service, run the documented reset command, and then run the seed command again. The reset command refuses to run unless the database host is `localhost`, and you must never point a reset or test command at a shared or production database.

## Backups and recovery

The platform team takes encrypted backups of every persistent service database every hour and keeps them for 35 days. Backups contain sensitive operational data and are available only to authorized operators. Request a restore through the platform team's incident process; developers never download production backups.

The platform team runs a restore drill on the first Monday of every month to confirm that backups can be restored into a compatible environment. Coordinate any migration that changes how stored data is interpreted with the platform team before release so the next restore drill covers it.

## Knowledge check

Which PostgreSQL version should new local development use? How often are production databases backed up, and how long are backups kept? Which migrations need approval from a database reviewer before merging?
