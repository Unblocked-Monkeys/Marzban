# Repository Guidelines

## Project Structure & Module Organization
`app/` contains the FastAPI backend. Keep HTTP endpoints in `app/routers/`, Pydantic schemas in `app/models/`, SQLAlchemy models and CRUD in `app/db/`, scheduled work in `app/jobs/`, and subscription/template logic under `app/subscription/` and `app/templates/`. `app/db/migrations/versions/` holds Alembic revisions.

`app/dashboard/` is the React/TypeScript dashboard. Source lives in `src/` (`components/`, `pages/`, `hooks/`, `service/`, `types/`, `utils/`, `assets/`); production output is written to `app/dashboard/build/`.

`cli/` contains the Typer-based CLI and generated CLI docs. `xray_api/` contains the Xray gRPC client and generated protobuf modules; avoid manual edits to generated `*_pb2*.py` files unless regenerating them.

## Build, Test, and Development Commands
```bash
python3 -m pip install -r requirements.txt
cp .env.example .env
alembic upgrade head
DEBUG=true python main.py
python main.py
```
Install backend dependencies, create local configuration, apply database migrations, run with auto-reload/debug behavior, or run normally.

```bash
cd app/dashboard && npm ci
cd app/dashboard && npm run dev
cd app/dashboard && npm run build -- --outDir build --assetsDir statics
./build_dashboard.sh
```
Install dashboard dependencies, start Vite on port 3000, build the dashboard, or run the repository build helper.

## Coding Style & Naming Conventions
Use 4-space indentation for Python and format changed Python files with:
```bash
autopep8 <file> --max-line-length 120
```
Prefer `snake_case` for Python modules, functions, and variables. Keep router modules named by resource, such as `user.py` or `subscription.py`.

Dashboard code uses React 18, TypeScript, Chakra UI, and Prettier with `printWidth: 80`. Use `PascalCase` for components, `use*` for hooks, and colocate feature helpers in the existing `src/` directories.

## Testing Guidelines
No formal test suite is present in this checkout. For backend changes, add `pytest` tests under `tests/` using `test_*.py` names when introducing behavior that can regress. At minimum, validate migrations and syntax before submitting:
```bash
alembic upgrade head
python -m compileall app cli xray_api
cd app/dashboard && npm run build -- --outDir build --assetsDir statics
```

## Commit & Pull Request Guidelines
Base development branches on `dev`. Recent history uses short, lowercase, imperative commits, often with a type prefix, for example `fix: use compact JSON for xhttp extra param` or `bump version to 0.8.4`.

Pull requests should include the problem, the solution, linked issues, migration notes, and screenshots for dashboard-visible changes. For bug reports or PR context, include relevant logs and redact `.env`, certificates, tokens, and Xray configuration secrets.
