# AGENTS.md examples for every stack

Ready-to-use `AGENTS.md` files for 12 common stacks. Drop one in your repo root and AI coding tools (Claude Code, Cursor, GitHub Copilot, Windsurf, etc.) pick it up automatically.

Each file covers the essentials: project context, commands, code style, testing expectations, commit conventions, safety rules, and stack-specific guardrails.

## What is AGENTS.md?

`AGENTS.md` is a convention for giving AI coding agents project-level instructions. You put it in your repo root. Tools that support it read it before generating or editing code. It is the tool-neutral baseline: you write it once, every agent benefits.

## Stacks

| Stack | AGENTS.md | Language |
|---|---|---|
| [Astro](astro/) | [AGENTS.md](astro/AGENTS.md) | TypeScript |
| [.NET (C#)](dotnet/) | [AGENTS.md](dotnet/AGENTS.md) | C# |
| [Go (standard library)](go-standard/) | [AGENTS.md](go-standard/AGENTS.md) | Go |
| [Laravel](laravel/) | [AGENTS.md](laravel/AGENTS.md) | PHP |
| [Next.js + TypeScript](nextjs-ts/) | [AGENTS.md](nextjs-ts/AGENTS.md) | TypeScript |
| [Node.js + Express](node-express/) | [AGENTS.md](node-express/AGENTS.md) | TypeScript |
| [Python + Django](python-django/) | [AGENTS.md](python-django/AGENTS.md) | Python |
| [Python + FastAPI](python-fastapi/) | [AGENTS.md](python-fastapi/AGENTS.md) | Python |
| [Ruby on Rails](rails/) | [AGENTS.md](rails/AGENTS.md) | Ruby |
| [React + Vite](react-vite/) | [AGENTS.md](react-vite/AGENTS.md) | TypeScript |
| [Rust + Tokio](rust-tokio/) | [AGENTS.md](rust-tokio/AGENTS.md) | Rust |
| [SvelteKit](svelte-kit/) | [AGENTS.md](svelte-kit/AGENTS.md) | TypeScript |

## How to use

1. Pick your stack from the table above.
2. Copy the `AGENTS.md` into your repo root.
3. Edit the command table to match your project (package manager, test runner, build script).
4. Commit it. Done.

The file works on its own. No other files required, no install step.

## Want the full kit?

These examples cover the `AGENTS.md` baseline. The full [Piekwerk AgentConfig Studio](https://piekwerk.gumroad.com/l/agentconfig) kits add:

- **CLAUDE.md** for Claude Code (verification loop, anti-patterns, `@import` from the baseline)
- **Cursor rules** (4 scoped `.mdc` files: core, stack, testing, safety)
- **copilot-instructions.md** for GitHub Copilot
- **8 workflow skills** (PR review, migration safety, dependency audit, etc.)
- **Idempotent installer** with dry-run, doctor, and uninstall
- **Validation harness** proving structural integrity across all 12 stacks
- **12 months of drift-watch updates** as tool formats evolve

All 12 stacks. One purchase.

## Contributing

Found a mistake? Have a stack you want added? Open an issue or PR.

## License

MIT. See [LICENSE](LICENSE).

---

Built by [Piekwerk](https://piekwerk.com).
