# AI Coding Agent Config Examples

Ready-to-use config kits for 12 stacks. Each directory contains working AGENTS.md, CLAUDE.md, Cursor rules, and GitHub Copilot instructions that you can drop into your project.

## Stacks

| Stack | Framework | Agent files | Key rules |
|-------|-----------|-------------|-----------|
| `nextjs-ts` | Next.js 15 + TypeScript | 4 | App Router, RSC, server actions |
| `react-vite` | React 19 + Vite | 4 | Hooks, Zustand, Vitest |
| `python-django` | Django 5.1 | 4 | CBV, DRF, pytest |
| `python-fastapi` | FastAPI 0.115 | 4 | Pydantic v2, async, alembic |
| `node-express` | Express 5 + TypeScript | 4 | Zod validation, ESM |
| `rails` | Rails 8 | 4 | Hotwire, importmaps, minitest |
| `go-standard` | Go 1.23 stdlib | 4 | No framework, table tests |
| `rust-tokio` | Rust + Tokio | 4 | Ownership, error handling, async |
| `laravel` | Laravel 11 | 4 | Eloquent, Pest, Livewire |
| `svelte-kit` | SvelteKit 2 | 4 | Runes, form actions, Vitest |
| `astro` | Astro 5 | 4 | Islands, content collections |
| `dotnet` | ASP.NET Core 9 | 4 | Minimal API, EF Core |

## Quick start

```bash
# Copy one stack into your project
cp -r nextjs-ts/.claude your-project/
cp -r nextjs-ts/.cursor your-project/
cp nextjs-ts/AGENTS.md your-project/
cp nextjs-ts/.github/copilot-instructions.md your-project/.github/
```

Or cherry-pick just the agent you use (Claude Code? Copy `.claude/CLAUDE.md`. Cursor? Copy `.cursor/rules/`).

## What these files do

- **AGENTS.md** — GitHub Copilot workspace agent reads this for project context
- **CLAUDE.md** — Claude Code loads this as project instructions on every session
- **.cursor/rules/*.mdc** — Cursor applies these rules when editing matching files
- **copilot-instructions.md** — GitHub Copilot Chat uses this for repository context

## License

MIT
