# Loop Agent Instructions

## Overview

Loop is an autonomous AI agent loop that runs Claude Code repeatedly until all PRD items are complete. Each iteration is a fresh instance with clean context.

## Commands

```bash
# Run Loop
./loop.sh [max_iterations]
```

## Key Files

- `loop.sh` - The bash loop that spawns fresh Claude Code instances
- `CLAUDE.md` - Instructions given to each Claude Code instance
- `prd.json.example` - Example PRD format

## Patterns

- Each iteration spawns a fresh Claude Code instance with clean context
- Memory persists via git history, `progress.txt`, and `prd.json`
- Stories should be small enough to complete in one context window
- Always update AGENTS.md with discovered patterns for future iterations
