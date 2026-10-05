# AGENTS.md — Node.js + Express

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: Node.js + Express (TypeScript)
- Package manager: pnpm
- Source lives in `src/`; tests in `**/*.test.ts`.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `pnpm install` |
| Run dev server | `pnpm dev` |
| Run tests (single file) | `pnpm vitest run path/to/file.test.ts` |
| Run all tests | `pnpm test` |
| Lint | `pnpm lint && pnpm exec tsc --noEmit` |
| Type check | `pnpm exec tsc --noEmit` |
| Production build | `pnpm build` |

## Code style

- Async handlers are wrapped so rejections hit the error middleware, never fall through. Routes stay thin: parse, delegate to a service, respond. Business logic never lives inside a route handler.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (unit tests for services with Vitest; route tests via supertest against the app instance).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Tests import the app factory, not `app.listen`. No test may bind a real port.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- Every route validates body/query/params with zod schemas at the boundary.
- Error responses follow one shape: `{ error: { code, message } }`. The error middleware is the only place that formats them.
- Config comes from an env schema validated at boot. The process refuses to start with missing vars.

## Definition of done

1. `pnpm test` passes.
2. `pnpm lint && pnpm exec tsc --noEmit` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
