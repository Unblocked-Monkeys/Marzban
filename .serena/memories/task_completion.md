# Task completion checklist
- Validate changed YAML/compose files after CI/CD edits.
- For backend/runtime changes, run the narrowest relevant verification available (for example `alembic upgrade head`, app startup checks, or targeted tests if present).
- For dashboard-related changes, ensure the Vite build still succeeds.
- Check `git diff --check` before finishing to catch whitespace or merge-marker issues.
- If container/runtime files changed, verify `docker compose config` or equivalent config rendering when possible.
