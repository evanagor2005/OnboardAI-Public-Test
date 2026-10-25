# Software: backend development

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Created: 2026-10-20 (simulated source date).
Last updated: 2026-10-24 (simulated source date).

This is synthetic evaluation content, not a real company's operating instructions. The dates describe the sample's simulated history, not Git commit timestamps.

## Prepare a development environment

A Software employee first accepts the team invitation and checks that their account can open the application repository. Team membership does not grant production access; production access requires a separate reviewed request.

The Cedar Works backend uses Python 3.14, uv, and PostgreSQL 17. Install uv once on the workstation and reuse it across repositories. Each repository has its own virtual environment. From a cloned repository, run `uv sync --locked` to create that environment using the committed dependency lockfile.

Copy the repository's safe environment template to a local `.env` file, generate local secrets, and follow its database startup instructions. Never commit `.env`, private keys, or database backups. A failed local database connection should be investigated by checking the database process and configuration, rather than deleting the data volume.

## Make a backend change

Create a feature branch and make one focused change. Run the affected tests and checks before requesting review. A change that modifies persistent data must include a migration and a brief explanation of the table or relationship changes.

If a new dependency is required, record it in the repository's package metadata and lockfile. Update the relevant development setup guide so a new employee can reproduce the environment. Do not ask a teammate to rely on packages installed only in your local environment.

## Review and merge

Open a merge request describing the behavior change, verification performed, and any remaining limitations. Wait for the configured approvals and a successful pipeline. Do not bypass branch protection or publish a feature that reviewers have not seen.

After merging, confirm the development environment still starts from its documented commands. Report a failing shared environment to the Software team; do not change production settings while troubleshooting a local setup problem.

## Knowledge check

Why can two repositories share one uv installation but still require separate virtual environments? Which files record an added Python dependency? What information should accompany a database migration in a merge request?
