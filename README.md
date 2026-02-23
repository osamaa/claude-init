# claude-init

A Claude Code agent that sets up structured project management systems for other Claude Code projects.

## What It Does

Point it at any project and it scaffolds the **Chief of Staff** pattern — a system where the root Claude Code agent acts as a manager that never writes code directly. It plans, writes task briefs, delegates implementation to sub-agents, reviews their output, and reports back to you.

### What Gets Created

```
your-project/
  CLAUDE.md              # Defines the agent's role, rules, and context
  .claude/
    skills/
      go-git/SKILL.md    # /go-git slash command (git add → commit → push)
      new-idea/SKILL.md  # /new-idea slash command (quick idea capture)
  hq/                    # The agent's workspace
    OPERATIONS.md        # How work gets done (lifecycle, templates, rules)
    TODO.md              # Running todo list
    tasks/               # Task briefs (0001-title.md, 0002-title.md, ...)
    decisions/           # Decision log with rationale
    contracts/           # Cross-project interface agreements
    plans/               # Strategy and planning docs
    ideas/               # Ideas backlog
    guides/              # How-to guides and runbooks
```

### The Workflow It Establishes

```
You request something
    ↓
Agent analyzes and writes a task brief
    ↓
Agent delegates to a sub-agent via Task tool
    ↓
Sub-agent implements, agent reviews and verifies the build
    ↓
Agent reports back to you
    ↓
You test, confirm, then agent commits
```

## How To Use

```bash
cd claude-init
claude
```

Then tell it which project to set up:

```
"Set up project management for ~/code/my-project"
```

It will ask you about the project (name, description, structure, tech stack) and generate everything tailored to your setup.

## Core Principle

The root agent **never edits code** — even for single-codebase projects. It always delegates to sub-agents. The manager manages. This keeps the root agent focused on planning, coordination, and quality control while sub-agents handle implementation.

## Included Skills

### `/go-git`

A one-command git workflow: stages changed files explicitly, commits with a style-matched message, and pushes. Checks if a remote exists before pushing — if there's no remote, it commits and stops. Never force pushes, never amends, skips secrets.

### `/new-idea`

Quick idea capture to the HQ ideas backlog. Usage: `/new-idea create a page for latest news`. No questions asked — it finds the next number, generates a slug, writes a formatted idea file to `{hq}/ideas/`, and confirms. Designed for speed: zero back-and-forth.

## Works With

- **Multi-project setups** (frontend + backend, microservices)
- **Single codebases** (one repo, one language)
- **Monorepos** (multiple packages under one roof)
