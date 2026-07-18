---
name: genflex
description: 'GenFlex Spec-Driven Development support toolkit loader. Loads GenFlex context and dispatches agent review, phase tracking, or audit logging when the user says "using genflex" or invokes "/genflex".'
---

# genflex — GenFlex Support Toolkit Loader

This is a context loader, not an agent persona. The golden source is `.genflex/` at the project root.

## On Activation

1. Verify `{project-root}/.genflex/` exists. If missing, ask the user to copy it from the genflex repository and stop.
2. Read `--docs-path <path>` from the same user message to change the generated-documents directory. Model selection is handled by the host AI tool.
3. Resolve the docs path to `{project-root}/genflex-docs/`, or the path supplied with `--docs-path <path>`. For a phase-tracking or resume request, inspect `genflex-state.md` if it exists. If it has any `PENDING`, `IN_PROGRESS`, or `BLOCKED` items, present the current phase list and ask whether to resume. Treat a list whose items are all `DONE` as complete; start a new list only when the user asks to start new tracking. Do not block an unrelated party or audit request on phase tracking.
4. Parse the case-insensitive text after either `using genflex` or `/genflex`:
   - an explicit `party`, `party mode`, `roundtable`, `invoke party`, or `multi-agent` request → read `.genflex/skills/genflex-party.md`.
   - `state`, `track`, `phase`, or `resume` → read `.genflex/skills/genflex-state.md`.
   - `audit` or `log` → read `.genflex/skills/genflex-audit.md`.
   - unclear intent → present the available features and ask what the user wants.
5. Dispatch immediately to the selected golden-source skill. Use one AI by default; do not start party mode from a general review request unless party mode is explicitly named.

## Source of Truth

- `.genflex/skills/` — feature behavior
- `.genflex/agents/` — default agent definitions
- `.genflex/templates/` — default generated-document templates

Read only the selected skill and the agent/template files it needs. Keep unchanged files in context and summarize party discussion context below 400 words.
