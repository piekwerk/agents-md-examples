# AGENTS.md — React + Vite

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: React + Vite (TypeScript)
- Package manager: pnpm
- Source lives in `src/`; tests in `**/*.test.ts(x)`.

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

- Function components only. Hooks obey the rules of hooks with exhaustive-deps on. State lives as low in the tree as it is used; lift only when two siblings share it.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (component tests with Vitest + Testing Library; query by role and accessible name).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Do not snapshot-test entire component trees. Assert on behavior and roles.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- Vite env vars must be `VITE_`-prefixed. Anything else is build-time only and silently undefined in the client.
- Keep `vite.config.ts` minimal. Plugins need a comment explaining why they are worth their bundle-time cost.

## Definition of done

1. `pnpm test` passes.
2. `pnpm lint && pnpm exec tsc --noEmit` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
