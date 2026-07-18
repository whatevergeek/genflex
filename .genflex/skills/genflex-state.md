# genflex-state — workflow state tracking

Use for state, tracking, resume, or long-running work. Default docs path is `<project-root>/genflex-docs/`. In the same chat message as the request, use `--docs-path <path>` to choose another directory.

## Initialize

If `<docs-path>/genflex-state.md` does not exist, choose the first available template: `<docs-path>/templates/genflex-state.md`, then `<project-root>/.genflex/templates/genflex-state.md`, then the built-in format below. Create parent directories as needed and replace timestamp placeholders with the current ISO 8601 timestamp.

```markdown
# GenFlex Workflow State
**Started**: `<ISO timestamp>`
**Updated**: `<ISO timestamp>`
**Status**: `in-progress`
**Current Task**: `<task description>`
**Completed Items**: []
**Pending Items**: []
**Decision Log**: []
```

Do not overwrite an existing file merely because it is incomplete. If malformed, preserve it, report the issue, and repair only fields needed for the requested operation.

## Update and resume

After each significant step, update `Updated`, `Current Task`, item lists, and decision entries. Move completed items out of Pending, keep prior decisions, and set `Status` to `complete` only when work is finished; add the final timestamp at completion. On resume, present current task, status, completed items, pending items, and decisions, then ask what pending item to handle next. State tracking is single-agent work and must not invoke party mode.
