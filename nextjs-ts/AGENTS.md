# AGENTS.md — Next.js + TypeScript

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: Next.js + TypeScript
- Package manager: pnpm
- Source lives in `app/`, `components/`; tests in `**/*.test.ts(x)`.

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

- Strict TypeScript: no `any` without a comment justifying it. Server components by default, `'use client'` only where interaction requires it. Data fetching in server components or route handlers, not in effects.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (unit with Vitest + Testing Library; route handlers tested directly, not through HTTP).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Component tests assert rendered output and roles, never implementation details like internal state.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (drop table, rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- Server Components must not import browser-only APIs. Guard with dynamic imports.
- Route handlers and server actions validate input with zod before touching data.
- Environment variables needed client-side must be prefixed `NEXT_PUBLIC_`. Everything else stays server-only.

## Definition of done

1. `pnpm test` passes.
2. `pnpm lint && pnpm exec tsc --noEmit` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
