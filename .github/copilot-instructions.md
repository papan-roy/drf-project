# Copilot / AI agent instructions for this repository

This is a minimal Django project named `watchmate` with one app `watchlist_app` (scaffolded).
Keep instructions short and actionable — the goal is to let an AI agent be productive quickly.

Core overview
- Project root: `watchmate/` (contains `manage.py`).
- Django project package: `watchmate/watchmate/` (settings, urls, wsgi, asgi).
- Application: `watchmate/watchlist_app/` (models.py, views.py, tests.py, migrations/).
- Virtualenv: `menv/` — use it for running/manage commands locally.
- DB (dev): SQLite at `BASE_DIR / 'db.sqlite3'` (configured in `watchmate/watchmate/settings.py`).

Quick dev workflows (PowerShell on Windows)
- Activate environment: `.
  menv\Scripts\Activate.ps1` (PowerShell) or `menv\Scripts\activate.bat` (cmd).
- Run migrations: `python watchmate\manage.py migrate` (or `cd watchmate ; python manage.py migrate`).
- Create superuser: `python watchmate\manage.py createsuperuser`.
- Start dev server: `python watchmate\manage.py runserver`.
- Run tests: `python watchmate\manage.py test` (app tests are under `watchlist_app/tests.py`).

Key project-specific patterns and notes
- settings:
  - `DEBUG = True` and a hard-coded `SECRET_KEY` in `watchmate/watchmate/settings.py`. Treat as dev-only; do not commit secrets for production.
  - INSTALLED_APPS currently contains only Django contrib apps — the scaffolded `watchlist_app` is not yet added. If you add features, register the app in `INSTALLED_APPS`.
  - Templates `DIRS` is empty and `APP_DIRS = True` is used — prefer `templates/` inside each app for small features.
- Use Pathlib `BASE_DIR` in settings (e.g., `BASE_DIR / 'db.sqlite3'`) — follow this pattern for file paths.
- Models/views/tests: follow standard Django layout. See `watchlist_app/models.py`, `views.py`, `tests.py` for examples (currently scaffolded/no logic).

Integration and boundaries
- No external services or third-party APIs configured in code. If you add integrations, document env vars and required packages in a top-level README.
- WSGI/ASGI entrypoints exist at `watchmate/watchmate/wsgi.py` and `watchmate/watchmate/asgi.py` — use them for deployment/adapters.

What the agent should check before making changes
- Ensure the virtualenv is used (`menv/`).
- Confirm `watchlist_app` is added to `INSTALLED_APPS` before adding models/migrations.
- Use `python manage.py makemigrations` then `migrate` when changing models.
- Keep changes small and runnable: run `python manage.py test` and `runserver` locally where applicable.

Example tasks the agent can perform immediately
- Add `"watchlist_app"` to `INSTALLED_APPS` in `watchmate/watchmate/settings.py` and create an initial migration for a new model.
- Implement a simple view and URL (add to `watchmate/watchmate/urls.py`) that returns JSON for a stubbed endpoint.
- Add a basic test in `watchlist_app/tests.py` that asserts the stub endpoint returns 200.

Files to open first (high signal-to-noise)
- `watchmate/manage.py` — how commands are invoked.
- `watchmate/watchmate/settings.py` — DB, INSTALLED_APPS, DEBUG.
- `watchmate/watchmate/urls.py` — current URL surface (only admin/).
- `watchmate/watchlist_app/` — models, views, tests, migrations.

Security/secret handling note
- Do not hardcode or expose secrets in PRs. Treat `SECRET_KEY` in settings as dev-only; prefer using environment variables for production.

If something is unclear
- Ask the repo owner where they expect the primary `manage.py` to be invoked from (root vs `watchmate/`), and whether `menv/` is the recommended dev environment.

Feedback request
- If anything here is incomplete or you'd like additional conventions (formatting, linter, CI commands), tell me what to add and I'll iterate.
