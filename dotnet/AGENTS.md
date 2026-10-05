# AGENTS.md — .NET (C#)

<!-- Example by Piekwerk AgentConfig Studio — versioned kits for 12 stacks. -->

> Baseline rules for AI coding agents working in this repository.
> Drop this file in your repo root. AI tools that support AGENTS.md
> will pick it up automatically.

## Project context

- Stack: .NET (C#)
- Package manager: NuGet (dotnet CLI)
- Source lives in `src/`; tests in `tests/`.

## Commands

| Action | Command |
|---|---|
| Install dependencies | `dotnet restore` |
| Run dev server | `dotnet run --project src/<Api>` |
| Run tests (single file) | `dotnet test tests/<Project> --filter Name` |
| Run all tests | `dotnet test` |
| Lint | `dotnet format --verify-no-changes` |
| Type check | `dotnet build` |
| Production build | `dotnet publish -c Release` |

## Code style

- Nullable reference types enabled, warnings treated as errors. Records for DTOs, primary constructors where they read cleanly. Dependency injection through constructor parameters only; service locator is banned.
- No dead code: unused imports, unreachable branches, and commented-out code get deleted, not commented.
- Prefer the smallest diff that solves the problem. Do not reformat code the change does not touch.

## Testing expectations

- Every bug fix ships with a regression test that fails without the fix.
- New features include tests at the level the project already uses (xUnit: unit tests per service, integration tests via `WebApplicationFactory<Program>`).
- Tests must be deterministic: no sleeps, no real network, no wall-clock dependence.
- Integration tests spin the real app with replaced external dependencies (Testcontainers or in-memory providers where semantics allow).

## Commit conventions

- Conventional Commits: `type(scope): summary` (feat, fix, docs, refactor, test, chore, perf).
- Summary line ≤ 72 chars, imperative mood, no trailing period.
- One logical change per commit.

## Safety rules

- Never commit secrets, tokens, or connection strings. Use env vars. If one leaks, rotate first, clean history second.
- Never run destructive commands (drop table, rm -rf, force-push to shared branches) without explicit human confirmation.
- Dependency changes: pin exact versions, state why the dep is needed, run the full test suite after adding.

## Stack-specific rules

- Async all the way: no `.Result`/`.Wait()`. They deadlock under load. Async methods end in `Async`.
- Options pattern (`IOptions<T>`) for configuration sections. `IConfiguration` injection into classes is a bug.
- EF Core: queries hitting relations in loops get `AsSplitQuery`/`Include` reviewed. Migrations reviewed like schema DDL.

## Definition of done

1. `dotnet test` passes.
2. `dotnet format --verify-no-changes` passes with zero warnings.
3. New logic is covered by tests.
4. Docs/README updated if behavior or interfaces changed.
