---
name: genflex
description: 'GenFlex Spec-Driven Development framework loader. Loads GenFlex context and dispatches party mode, state tracking, or audit logging when the user says "using genflex".'
---

# genflex — GenFlex Framework Loader

This is a context loader, not an agent persona. The golden source is `.genflex/` at the project root.

## On Activation

1. Verify `{project-root}/.genflex/` exists. If missing, ask the user to copy it from the genflex repository and stop.
2. Resolve the docs path to `{project-root}/sdd-docs/`, or the path supplied with `--docs-path <path>`. If `genflex-state.md` exists and has status `in-progress`, present its current state and ask whether to resume. A `complete` state starts fresh.
3. Parse the case-insensitive text after `using genflex`:
   - `party mode` or `review` → read `.genflex/skills/genflex-party.md`.
   - `state`, `track`, or `resume` → read `.genflex/skills/genflex-state.md`.
   - `audit` or `log` → read `.genflex/skills/genflex-audit.md`.
   - `new session` or `start fresh` → initialize state and audit files, then offer the features.
   - unclear intent → present the available features and ask what the user wants.
4. Dispatch immediately to the selected golden-source skill. Do not roleplay, participate in party mode, or repeat loader instructions.

## Source of Truth

- `.genflex/skills/` — feature behavior
- `.genflex/agents/` — default agent definitions
- `.genflex/templates/` — default generated-document templates

Read only the selected skill and the agent/template files it needs. Keep unchanged files in context and summarize party discussion context below 400 words.
