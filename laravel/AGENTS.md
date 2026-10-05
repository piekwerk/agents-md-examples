# AGENTS.md — PHP + Laravel

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: PHP + Laravel
- Package manager: Composer
- Source lives in `app/`; tests in `tests/`.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `composer install` |
| Run dev server | `php artisan serve` |
| Run tests (single file) | `vendor/bin/pest tests/Feature/ExampleTest.php` |
| Run all tests | `vendor/bin/pest` |
| Lint | `vendor/bin/pint --test` |
| Type check | `vendor/bin/phpstan analyse` |
| Run migrations | `php artisan migrate` |

## Code style

- Follow Laravel conventions: Form Requests validate, Eloquent models relate, Jobs queue, Events broadcast. Fat controllers are a bug: extract actions or services when a method exceeds orchestration.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (Pest: feature tests per endpoint with RefreshDatabase, unit tests for actions).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Factories generate state. Tests never seed by hand unless asserting the seeder itself.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (drop table, rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- Mass assignment: explicit `$fillable` on every model. `GuardedModel`-style catch-alls are banned.
- Migrations forward-only. Column changes need a `down()` that is actually correct, not stubbed.
- Queued jobs implement retries with backoff and are tested with `Bus::fake` or a sync driver.

## Definition of done

1. `vendor/bin/pest` passes.
2. `vendor/bin/pint --test` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
