---
name: new-idea
description: Quickly capture an idea to the project's ideas backlog
user-invocable: true
---

# /new-idea — Quick Idea Capture

When the user runs `/new-idea <description>`, immediately create an idea file in the HQ ideas directory. No questions, no back-and-forth — just capture it and confirm.

## Steps

1. **Find the HQ directory** — Look for a directory matching `*-hq/` or `hq/` in the project root. Check `CLAUDE.md` if unclear.

2. **Determine the next number** — List existing files in `{hq}/ideas/` and pick the next sequential number (0001, 0002, ...). If the directory is empty or only has `.gitkeep`, start at 0001.

3. **Generate a slug** — Turn the idea description into a short kebab-case slug (3-5 words max). Example: "add dark mode toggle" → `add-dark-mode-toggle`.

4. **Create the file** — Write `{hq}/ideas/NNNN-slug.md` with this format:

```markdown
# Idea: [Short Title]

**Date:** YYYY-MM-DD

## Description

[The user's idea, expanded into a clear 2-4 sentence description. Capture the intent, add any obvious context from the project, but don't over-elaborate.]

## Notes

_No additional notes yet._
```

5. **Confirm** — Reply with a single short line like: `Captured idea #NNNN: [title] → {hq}/ideas/NNNN-slug.md`

## Rules

- **Never ask questions.** Interpret the user's input and just create the file. This is for quick capture — speed matters more than perfection.
- **Never delegate.** Write the file directly — this is an HQ operation, not a code change.
- **Keep it brief.** The description should be 2-4 sentences. Don't write an essay.
- **Use today's date** for the Date field.
- If the ideas directory doesn't exist, create it.
