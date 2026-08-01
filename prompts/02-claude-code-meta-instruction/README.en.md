# 📖 How to use it

[Traditional Chinese overview](README.md) · [English prompt](prompt.en.md) · [English guide](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.en.html) · [Traditional Chinese prompt](prompt.md) · [Traditional Chinese guide](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.html) · [Home](../../README.en.md)

When an AI can enter your project or folder, the question is no longer only whether it gives a good answer. It can edit before it understands the rules, draw a conclusion from unchecked material, or say a job is finished halfway through.

These instructions give that kind of agent a clear way to work. The agent needs to understand the project and task before doing what needs doing. A small fix should not become a ceremony. But data, secrets, publication, and changes that affect each other need clear scope and impact before work begins, and a result you can check afterwards. Your tool's permissions—and any real decision to publish or make an irreversible change—remain yours.

## From familiar principles to working rules

![How familiar AI principles become working rules in Project-based AI Agent Instructions](images/prompt-02-principles-en.png)

This instruction does not provide built-in knowledge of research, code, law, or any industry. It governs how an agent uses the user's request, project files, tools, permissions, and checkable sources.

You may already use `Follow YAGNI principles`, `Keep it simple`, `Verify before acting`, `Plan before execution`, or `Human in the loop`. Those principles are useful, but on their own they usually do not define conditions, stopping points, or exceptions. These instructions turn them into working rules:

| Familiar prompt direction | What the short phrase leaves open | How these instructions make it operational |
|---|---|---|
| `Follow YAGNI principles` / `Keep it simple` | What can be omitted, and what is still required for this delivery. | Within the user goal and explicit scope, match effort to consequence, uncertainty, and reversibility. Include only issues that block acceptance, were caused by the change, or make the delivery inconsistent. Make the smallest sufficient related change, without letting persistence, sync, or governance expand the task automatically. |
| `Verify before acting` | What to verify, and what to do when sources conflict. | Read the source of truth and direct context first. Separate source, date, fact, inference, and what remains unverified. |
| `Plan before execution` | Whether small work needs a long plan, and when a plan is reliable. | Use a full-picture plan only for dependent, consequential, hard-to-recover, or externally consequential work. The plan needs success evidence, counterexamples, and an applicable independent challenge. |
| `Human in the loop` | What safe work can proceed, and what must stop for approval. | Proceed with authorized, low-risk, reversible, no-side-effect work. Require separate explicit authorization for publishing, deletion, access changes, spending, and other external actions. |
| `Manage context` | How to avoid long rules, search output, and stale context interfering with each other. | Map the scope with search, indexes, and sampling, then read direct material. Preserve handoff state separately for long-running work. |

These directions align with public guidance from OpenAI, Anthropic, and Google: use direct, structured rules; remove repetition; and keep the high-signal material needed to complete the work. This is not an endorsement of these instructions by any of them. The instruction integrates public principles with failure modes observed in practical agent work into one usable rule set. References: [OpenAI model guidance](https://developers.openai.com/api/docs/guides/latest-model), [Anthropic context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents), and [Google prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies).

## What it helps with

The reason for v0.9.3 is to make 02 a single core meta instruction: keep safety, authorization, sources of truth, acceptance, and high-risk counter-review, while reducing repeated workflow language and tool-specific assumptions.

- **Workplace**: for documents, fact checks, summaries, and local work updates, small tasks stay direct while external or irreversible actions still require explicit authorization.
- **Creative**: writing, editing, naming, and visual direction are judged by the brief, tone, format, and constraints instead of engineering workflow; real-world claims still get checked.
- **Coding agent**: the agent reads the target and direct context, makes the smallest sufficient change, and handles stuck tools by checking for partial writes before one equally safe retry.
- **Governance**: rule repairs start by identifying sources of truth and responsibility. Low-risk local repairs stay light; high-risk governance gets a full-picture plan and independent challenge.
- **Counter-review**: when a plan may affect safety, permissions, data integrity, public boundaries, or cross-surface promises, the agent looks for disconfirming cases before treating the plan as ready.

This repo provides the complete meta instruction only. Tool-specific config files, imports, and installation locations should follow that tool's documentation or your Agent Handoff Kit setup. Ordinary ChatGPT and Claude web chat are not supported here as reliable project agents.

## What changes after installation

- The agent finds the relevant files, rules, and acceptance path before changing code.
- Research separates source, date, fact, inference, and unknowns.
- A new file follows an existing project or platform location instead of inventing a folder.
- A write is read back; failure, interruption, or conflict cannot be reported as success.
- If a tool, sandbox, patch, test, or read command gets stuck, the agent first checks for partial writes; only an equally safe, authorized, auditable official channel may be retried once.
- Deletion, overwrite, release, access, money, and secrets have extra confirmation gates.
- A small edit stays short. A plan where a mistake would have a larger impact must survive an independent challenge before it is called executable.
- You do not receive a half-finished plan that still needs its main checks. If a core condition is missing, the agent explains the block and exactly what is needed to continue.

## Fast setup

1. Copy [prompt.en.md](prompt.en.md).
2. Open the correct project or workspace.
3. Paste it where your tool keeps long-term project instructions or rules, save it, then start a fresh task.
4. Try one small real task: ask the agent to read project rules, correct one small mistake, and read it back.

Use the current official instructions or your Agent Handoff Kit setup for tool UI names and long-term instruction locations.

## It does not make every task complicated

The instruction matches effort to impact. A clear small fix can be completed and read back directly. Work involving data, secrets, public release, or several dependent changes gets the extra checks and confirmation it needs.

You do not need to understand how the rules were assembled. Paste the full instruction into your tool, then begin with one small, real task.
