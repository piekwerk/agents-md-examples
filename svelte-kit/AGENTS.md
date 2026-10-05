# AGENTS.md — SvelteKit

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: SvelteKit (TypeScript)
- Package manager: pnpm
- Source lives in `src/lib/` and `src/routes/`; tests in `**/*.test.ts`.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `pnpm install` |
| Run dev server | `pnpm dev` |
| Run tests (single file) | `pnpm vitest run path/to/file.test.ts` |
| Run all tests | `pnpm test` |
| Lint | `pnpm lint && pnpm exec svelte-check` |
| Type check | `pnpm exec svelte-check` |
| Production build | `pnpm build` |

## Code style

- Load functions fetch; components render. Server-only data stays in `+page.server.ts` / `+server.ts`. The moment a module imports something Node-specific, it belongs there, not in shared code.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (unit tests for lib logic with Vitest; route handlers tested by importing `+server.ts` directly).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Testing Library for components when they hold behavior. Pure rendering is not unit-test-worthy.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- `$lib/server` imports are server-only by construction. Never route around them via re-exports.
- Form actions over client-side fetch for mutations where progressive enhancement matters.
- Stores: prefer runes (`$state`/`$derived`) in new code. Mixing stores and runes in one component needs a comment.

## Definition of done

1. `pnpm test` passes.
2. `pnpm lint && pnpm exec svelte-check` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
