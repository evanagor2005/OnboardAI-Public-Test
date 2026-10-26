# Backend development

## Prepare your environment

Clone the OnboardAI repository and open a terminal at its root. Install the Python version required by the project and install `uv`. Keep this project's virtual environment separate from other repositories.

## Install dependencies

Run `uv sync --locked` to create the virtual environment and install the dependency versions recorded in the lockfile. If setup fails, check that you are using the required Python version and that the lockfile is present.

## Start the Django backend

From the repository root, run:

```sh
uv run python manage.py runserver
```

Open the local address printed by Django to check that the development server started.

## Check the setup

In another terminal at the repository root, run:

```sh
uv run python manage.py check
```

A successful check means Django can load the project configuration. Before changing backend code, run the project's existing checks and tests so you can distinguish pre-existing failures from new ones.

## Keep local settings safe

Use the repository's example environment file for local configuration. Keep passwords, tokens, and other generated credentials out of Git. Ask the Software onboarding buddy if the setup guide and the behavior you see disagree.
