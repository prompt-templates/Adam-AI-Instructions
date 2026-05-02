# Session Handoff

<!-- Compactness budget: Current Baseline max 6 lines; Open Priorities max 5; Known Risks max 7; keep details in SESSION_LOG. -->

## Current Baseline

1. Version: v0.1.0(annotated tag 已 push;GitHub Release 頁尚未建)
2. Core features: 公開分享 Meta Instructions repo;首份 prompt(01-claude-cowork-meta-instruction)含原文 + 文字介紹 + 互動指南 HTML
3. Regression baseline: 互動指南 Hero 三情境(FPFR / 回覆骨架 / Patch)桌面與手機渲染通過實測
4. Release / merge status: v0.1.0 tag 已 push;GitHub Release 頁待建
5. Active branch / environment: main(origin/main 同步;HEAD = ff18056)
6. External platforms in scope: GitHub Pages、Microlink API(og:image 動態載入)

## Layer Map

1. Product / System Layer: 公開分享 prompts 內容;GitHub Pages 靜態站
2. Development Governance Layer: AGENTS.md SSOT + dev/ 工作流(2026-05-02 首裝)
3. Current task belongs to which layer: 兩層皆活躍
4. Known layer-boundary risks: 治理為首裝,跨 session 套用效果待觀察

## Mandatory Start Checklist

1. Read `dev/SESSION_HANDOFF.md`
2. Read `dev/SESSION_LOG.md`
3. Read `dev/CODEBASE_CONTEXT.md` (if exists)
4. Read `dev/PROJECT_MASTER_SPEC.md` (if exists)
5. Confirm working tree / file status: `git status` 應 clean
6. Run baseline checks: 訪問 https://prompt-templates.github.io/Adam-AI-Instructions/ 確認 Pages 正常
7. Confirm environment / dependency state: Microlink API 仍可用(免費層 50 req/day/IP)
8. Confirm whether external platform alignment is required: 視任務內容
9. Search for related SSOT / spec / runbook before change: 治理規則查 AGENTS.md;內容查 prompts/<id>/
10. Search for duplicate rule / duplicate term / prior related fixes: grep 在 repo 內搜

## Open Priorities (max 5; one line per item)

1. 從 v0.1.0 tag 創建正式 GitHub Release 頁面
2. 準備第二份 Prompt(prompts/02-...)依現有結構建立
3. CODEBASE_CONTEXT.md 於下個 session 啟動時依 §1 規則自動生成,需補入 Microlink API External Services block

## Known Risks / Blockers (max 7 unresolved active risks)

1. Microlink API 免費層 50 req/day per IP,流量大時 og:image 回退至 SVG fallback
2. dev/init_backup/ 已 commit 至公開 repo;目前為空快照無敏感資料,但未來 install 需注意
3. 治理框架為首裝,§1-§13 各規則套用效果待後續 session 觀察
4. PROJECT_MASTER_SPEC suggestion issued: Claude_20260502_1637 2026-05-02(架構決策已立,符合長期維護條件;待用戶決定是否建立)

## Regression / Verification Notes

1. Required checks: GitHub Pages 站台可訪問;互動指南 Hero 三情境可切換;Facebook 卡片 og:image 載入或 fallback
2. Current failing checks: 無
3. Release / merge blocking conditions: §3c Phase 2 規定 release 須有 GitHub Release 頁,目前 v0.1.0 僅有 annotated tag

## Consolidation Watchlist

1. Rules currently duplicated across files: 治理首裝,無已知重複
2. Areas showing accretive drift: README ✅ 好處清單若日後加項,需檢查是否已被 7 大組規則導讀涵蓋
3. Candidate items for consolidation / retirement: 無

## Update Rule

This file and `dev/SESSION_LOG.md` must be updated at the end of every session.

If the session's changes affect behavior, acceptance criteria, specifications, runbooks, release conditions, or external platform integrations, query `dev/DOC_SYNC_CHECKLIST.md` (if it exists) for the complete scope of affected docs and update all listed entries.

If the session's fix involves adding a new rule, first check whether the existing definition should be integrated or outdated wording retired — avoid stacking without consolidating.

## Last Session Record (compact summary; details in SESSION_LOG)

1. UTC date: 2026-05-02
2. Session ID: Claude_20260502_1637
3. Completed: Hero 三情境互動 + Facebook og:image 動態載入 + governance 框架安裝 + README 好處清單迭代
4. Pending: GitHub Release 頁建立;第二份 Prompt 規劃
5. Next priorities (max 3): 見 Open Priorities
6. Risks / blockers: Microlink 免費層限制;治理首裝待跨 session 驗證
7. Files materially changed: prompts/01-.../guide.html;README.md;AGENTS.md(新);CLAUDE.md(新);GEMINI.md(新);dev/SESSION_HANDOFF.md(新);dev/SESSION_LOG.md(新);dev/DOC_SYNC_CHECKLIST.md(新)
8. Validation summary: working tree clean;origin/main HEAD = ff18056;Pages 已重建並驗證
9. Consolidation actions taken: Section 1 哲學基礎 SVG 與 Hero 情境 1 訊息重複 — 刪除 Section 1 SVG,改加 hyperlink 指向 Hero
