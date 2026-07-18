# GenFlex SDD

GenFlex is a small, skills-based Spec-Driven Development framework for party reviews, durable workflow state, and an append-only audit trail.

## Install

Copy these into a project:

```text
.genflex/                         # golden source
pointer-skills/agents/genflex/SKILL.md  # pointer for agent-based tooling
pointer-skills/cline/genflex/SKILL.md   # pointer for Cline
```

Keep `.genflex/` at the project root. The pointer may also be copied into another compatible tooling skill directory.

## Use

Start with `using genflex` (case-insensitive):

- `using genflex, start party mode to review this PRD`
- `using genflex, resume the implementation exercise`
- `using genflex, log this decision`
- `using genflex, start a new session`

GenFlex checks for an existing `sdd-docs/genflex-state.md`, reports in-progress work, and dispatches only the requested feature. State and audit work do not implicitly start party mode.

## Layout and customization

```text
.genflex/
├── agents/       default party roster; project `sdd/agents/` overrides it
├── skills/       party, state, and audit behavior
└── templates/    default audit and state documents
```

Generated project files live under `sdd-docs/`:

```text
sdd-docs/genflex-state.md
sdd-docs/audit.md
```

Use `--docs-path <path>` to change the generated-documents directory. Templates in `<docs-path>/templates/` take precedence over `.genflex/templates/`. Add custom party agents under `sdd/agents/` without changing GenFlex files.

Party mode supports `--solo` and `--model <model>` when the host tooling supports them. Load only the feature and agent files needed for the current request.
