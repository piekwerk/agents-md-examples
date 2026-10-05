# AGENTS.md — Go (standard library)

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: Go (standard library)
- Package manager: go modules
- Source lives in `cmd/` and `internal/`; tests in `**/*_test.go`.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `go mod download` |
| Run dev server | `go run ./cmd/<server>` |
| Run tests (single file) | `go test ./internal/... -run TestName -v` |
| Run all tests | `go test ./...` |
| Lint | `go vet ./... && test -z "$(gofmt -l .)"` |
| Type check | `go build ./...` |
| Production build | `go build ./...` |

## Code style

- gofmt is not negotiable. Errors are returned, never ignored with `_` without a comment justifying it. Interfaces are declared by their consumer, small (1-3 methods), and unexported unless required.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (table-driven tests in the same package; `httptest` for handlers; no external assertion libraries).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Use `t.Parallel()` where tests are independent. `t.Cleanup` for teardown. No testify; standard library keeps the dependency tree honest.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- Errors carry context with `fmt.Errorf("...: %w", err)`. `errors.Is`/`errors.As` at the boundary decides behavior.
- `context.Context` is the first parameter of every function that does I/O. It is never stored in structs.
- Goroutines are bounded: every `go func()` has an owner that can stop it (context, WaitGroup, or channel close).

## Definition of done

1. `go test ./...` passes.
2. `go vet ./... && test -z "$(gofmt -l .)"` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
