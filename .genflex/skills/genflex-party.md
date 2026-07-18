# genflex-party — multi-agent review

Use only when the user explicitly requests party mode, a roundtable, or a multi-agent review. General GenFlex requests use one AI and must not activate this skill.

## Activation

1. Use the resolved docs path from the pointer (default `<project-root>/genflex-docs/`) and discover Markdown agents in this order: `<docs-path>/agents/*.md`, then `<project-root>/.genflex/agents/*.md`. Project files with the same name override defaults. If neither location contains agents, use this built-in roster: Winston (Architect), Mary (Business Analyst), John (Product Manager), Amelia (Senior Developer), Sally (UX Designer), Paige (Technical Writer), and Murat (Test Architect).
2. Present each available agent's icon, name, and role. Ask what artifact, decision, or code change to discuss.
3. Before requesting opinions, load the artifact or project files needed for the discussion with the host's available tools. Give agents the relevant content or a compact evidence-based excerpt; do not ask them to review material they have not been given. Load project context such as `**/project-context.md` only when present and keep the discussion summary below 400 words.

## Discussion loop

After activation, remain in party mode for subsequent messages in the same AI session. Do not require the user to repeat `/genflex invoke party` or `using genflex` for each follow-up. Preserve the discussion context, the available roster, and the currently engaged agents. The initial roster display is not itself a response from every agent; engage agents when the user provides the artifact, question, or review request.

For every user message, select 2–4 relevant agents unless the user names specific agents. When the user names agents or roles, use only those agents; match case-insensitively against agent names, titles, and role descriptions. The default Winston role is the Architect, and Amelia is the Senior Developer. If a requested role has no match, explain the available names and ask the user to choose. Rotate relevant agents over time so the same voices do not dominate every round. When agents agree, invite a complementary or contrarian perspective when useful. Use separate agents in parallel when the host supports it. If the host cannot spawn separate agents, simulate the selected roles sequentially in the current AI session and state that this is a simulated party discussion. Build each prompt from the identity file, compact discussion context, the loaded artifact evidence, the user's current message, and prior responses when reactions are requested. Agents must not use tools. They should begin with their icon and bold name, speak in the configured language, make specific recommendations, disagree when warranted, and avoid padding or invented evidence.

Present each response in full and in agent order. An optional **Orchestrator Note** may flag disagreements or missing evidence; never blend or paraphrase agent positions. Summarize after 2–3 rounds or a material topic change. Users may address an agent by name or request a new agent. When done, provide a short wrap-up and return to normal mode.

## Follow-up patterns

- If the user asks one agent to respond to another agent's point, engage only the requested agent and include the referenced response as context.
- If the user asks to bring in an agent, engage that agent with a compact summary of the discussion so far.
- If the user asks what multiple named agents think about another agent's proposal, engage only the named agents and include the proposal as context.
- If the user continues the general discussion, select a fresh relevant combination of agents.
- If the user says `thanks`, `that's all`, `end party mode`, or otherwise indicates they are done, provide a brief wrap-up and return to normal mode.

Users can add Markdown agents under `<docs-path>/agents/`. Each should identify name, title, icon, role, and behavior. No registry edit is required. Exit party mode only when the user says they are done, asks to return to normal mode, or invokes another GenFlex feature.
