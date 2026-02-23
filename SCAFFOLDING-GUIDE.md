# Scaffolding Guide

This document explains what `claude-init` creates and how to customize it for each project.

## What Gets Created

When you point claude-init at a project, it creates:

### 1. Root `CLAUDE.md`
The most important file. This tells Claude Code:
- **What role it plays** (Chief of Staff / coordinator)
- **What the project is** (context so the AI understands the domain)
- **Rules** (what it can/can't do, where it can/can't edit)
- **Operating procedures** (how to handle work: task briefs first, then delegate)
- **Workspace layout** (what directories exist and what they contain)

### 2. HQ Directory (`{project}-hq/` or `hq/`)
The agent's workspace. Contains:

| Directory | Purpose |
|-----------|---------|
| `tasks/` | Task briefs — the unit of work. Every non-trivial change starts as a task brief. |
| `decisions/` | Decision log — records of key choices and their rationale. |
| `contracts/` | Cross-project contracts — interface agreements between sub-projects. |
| `plans/` | Strategy docs — larger plans that spawn multiple tasks. |
| `ideas/` | Ideas backlog — things to explore later. |
| `guides/` | How-to guides and runbooks — operational knowledge. |

### 3. `OPERATIONS.md`
The operations manual inside the HQ. Defines:
- The task lifecycle (request -> brief -> implement -> verify -> done)
- Task brief format
- Decision log format
- Contract format (for multi-project setups)
- Numbering conventions

### 4. `TODO.md`
A simple running todo list organized by project area.

### 5. `.claude/skills/go-git/`
A skill that gives the agent a `/go-git` slash command — a full git add → commit → push workflow in one step. It checks for a remote before pushing (skips push if none exists), stages files explicitly (no `git add .`), skips secrets, and follows the repo's commit style.

### 6. `.claude/skills/new-idea/`
A skill that gives the agent a `/new-idea` slash command — quick idea capture to the HQ ideas backlog. Usage: `/new-idea create a page for latest news`. No questions asked — it creates a numbered idea file in `{hq}/ideas/` immediately and confirms.

## Core Principle: Always Delegate

The root agent **NEVER edits code directly** — regardless of whether the project has one codebase or ten. It always delegates implementation to sub-agents via the Task tool. The root agent is the manager: it plans, writes task briefs, delegates, reviews output, runs build/verify commands, and reports back. This is non-negotiable.

## Project Types

### Multi-Project (like DrivenArabia)
When a project has multiple sub-directories that are separate codebases (frontend + backend, multiple services, etc.):
- Root agent delegates to named sub-project agents via Task tool
- Contracts are used for cross-project interfaces
- Each sub-project should have its own CLAUDE.md with its conventions

### Single-Project (like vi-go)
When there's just one codebase:
- Root agent still delegates all code changes to sub-agents via Task tool
- No contracts needed (only one codebase)
- Sub-agents are unnamed — just "implementation agent" spawned for each task
- The CLAUDE.md includes tech stack, build commands, key files, and coding conventions so delegated agents have full context

### Monorepo with Packages
When there's a monorepo with multiple packages:
- Treat like multi-project — root agent delegates to sub-agents
- Contracts might be less formal since it's one repo
- Adapt based on how independent the packages are

## Customization Points

1. **Personality** — The user can define a personality for their agent. If they don't care, skip it.
2. **HQ directory name** — Default to `{project}-hq` for multi-project, `hq` for single-project. Let the user choose. (vi-go uses `hq/`, DrivenArabia uses `driven-hq/`.)
3. **Agent names** — Based on the actual directory names.
4. **Target options in task briefs** — List the actual sub-projects.
5. **TODO sections** — Based on the actual project areas.
6. **Contract parties** — Based on the actual sub-projects that need to coordinate.

## What NOT to Create

- Don't create sub-project CLAUDE.md files — those should be created by the people who know those codebases.
- Don't create any actual task briefs, decisions, or contracts — those come from real work.
- Don't set up git, CI/CD, or anything outside the project management system.
- Don't modify existing code files.
