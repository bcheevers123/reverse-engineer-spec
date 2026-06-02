# reverse-engineer-spec

An agent skill that analyses an existing project and produces a clean rebuild brief — without inheriting the original's flaws.

## What it does

Point it at any codebase and it will:

1. **Reconstruct the original spec** — what the project was meant to do, inferred from code, structure, git history, config, and tests
2. **Find design flaws** — where the design broke down, each with a root cause and cost
3. **Produce a clean rebuild brief** — a revised spec with every flaw resolved, ready to hand to an AI agent or a planning session

Everything lands in a `reverse-engineering-new-project/` folder alongside your source project — spec plus useful reference files copied from the original (brand assets, docs, config templates, domain knowledge). No source code, no migrations, no build artefacts.

## Compatibility

Works with any agent that supports the [Agent Skills](https://agentskills.io) open format, including Claude Code, Codex, Gemini CLI, Cursor, GitHub Copilot, and OpenCode.

References to `superpowers:writing-plans` and `superpowers:brainstorming` in the output require the [Superpowers](https://github.com/obra/superpowers) plugin, which is available for all of the above.

## Installation

Copy the skill folder into your skills directory:

```bash
# Claude Code / Gemini CLI / OpenCode — Mac / Linux
cp -r reverse-engineer-spec ~/.claude/skills/

# Claude Code — Windows
xcopy /E /I reverse-engineer-spec %USERPROFILE%\.claude\skills\reverse-engineer-spec

# Codex
cp -r reverse-engineer-spec ~/.codex/skills/
```

The skill is picked up automatically on next launch.

## Usage

Just tell Claude to analyse a project:

> "Reverse engineer the spec for the project at `path/to/my-project`"

Claude will assess the project size and either analyse it directly or fan out parallel specialist agents for large codebases.

## Output

```
reverse-engineering-new-project/
  spec.md                  # Three-section reverse-engineered spec
  .env.example             # Required environment variables
  pyproject.toml           # Dependency reference
  docker-compose.yml       # Infrastructure intent
  assets/                  # Brand assets, style guides, examples
  docs/                    # Domain knowledge docs
  ...                      # Any other useful reference files
```

`spec.md` has three sections:

- **Part 1 — Inferred Original Specification** — purpose, inputs, outputs, constraints, what was out of scope
- **Part 2 — Flaw Report** — each design flaw with type, how it was detected, root cause, and cost
- **Part 3 — Clean Rebuild Brief** — the revised spec ready to pass to `superpowers:writing-plans` or `superpowers:brainstorming`

## What gets copied

The skill copies files that give a new project a head-start without inheriting the old design's flaws: architecture docs, API contracts, brand assets, config templates, domain knowledge docs, judge criteria, example outputs. It never copies source code, migration scripts, build artefacts, or secrets.

## Author

Barry Cheevers
