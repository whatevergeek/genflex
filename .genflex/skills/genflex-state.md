# genflex-state — workflow state tracking

Use for state, tracking, resume, or long-running work. Default docs path is `<project-root>/genflex-docs/`. In the same chat message as the request, use `--docs-path <path>` to choose another directory.

## Initialize

If `<docs-path>/genflex-state.md` does not exist, ask the user for the granular phases or work items that the state file must track. Do not invent a phase breakdown when the user has not provided one. Choose the first available template: `<docs-path>/templates/genflex-state.md`, then `<project-root>/.genflex/templates/genflex-state.md`, then the built-in format below. Create parent directories as needed and replace timestamp placeholders with the current ISO 8601 timestamp.

```markdown
# GenFlex Workflow State
**Started**: `<ISO timestamp>`
**Updated**: `<ISO timestamp>`
**General Status**: `<overall progress summary>`
**Next Action**: `<next phase or action>`

| Item | Status |
|---|---|
| `<user-provided phase or work item>` | `PENDING` |
```

Do not overwrite an existing file merely because it is incomplete. If malformed, preserve it, report the issue, and repair only fields needed for the requested operation.

## Update and resume

After each significant step, update `Updated`, `General Status`, `Next Action`, and the status table. Mark finished items `DONE`; keep unfinished items `PENDING`. Use `IN_PROGRESS` or `BLOCKED` only when useful. When all items are `DONE`, update the final timestamp and state that work is complete in `General Status`. Do not record decisions in this file; record them in the audit log. On resume, present the general status, next action, and status table, then ask what pending item to handle next. State tracking is single-agent work and must not invoke party mode.
