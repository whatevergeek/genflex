# genflex-party — multi-agent review

Use only when the user explicitly requests party mode, a roundtable, or multi-agent review.

## Activation

1. Discover Markdown agents in this order: `<project-root>/sdd/agents/*.md`, then `<project-root>/.genflex/agents/*.md`. Project files with the same name override defaults. If neither location contains agents, use the built-in seven-agent roster: Winston, Mary, John, Amelia, Sally, Paige, and Murat.
2. Present each available agent's icon, name, and role. Ask what artifact, decision, or code change to discuss. Honor `--solo` by roleplaying selected agents in one conversation and `--model <model>` when the host supports model selection.
3. Load project context such as `**/project-context.md` only when present and keep the discussion summary below 400 words.

## Discussion loop

For every user message, select 2–4 relevant agents. Build each prompt from the identity file, compact discussion context, the user's current message, and prior responses when reactions are requested. Agents must not use tools. They should begin with their icon and bold name, speak in the configured language, make specific recommendations, disagree when warranted, and avoid padding or invented evidence.

Present each response in full and in agent order. An optional **Orchestrator Note** may flag disagreements or missing evidence; never blend or paraphrase agent positions. Summarize after 2–3 rounds or a material topic change. Users may address an agent by name or request a new agent. When done, provide a short wrap-up and return to normal mode.

Users can add Markdown agents under `sdd/agents/`. Each should identify name, title, icon, role, and behavior. No registry edit is required.
