# AGENTS.md — Rust + Tokio

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: Rust + Tokio
- Package manager: Cargo
- Source lives in `src/`; tests in `tests/` and `#[cfg(test)]` modules.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `cargo fetch` |
| Run dev server | `cargo run` |
| Run tests (single file) | `cargo test --test <file>` |
| Run all tests | `cargo test` |
| Lint | `cargo clippy --all-targets -- -D warnings && cargo fmt --check` |
| Type check | `cargo check` |
| Production build | `cargo build --release` |

## Code style

- Clippy clean at `-D warnings`. Prefer owned types and clone where it is provably cheap. Reach for lifetimes only when the borrow checker demands it, and comment why. Error types via thiserror for libraries, `anyhow::Result` inside binaries.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (unit tests in `#[cfg(test)]` modules; integration tests in `tests/`; `#[tokio::test]` for async).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Deterministic time via `tokio::time::pause` where timing matters.

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- No `unwrap`/`expect` outside tests and genuinely-infallible cases. Each one gets a comment proving infallibility.
- Spawned tasks are abortable or joined. A detached `tokio::spawn` needs a comment explaining its lifecycle.
- Locking: `std::sync::Mutex` in sync code, `tokio::sync::Mutex` only when holding across `.await` (which is usually a design smell).

## Definition of done

1. `cargo test` passes.
2. `cargo clippy --all-targets -- -D warnings && cargo fmt --check` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
