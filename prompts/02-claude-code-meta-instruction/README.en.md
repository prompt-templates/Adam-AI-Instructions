# 📖 How to use it

[Traditional Chinese overview](README.md) · [English prompt](prompt.en.md) · [English guide](guide.en.html) · [Traditional Chinese prompt](prompt.md) · [Traditional Chinese guide](guide.html) · [Home](../../README.en.md)

When an AI can enter your project or folder, the question is no longer only whether it gives a good answer. It can edit before it understands the rules, draw a conclusion from unchecked material, or say a job is finished halfway through.

These instructions give that kind of agent a clear way to work. The agent needs to understand the project and task before doing what needs doing. A small fix should not become a ceremony. But data, secrets, publication, and changes that affect each other need clear scope and impact before work begins, and a result you can check afterwards. Your tool's permissions—and any real decision to publish or make an irreversible change—remain yours.

## What it helps with

| Tool | Simplest installation point |
|---|---|
| Claude Code | Root `CLAUDE.md` |
| OpenAI Codex | Root `AGENTS.md` |
| Cursor | Root `AGENTS.md` |
| Antigravity | Always-on Workspace Rule |

Ordinary ChatGPT and Claude web chat are not supported here as reliable project agents.

## What changes after installation

- The agent finds the relevant files, rules, and acceptance path before changing code.
- Research separates source, date, fact, inference, and unknowns.
- A new file follows an existing project or platform location instead of inventing a folder.
- A write is read back; failure, interruption, or conflict cannot be reported as success.
- Deletion, overwrite, release, access, money, and secrets have extra confirmation gates.
- A small edit stays short. A plan where a mistake would have a larger impact must survive an independent challenge before it is called executable.
- You do not receive a half-finished plan that still needs its main checks. If a core condition is missing, the agent explains the block and exactly what is needed to continue.

## Fast setup

1. Copy [prompt.en.md](prompt.en.md).
2. Open the correct project or workspace.
3. Paste it at the location in the table, save it, then start a fresh task.
4. Try one small real task: ask the agent to read project rules, correct one small mistake, and read it back.

Use the current official instructions for UI details: [Claude Code](https://code.claude.com/docs/en/memory), [Codex](https://developers.openai.com/codex/guides/agents-md/), [Cursor](https://docs.cursor.com/context/rules-for-ai), and [Antigravity](https://antigravity.google/docs/rules-workflows).

## It does not make every task complicated

The instruction matches effort to impact. A clear small fix can be completed and read back directly. Work involving data, secrets, public release, or several dependent changes gets the extra checks and confirmation it needs.

You do not need to understand how the rules were assembled. Paste the full instruction into your tool, then begin with one small, real task.
