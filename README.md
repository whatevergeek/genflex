# GenFlex

GenFlex is a lightweight, flexible, and adaptive set of facilities that aims to support the user's own SDD workflow. The central `/genflex` or `using genflex` trigger loads the toolkit, understands the request, and dispatches it to the appropriate facility:

- review of documents or code changes by relevant specialist roles;
- ad hoc tracking of user-defined phases; or
- ad hoc logging of changes, decisions, review results, and activity.

It uses Markdown files, so it has no package or installation requirements.

## Install

Copy these files and directories into the root of your project:

```text
.genflex/                         # GenFlex instructions and defaults
.agents/skills/genflex/SKILL.md   # entry point for agent-based tools
.cline/skills/genflex/SKILL.md    # entry point for Cline
```

From the directory containing the `genflex` repository:

```bash
cp -r genflex/.genflex <project-root>/
cp -r genflex/.agents <project-root>/
cp -r genflex/.cline <project-root>/
```

Keep `.genflex/` at the project root. If you use another AI tool, copy the same `SKILL.md` entry point into that tool's skill directory.

## Use

Start a request with either `using genflex` or `/genflex`. Capitalization does not matter.

- `using genflex, start party mode to review this PRD`
- `/genflex, start party mode to review this PRD`
- `/genflex invoke party to review this PRD`
- `/genflex invoke party, ask the Architect and Senior Developer to review the implementation plan`
- `/genflex invoke party, ask the Senior Developer and Test Architect to review these code changes`
- `using genflex, resume phase tracking`
- `using genflex, log this decision`

The trigger dispatches to one of three independent facilities:

```text
/genflex or using genflex
          │
          ▼
  ┌───────┼────────┐
  ▼       ▼        ▼
Agent   Phase    Audit
review  tracking logging
```

For state or resume requests, the trigger checks `genflex-docs/genflex-state.md` for unfinished work by reading its status table. It then dispatches to the instructions for the requested task. GenFlex uses one AI by default. A group review starts only when party, roundtable, or multi-agent review is explicitly requested.

GenFlex does not start or manage the underlying chat session. The AI tool starts the session; GenFlex only loads its instructions and manages its optional support documents within that session.

## Options

Options are plain text in the same chat message as either trigger. Put them after the trigger and before or after your request. Use `/genflex` when your AI tool supports slash-style skill commands; otherwise use `using genflex`.

### `--docs-path <path>`

Use this when phase-tracking and audit files should live somewhere other than the default `genflex-docs/` directory. It applies to phase tracking and audit logging. The path is a directory relative to the project root unless your AI tool specifies otherwise.

```text
using genflex --docs-path notes/genflex, resume phase tracking
using genflex, log this decision --docs-path notes/genflex
```

## Layout and customization

```text
.genflex/
├── agents/       default roles for group reviews
├── skills/       instructions for reviews, state, and audit logs
└── templates/    starting templates for generated documents
```

Generated project files live under `genflex-docs/`:

```text
genflex-docs/genflex-state.md
genflex-docs/audit.md
```

By default, GenFlex creates documents in `genflex-docs/`. To customize a project, add templates under `<docs-path>/templates/` and review roles under `<docs-path>/agents/`. These project files take precedence over the defaults in `.genflex/`. When `--docs-path` is omitted, `<docs-path>` means `genflex-docs/`.

GenFlex uses one AI for normal requests. In party mode, it chooses 2–4 relevant roles or uses only the roles you name in the request. The default Architect is Winston and the default Senior Developer is Amelia. If a named role does not match an available agent, GenFlex asks you to choose from the available roles. If the host cannot run separate agents, GenFlex presents the selected roles sequentially in the current AI session and labels the discussion as simulated. The active party-mode handler loads the artifact being reviewed before requesting opinions. Model selection remains the responsibility of the host AI tool.

After party mode is invoked, follow-up messages in the same AI session stay in party mode. Do not repeat the `/genflex invoke party` trigger unless the host has lost the conversation context or you intentionally want to restart the party discussion.

Audit logs preserve raw user input unless sensitive information must be removed. Secrets, credentials, private personal data, and similar sensitive content are redacted and the redaction is noted in the entry.
