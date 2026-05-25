# Style and conventions
- Python code is configuration-heavy and environment-variable driven; `config.py` exposes many ALL_CAPS module-level constants.
- Naming follows standard Python conventions: snake_case for functions/variables, ALL_CAPS for constants.
- The repo does not appear to use a central formatter config in the root; preserve existing local formatting and avoid broad style churn.
- Frontend uses React + TypeScript via Vite in `app/dashboard`; keep changes aligned with existing package/tooling versions unless there is a strong reason to upgrade.
- CI/CD files favor straightforward shell steps and standard GitHub/Docker actions over heavy abstraction.
