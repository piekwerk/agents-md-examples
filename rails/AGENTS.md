# AGENTS.md — Ruby on Rails

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: Ruby on Rails
- Package manager: Bundler
- Source lives in `app/`; tests in `spec/`.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `bundle install` |
| Run dev server | `bin/rails server` |
| Run tests (single file) | `bundle exec rspec spec/path/to_spec.rb -e 'description'` |
| Run all tests | `bundle exec rspec` |
| Lint | `bundle exec rubocop` |
| Run migrations | `bin/rails db:migrate` |

## Code style

- Convention over configuration: follow Rails' own naming before inventing structure. Business logic lives in models, service objects, or jobs. Controllers stay CRUD-shaped.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (RSpec: request specs for API behavior, model specs for logic, system specs sparingly because they are slow).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Factories (factory_bot) over fixture files. Request specs assert JSON structure and status, not implementation.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (drop table, rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- Migrations are forward-only. `schema.rb` is generated, never hand-edited.
- Strong parameters in every controller. `params[:x]` direct access in a create/update path is a bug.
- N+1 checks: use `strict_loading` or Bullet in test env. Queries inside views get reviewed hardest.

## Definition of done

1. `bundle exec rspec` passes.
2. `bundle exec rubocop` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
