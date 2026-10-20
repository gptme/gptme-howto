# gptme-howto

> Copy-paste recipes for [gptme](https://github.com/gptme/gptme) — the terminal-based AI agent.

[![gptme](https://img.shields.io/badge/powered%20by-gptme-blue)](https://gptme.org)
[![Discord](https://img.shields.io/discord/1271539422017618012?logo=discord&style=social)](https://discord.gg/NMaCmmkxWv)

---

gptme runs real tools — bash, Python, file edits, git — directly in your terminal.
This repo is a collection of task-oriented recipes showing exactly what to type.

## Recipes

| Recipe | What it covers |
|--------|----------------|
| [Edit files surgically](howto-edit-files.md) | Targeted patches, new files, multi-file edits |
| [Review code with context](howto-code-review.md) | PR review, diff review, pre-commit checks |
| [Debug a failing test](howto-debug-python.md) | Reproduce, trace, fix, verify |
| [Automate a workflow](howto-automate-task.md) | Release scripts, deploy scripts, scaffolding |
| [Refactor across files](howto-refactor.md) | Rename, extract, move, signature changes |
| [Connect ibara over MCP](howto-connect-ibara.md) | Configure a local server and verify tool discovery without a desktop task |

## Quick start

```sh
# Install gptme
pipx install gptme

# Start a session
gptme "review my staged changes"
```

Full docs at [gptme.org](https://gptme.org/docs/getting-started.html).

## What makes gptme different

Most AI coding tools send your code to a web UI. gptme runs locally in your terminal with direct access to:

- **Shell** — runs real bash commands, reads output
- **File tools** — minimal-diff patch edits, not full rewrites
- **Python REPL** — executes code directly, not in a sandbox
- **Git** — reads diffs, checks history, stages and commits
- **Web** — fetches URLs and searches when needed

This means the recipes here are *actually running* — not simulations.

## Contributing

Add a recipe:

1. Create `howto-<topic>.md` following the format of existing recipes
2. Add a row to the table above in `README.md`
3. Open a PR

Good recipes: concrete prompt → observable tool flow → tip on how to adapt it.

---

More at [gptme.org](https://gptme.org) · [Discord](https://discord.gg/NMaCmmkxWv) · [GitHub](https://github.com/gptme/gptme)
