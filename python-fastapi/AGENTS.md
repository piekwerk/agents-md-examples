# AGENTS.md — Python + FastAPI

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: Python + FastAPI
- Package manager: uv
- Source lives in `app/`; tests in `tests/`.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `uv sync` |
| Run dev server | `uv run uvicorn app.main:app --reload` |
| Run tests (single file) | `uv run pytest tests/test_file.py -x` |
| Run all tests | `uv run pytest` |
| Lint | `uv run ruff check . && uv run ruff format --check .` |
| Type check | `uv run mypy app` |
| Production build | `uv build` |

## Code style

- Full type hints everywhere. Pydantic models for request/response, never raw dicts in signatures. Dependency injection via `Depends` for DB sessions, auth, and settings. No module-level singletons for anything request-scoped.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (pytest with httpx `AsyncClient` against the app; real logic, fake externals).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Fixtures own setup/teardown. Tests never mutate module state. Async tests via pytest-asyncio in auto mode.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (drop table, rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- One pydantic model per request/response shape. `response_model` is explicit on every route.
- Settings come from a single pydantic-settings object. `os.environ` reads outside it are a bug.
- Sync database drivers must not run in async routes. Use async drivers or `def` routes, never mix.

## Definition of done

1. `uv run pytest` passes.
2. `uv run ruff check . && uv run ruff format --check .` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
