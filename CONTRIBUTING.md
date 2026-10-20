# Contributing

Pull requests welcome. Each stack directory follows the same structure:

```
stack-name/
  AGENTS.md          # GitHub Copilot agent instructions
  .claude/
    CLAUDE.md        # Claude Code project config
  .cursor/
    rules/
      *.mdc          # Cursor rules (one per concern)
  .github/
    copilot-instructions.md
```

## Adding a new stack

1. Copy an existing directory (e.g. `nextjs-ts/`) as a starting point
2. Replace every stack-specific reference (framework, package manager, test runner)
3. Keep the same file structure — consistency across stacks matters more than per-stack optimization
4. Run the validator if you have it: `python3 validator/validate.py`

## Style

- Plain imperative sentences. No filler words.
- Pin dependency versions where the config references them.
- One concern per Cursor rule file.
