# Adam's AI Instructions | For agents that actually do the work

[繁體中文](README.md) · [English instruction](prompts/02-claude-code-meta-instruction/prompt.en.md) · [English guide](prompts/02-claude-code-meta-instruction/guide.en.html) · [Traditional Chinese instruction](prompts/02-claude-code-meta-instruction/prompt.md) · [Traditional Chinese guide](prompts/02-claude-code-meta-instruction/guide.html)

This is not a template that tells an AI to “be obedient.”

It gives an AI agent that can read files, change a workspace, use tools, organize material, or prepare a release a steadier way to work: understand first, act second, move quickly when the risk is low, stop when it is not, and leave work that can be checked.

You do not need to be a developer. Put it in the instructions for an agent working inside a project or folder you have deliberately authorized.

> Ordinary ChatGPT and Claude web chat are outside this project’s support scope. They can help you think, but they are not treated here as reliable project agents for local files and cross-session delivery.

## What it changes

Without clear boundaries, an agent can sound decisive while doing the wrong thing: editing before it has read the project, turning a guess into a research conclusion, or treating “a file was written” as proof that the job is done.

This instruction asks it to do the useful things first:

- read project rules, relevant files, and available checks before changing code;
- separate sources, dates, facts, inference, and unverified material in research;
- establish the real source of truth and delivery location before organizing knowledge, then read back after a write;
- state the impact and request the right confirmation before deletion, overwrite, publication, access changes, money, or secrets;
- keep small work light, but challenge a plan where a mistake would have a larger impact before calling it executable.

## Choose your instruction language

Choose either the English or Traditional Chinese version and paste it into the Agent tool you already use. They set the same working boundaries; the difference is the agent’s default reply language.

| Tool | Where to put the instruction |
|---|---|
| Claude Code | Put it in `CLAUDE.md` at the project root. |
| OpenAI Codex | Put it in `AGENTS.md` at the project root. |
| Cursor | The simplest path is root `AGENTS.md`; Project Rules also work. |
| Antigravity | Create an always-on Workspace Rule and paste the instruction. |

## Start in three minutes

1. Open the [English instruction](prompts/02-claude-code-meta-instruction/prompt.en.md) and copy it.
2. Open the right project or workspace in your tool. Do not begin by giving an agent an unrelated personal folder.
3. Paste the prompt where the table says, save it, and begin a fresh task.
4. Try one small, real job: “Read this project’s rules and test instructions, then fix one typo in the README and read it back to confirm.”

Current official setup references:

- [Claude Code: CLAUDE.md](https://code.claude.com/docs/en/memory)
- [OpenAI Codex: AGENTS.md](https://developers.openai.com/codex/guides/agents-md/)
- [Cursor: Rules and AGENTS.md](https://docs.cursor.com/context/rules-for-ai)
- [Antigravity: Rules](https://antigravity.google/docs/rules-workflows)

## Why it does not make work complicated

This instruction does not ask an agent to stop and write a plan for everything. It first judges whether the work is clear, reversible, and likely to have a meaningful impact if something goes wrong.

That means a clear small fix can be completed and read back directly. Work involving data, secrets, public release, or several dependent changes gets the extra checks it needs. You get fewer unnecessary back-and-forths, and clearer evidence and confirmation when they matter.

## Latest update: v0.8.2

For work with a larger impact, the agent looks for ways a plan could fail before calling it ready to run. Small work stays direct. You can see the scope, risk, and how to check the result before you approve action. [Read what changed](docs/releases/v0.8.2.md)

## With Agent Handoff Kit and Innovation Loop

This instruction governs how the agent works in this task. [Agent Handoff Kit](https://adamchanadam.github.io/agent-handoff-kit/agent-handoff-kit-intro.html) preserves state, handoff, and closeout across work sessions. [Innovation Loop](https://github.com/Adamchanadam/agent-handoff-innovation-loop) helps a longer project move from ideas through research and validation into a plan.

Use only the layer you need:

| Need | Use |
|---|---|
| An agent that reads first, changes carefully, checks its work, and knows when to stop | Project-based AI Agent Instructions |
| A new session or agent that can pick up where the last one stopped | Agent Handoff Kit |
| A long project that needs exploration, validation, and planning to connect | Innovation Loop |

## What this cannot do for you

- It cannot override the tool’s permissions, sandbox, or company policy.
- A prompt is not a backup, access control, or security boundary by itself.
- It does not turn ordinary chat into a reliable project agent.
- It never authorizes publishing, payment, pushing, deletion, or permission changes on your behalf.

## More

- [English overview](prompts/02-claude-code-meta-instruction/README.en.md)
- [Traditional Chinese overview](prompts/02-claude-code-meta-instruction/README.md)
- [English interactive guide](prompts/02-claude-code-meta-instruction/guide.en.html)
- [Traditional Chinese interactive guide](prompts/02-claude-code-meta-instruction/guide.html)
- [Changelog](CHANGELOG.md)

## License and feedback

This project is licensed under the [MIT License](LICENSE). If your experience differs from this guide, share the tool name, instruction location, and a reproducible scenario. Do not include secrets or private file content.
