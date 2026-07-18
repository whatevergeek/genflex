# genflex-audit — append-only activity log

Use for audit, log, activity, decision, deliberation, review, or work-duration entries. Default output is `<project-root>/genflex-docs/audit.md`. In the same chat message as the request, use `--docs-path <path>` to choose another directory.

## Initialize

If the audit file does not exist, choose `<docs-path>/templates/audit.md`, then `<project-root>/.genflex/templates/audit.md`, then the built-in minimum heading `# GenFlex Audit Log`. Create parent directories as needed and replace timestamp placeholders with the current ISO 8601 timestamp.

## Record

Append, never rewrite, reorder, or delete prior entries. Begin each entry with the next sequential `Entry XXX` identifier and write each property on its own line. Every entry must include the entry ID, stage, ISO timestamp, complete raw user input (never summarized), AI response/action summary, and context. Capture user decisions and party deliberations faithfully, distinguishing facts from recommendations. For a duration entry include start, end, and elapsed time if known. Corrections append a new entry referencing the original entry ID rather than deleting history.

Audit logging is independent of party mode: logging a review does not start another review. Keep entries concise and link to stable project paths rather than copying large documents.

Log every user input with its timestamp and complete raw text. Log every approval prompt before asking it, and log the user's response after receiving it. Include the stage or interaction context for every entry.
