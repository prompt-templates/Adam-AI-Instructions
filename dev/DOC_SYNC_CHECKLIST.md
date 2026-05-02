# Doc Sync Checklist

<!-- LOCAL PROJECT RECORD -->
<!--
  USAGE: At PERSIST phase, if any file was created or modified during CHANGE:
  1. Identify the change category in the registry below
  2. Execute all "Required Doc Updates" for matched rows
  3. Record triggered rows in SESSION_LOG under "Doc Sync"
  4. If your change type has no matching row: add the row first, then proceed
     (prevents this registry from going stale)
-->

## Change Category Registry

| Change Category | Required Doc Updates | Verification Method |
|---|---|---|
| Governance rule change (AGENTS.md) | INIT.md FILE 1 mirror; README if behavior is user-facing | grep parity check |
| Tech stack / build / dependency change | CODEBASE_CONTEXT.md Stack or Build section | manual review |
| External API / service change | CODEBASE_CONTEXT.md External Services block | block format check |
| New governance file added to install | §5a backup list in AGENTS.md; INIT.md ROOT SAFETY CHECK backup list; INIT.md FILE 1 §5a | grep check |
| Session-log maintenance policy changed | AGENTS.md §4a mechanism enforcement; INIT.md FILE 1 §4a + §5a backup list; README*.md safeguards section | grep + policy parity check |
| Session-log entry format / size policy changed | AGENTS.md §4 entry format + budget rule 5; INIT.md FILE 1 §4 mirror; existing over-cap session log entries refactored with detail relocated to `dev/SESSION_STATE_DETAIL.md` | grep parity + per-entry line count |
| Reply behavior governance changed (§11a rules 1-10 incl. judgement / choice format / ambiguity / fact verification / plain language / reply skeleton / emoji vocabulary / output-only / SSOT alignment / register) | AGENTS.md §11a; INIT.md FILE 1 §11a mirror; AGENTS/INIT marker line `MANDATORY REPLY DISCIPLINE`; README*.md if behavior is described user-facing | grep parity check |
| Closeout output skeleton or startup transparency wording changed | AGENTS.md §1 (seed-context line) + §4 rule 3 / rule 6 (Section 2 heading + skeleton); INIT.md FILE 1 mirror; INIT.md install-time Quick Start `Resume in another AI tool` block; README*.md Quick Operations `Resume next session` block (4 languages); harness grep parity checks for new heading text | grep parity check |
| Release notes template / format changed | docs/releases/_TEMPLATE.md (single-source template); existing release notes files retroactively updated only if user-facing impact; harness check for `_TEMPLATE.md` presence + new releases `What you'll feel` section | file existence + grep section presence |
| New project doc added | This file — add a row for the new doc's update triggers | row presence check |
| Preference Priority Order changed (§0c) | AGENTS.md §0c; INIT.md FILE 1 §0c mirror; CORE RULES marker block in both files | grep parity check |
| FPFR output format changed (§3.5 trigger / 5 sections / closing line) | AGENTS.md §3.5 + §3 PLAN HIGH-risk cross-ref; INIT.md FILE 1 mirror | grep parity check |
| Patch-only delivery format changed (§11b) | AGENTS.md §11b + §11 cross-ref; INIT.md FILE 1 mirror; CORE RULES marker block | grep parity check |
| Deep-Fix / Final-Landing trigger changed (§11c) | AGENTS.md §11c; INIT.md FILE 1 mirror | grep parity check |
| Tooling format rules changed (§13 calc / JSON / Mermaid) | AGENTS.md §13.1 / §13.2 / §13.3; INIT.md FILE 1 mirror | grep parity check |
| _[Add project-specific rows below this line]_ | | |

## Anti-pattern: No Matching Row

If your change has no matching row above:
- Do NOT skip silently — add the missing row first, then proceed
- Record the registry addition in SESSION_LOG under `Doc Sync: registry updated`
- Reason: a stale registry is worse than no registry (false safety net)
