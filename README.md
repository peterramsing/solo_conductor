# Solo Conductor

An orchestrator Claude Code session that plans, delegates, and coordinates work across your projects in Solo using the [Solo](https://soloterm.com) tool.

The conductor does not write application code. It spawns agents, tracks progress via todos and scratchpads, and reports back.

---

## What It Does

When you say "build X in project Y", the conductor:

1. Writes a plan to a scratchpad and gets your sign-off
2. Breaks the work into discrete todos
3. Spawns Claude (or Codex) agents into the target project
4. Sends each agent its task with the right Solo context
5. Monitors progress and coordinates between agents
6. Reports back when the work is done

---

## Getting Started

Open this directory in Claude Code. The `CLAUDE.md` contains full orchestration instructions — the conductor will orient itself automatically.

To kick off a task, just describe what you want built and in which project:

> "Add a feature to audio-brevity that lets users save favorite episodes."

The conductor will take it from there.

---

## How It Works

### Coordination Primitives

| Need | Tool |
|---|---|
| Shared plan / notes | `scratchpad_write`, `scratchpad_append` |
| Task tracking | `todo_create`, `todo_complete`, `todo_list` |
| Prevent concurrent edits | `lock_acquire` / `lock_release` |
| Move a todo to another project | `todo_transfer` |

---

## Principles

- **Conductor, not implementer.** Application code lives in the target projects, not here.
- **Plan before spawning.** A clear scratchpad prevents wasted agent cycles.
- **One todo = one agent.** Keep tasks focused and discrete.
- **Always prepend `agent_instructions`.** Spawned agents need Solo context to coordinate correctly.
