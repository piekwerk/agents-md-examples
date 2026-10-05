# AGENTS.md — Python + Django

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: Python + Django
- Package manager: uv
- Source lives in Django apps under the project root; tests in `**/tests.py` or `**/tests/`.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `uv sync` |
| Run dev server | `uv run python manage.py runserver` |
| Run tests (single file) | `uv run pytest path/to/tests.py -x` |
| Run all tests | `uv run pytest` |
| Lint | `uv run ruff check . && uv run ruff format --check .` |
| Type check | `uv run mypy .` |
| Run migrations | `uv run python manage.py migrate` |

## Code style

- Fat models, thin views. Business logic lives in model methods or `services.py`. Views orchestrate. ORM queries avoid N+1 (`select_related`/`prefetch_related` reviewed on every queryset touching relations).
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (pytest-django with the `db` fixture where needed; factories via factory_boy over fixtures with hardcoded rows).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Migrations are tested by the CI `makemigrations --check` gate, not by hand.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (drop table, rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- Migrations: never edit an applied migration. Forward-only fixes via new migrations.
- Settings are split per environment (base/dev/prod) with django-environ for secrets. No secrets in settings modules.
- Raw SQL is a last resort. Justify in a comment next to the query. Parameterized always.

## Definition of done

1. `uv run pytest` passes.
2. `uv run ruff check . && uv run ruff format --check .` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
