# 📖 How to use it

[Traditional Chinese overview](README.md) · [English prompt](prompt.en.md) · [English guide](guide.en.html) · [Traditional Chinese prompt](prompt.md) · [Traditional Chinese guide](guide.html) · [Home](../../README.en.md)

When an AI can enter your project or folder, the question is no longer only whether it gives a good answer. It can edit before it understands the rules, draw a conclusion from unchecked material, or say a job is finished halfway through.

These instructions give that kind of agent a clear way to work. The agent needs to understand the project and task before doing what needs doing. A small fix should not become a ceremony. But data, secrets, publication, and changes that affect each other need clear scope and impact before work begins, and a result you can check afterwards. Your tool's permissions—and any real decision to publish or make an irreversible change—remain yours.

## From familiar principles to working rules

![How 02 Prompt turns familiar AI principles into working rules](images/prompt-02-principles-en.png)

This instruction does not provide built-in knowledge of research, code, law, or any industry. It governs how an agent uses the user's request, project files, tools, permissions, and checkable sources.

You may already use `Follow YAGNI principles`, `Keep it simple`, `Verify before acting`, `Plan before execution`, or `Human in the loop`. Those principles are useful, but on their own they usually do not define conditions, stopping points, or exceptions. 02 turns them into working rules:

| Familiar prompt direction | What the short phrase leaves open | How 02 makes it operational |
|---|---|---|
| `Follow YAGNI principles` / `Keep it simple` | What can be omitted, and what is still required for this delivery. | Match effort to consequence, uncertainty, and reversibility. Include only issues that block acceptance, were caused by the change, or make the delivery inconsistent. Make the smallest complete related change. |
| `Verify before acting` | What to verify, and what to do when sources conflict. | Read the source of truth and direct context first. Separate source, date, fact, inference, and what remains unverified. |
| `Plan before execution` | Whether small work needs a long plan, and when a plan is reliable. | Use a full-picture plan only for dependent, consequential, hard-to-recover, or externally consequential work. The plan needs success evidence, counterexamples, and an applicable independent challenge. |
| `Human in the loop` | What safe work can proceed, and what must stop for approval. | Proceed with authorized, low-risk, reversible, no-side-effect work. Require separate explicit authorization for publishing, deletion, access changes, spending, and other external actions. |
| `Manage context` | How to avoid long rules, search output, and stale context interfering with each other. | Map the scope with search, indexes, and sampling, then read direct material. Preserve handoff state separately for long-running work. |

These directions align with public guidance from OpenAI, Anthropic, and Google: use direct, structured rules; remove repetition; and keep the high-signal material needed to complete the work. This is not an endorsement of 02 by any of them. 02 integrates public principles with failure modes observed in practical agent work into one usable instruction. References: [OpenAI model guidance](https://developers.openai.com/api/docs/guides/latest-model), [Anthropic context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents), and [Google prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies).

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
