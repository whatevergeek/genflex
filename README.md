# GenFlex

GenFlex is a lightweight set of instructions for three tasks:

- reviewing work with a group of specialist roles;
- tracking progress on long-running work; and
- recording decisions and activity.

It uses Markdown files, so it has no package or installation requirements.

## Install

Copy these files and directories into the root of your project:

```text
.genflex/                         # GenFlex instructions and defaults
.agents/skills/genflex/SKILL.md   # entry point for agent-based tools
.cline/skills/genflex/SKILL.md    # entry point for Cline
```

Keep `.genflex/` at the project root. If you use another AI tool, copy the same `SKILL.md` entry point into that tool's skill directory.

## Use

Start a request with either `using genflex` or `/genflex`. Capitalization does not matter.

- `using genflex, start party mode to review this PRD`
- `/genflex, start party mode to review this PRD`
- `using genflex, resume the implementation exercise`
- `using genflex, log this decision`
- `using genflex, start a new session`

GenFlex checks `genflex-docs/genflex-state.md` for unfinished work. It then opens the instructions for the requested task. GenFlex uses one AI by default. A group review starts only when party mode or multi-agent review is explicitly requested.

## Options

Options are plain text in the same chat message as either trigger. Put them after the trigger and before or after your request. Use `/genflex` when your AI tool supports slash-style skill commands; otherwise use `using genflex`.

### `--docs-path <path>`

Use this when state and audit files should live somewhere other than the default `genflex-docs/` directory. It applies to state tracking, audit logging, and new-session setup. The path is a directory relative to the project root unless your AI tool specifies otherwise.

```text
using genflex --docs-path notes/genflex, resume the implementation exercise
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

By default, GenFlex creates documents in `genflex-docs/`. To customize a project, add templates under `<docs-path>/templates/` and review roles under `<docs-path>/agents/`. These project files take precedence over the defaults in `.genflex/`.

GenFlex uses one AI for normal requests. In party mode, it chooses 2–4 relevant roles or uses the roles you name in the request. Model selection remains the responsibility of the host AI tool.
