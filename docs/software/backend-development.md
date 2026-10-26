# Backend development

## Before you begin

Install Python 3.14 and uv, then clone the OnboardAI repository.

## Run the backend

From the repository root, run `uv sync` to install dependencies. Start Django with `uv run python manage.py runserver`.

## Test your setup

Run `uv run python manage.py check`. A successful check confirms Django can load the project configuration.
