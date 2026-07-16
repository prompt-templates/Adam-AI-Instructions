---
name: prompt-evaluation-lab
description: "Run the repo-scoped evaluation workflow for a proposed Prompt 02 or project-local skill change, including a plain-language recommendation of evaluation depth. Use only when explicitly invoked as $prompt-evaluation-lab to design, freeze, execute, review, or interpret a versioned evaluation; do not use for ordinary prompt editing or one-off writing."
---

# Prompt Evaluation Lab

Use this skill only after the user asks to evaluate a candidate version. It is a repo-local bundle, not a global installation and not an authority independent of the project rules.

## Required sources

1. Read `dev/PROJECT_MASTER_SPEC.md` for product goal, adoption language, and exclusions.
2. Read `dev/rules/prompt-evaluation.md` for the complete method.
3. Read the target prompt or project skill, its baseline, current QA evidence, `dev/PROJECT_INDEX.md`, and `dev/DOC_SYNC_REGISTRY.md`.
4. Treat any existing frozen research folder as read-only evidence.

## Choose depth in plain language

Read the named preset table in `dev/rules/prompt-evaluation.md` live. Recommend the smallest adequate preset: Quick for a narrow repair, Standard for a material candidate improvement, or Maximum normal for the core no-Prompt／Prompt question. Present the current time target and the decision that each option can answer in everyday language. State that Maximum normal is a strong screening signal, not a universal-proof claim.

Let the user choose only the named time/depth option. Do not ask them to choose models, scenarios, graders, isolation, analysis, retries, or other technical mechanics. After selection, execute the named preset exactly as the method source requires. If its preflight or integrity stop rule fails, stop and report incomplete; do not silently reduce, reroute, retry, or expand it.

## Workflow

1. Classify the request: local repair verification, restricted trial, or candidate replacement.
2. Define the candidate delta and prepare a versioned protocol before any model run. Select the named preset from the method source, then freeze sources, scenario groups, model / environment, repetitions, graders, stop rules, and decision thresholds.
3. Keep stable regression, change-specific, and held-out cases separate. Do not expose held-out cases to the candidate author before freeze.
4. Run only the frozen protocol in isolated environments. Preserve raw outputs append-only and stop on the declared routing, fallback, timeout, or permission condition.
5. Blind comparative outputs where a treatment claim is requested. Apply the declared adjudication rule; do not revise it after seeing outcomes.
6. Report evidence at the correct level: local repair, restricted trial, replacement, rollback, or insufficient evidence. Never turn a targeted passing run into a broad product claim.
7. Index durable artifacts, update sync obligations, and preserve session state / trace in their separate governance homes.

## Boundaries

- Do not modify `docs/experiments/2026-07-14-02-prompt-impact-study/` frozen artifacts or rerun its completed study.
- Do not change the English prompt until the Chinese behavior baseline is verified and a semantic mapping is prepared.
- Do not commit, push, tag, release, publish, or install this bundle globally without separate user authorization.
