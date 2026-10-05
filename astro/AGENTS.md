# AGENTS.md — Astro

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: Astro (TypeScript)
- Package manager: pnpm
- Source lives in `src/pages/`, `src/components/`, `src/content/`; tests in `**/*.test.ts`.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `pnpm install` |
| Run dev server | `pnpm dev` |
| Run tests (single file) | `pnpm vitest run path/to/file.test.ts` |
| Run all tests | `pnpm test` |
| Lint | `pnpm lint && pnpm exec astro check` |
| Type check | `pnpm exec astro check` |
| Production build | `pnpm build` |

## Code style

- Zero-JS by default. Use islands (`client:*` directives) only where interactivity is proven needed. Content collections with zod schemas are the single source of content structure.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (unit tests for lib/util logic and content collection helpers with Vitest).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Build-time checks (`astro check` + content schema validation) are part of "tests pass."

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- Content collections validate via zod config in `src/content/config.ts`. Schema changes are breaking changes to content.
- `client:` directives: use the smallest one that works (`client:idle` over `client:load`), each with a reason.
- Secrets only in server endpoints or SSR context. `PUBLIC_`-prefixed env vars are world-readable.

## Definition of done

1. `pnpm test` passes.
2. `pnpm lint && pnpm exec astro check` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
