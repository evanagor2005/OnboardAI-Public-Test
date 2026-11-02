# Software: backend development

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Created: 2026-10-20 (simulated source date).
Last updated: 2026-11-02 (simulated source date).

This synthetic guide describes the Cedar Works development environment. It is not a real company's operating policy. Dates are simulated source metadata, not Git commit timestamps.

## Prepare a local development environment

Cedar Works backend development uses Python 3.14, uv, Django, and PostgreSQL. Install uv, clone the application repository, and open a terminal at its root. Keep each repository's virtual environment separate from other projects.

Install the locked Python dependencies with:

```sh
uv sync --locked
```

Use the repository's safe environment template for local configuration, then start its documented PostgreSQL development service. Keep the database and generated credentials local. Never copy production data into a development database.

## Start the Django backend

From the application repository root, run:

```sh
uv run python manage.py runserver
```

Open the local address printed by Django and confirm the development page loads. If startup fails, check the Python version, dependency sync, local environment variables, and database availability before changing shared configuration.

## Check the application configuration

In another terminal at the repository root, run:

```sh
uv run python manage.py check
```

A successful check means Django can load the project configuration. Run this check and the relevant tests before changing backend code so pre-existing failures can be separated from new regressions.

## Make a focused backend change

Work on a feature branch and keep each change focused. A change to persistent data needs a migration that describes the schema change and remains compatible with the application's release order. If a new Python dependency is required, record it in the project metadata and lockfile so another developer can reproduce the environment.

Keep passwords, tokens, and other generated credentials out of Git. Do not commit local `.env` files, private keys, database backups, or production settings. Ask the Software onboarding buddy if the documented setup and observed behavior disagree.

## Review and verify the change

Before requesting review, run the checks and tests related to the change and confirm the backend still starts with the documented local commands. Open a merge request that explains the behavior change, verification performed, and any known limitations. Wait for the required approvals and a successful pipeline before merging.

After merge, confirm the development environment still starts from a clean checkout. Report a shared-environment failure to the Software team rather than changing production settings while troubleshooting a local setup problem.

## Knowledge check

Which command installs the locked dependencies? How do you start Django and check its configuration? Where should generated local credentials be kept?
