# Session Handoff

<!-- Compactness budget: Current Baseline max 6 lines; Open Priorities max 5; Known Risks max 7; keep details in SESSION_LOG. -->

## Current Baseline

1. Version: v0.1.0(annotated tag 已 push;GitHub Release 頁已建立);HEAD = a69f39b
2. Core features: 公開分享 Meta Instructions repo;首份 prompt(01-claude-cowork-meta-instruction)含原文 + 文字介紹 + 互動指南 HTML;語言分層規則已加入
3. Regression baseline: 互動指南 Hero 四情境(語言分層 / 全圖優先規則 / 回覆骨架 / 補丁式變更)；FPFR 五標題已改中文；working tree clean
4. Release / merge status: v0.1.0 tag 已 push;GitHub Release 頁待建
5. Active branch / environment: main(origin/main 同步;HEAD = a69f39b)
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
5. Read `dev/OPERATIONAL_RUNBOOK.md` (if exists) — 環境限制 + Tier 1/2/3 策略 + lock recovery + §5j 例外
6. Confirm working tree / file status: `git status` 應 clean
7. Run baseline checks: 訪問 https://prompt-templates.github.io/Adam-AI-Instructions/ 確認 Pages 正常
8. Confirm environment / dependency state: Microlink API 仍可用(免費層 50 req/day/IP)
9. Confirm whether external platform alignment is required: 視任務內容
10. Search for related SSOT / spec / runbook before change: 治理規則查 AGENTS.md;環境策略查 OPERATIONAL_RUNBOOK;內容查 prompts/<id>/
11. Search for duplicate rule / duplicate term / prior related fixes: grep 在 repo 內搜

## Open Priorities (max 5; one line per item)

1. guide.html 語言分層情境 4 在瀏覽器實測渲染（Pages deploy 後）
2. 規劃第二份 Prompt(prompts/02-...)依現有結構
3. 觀察新治理跨 session 套用（本 session 已再次確認正常）

## Known Risks / Blockers (max 7 unresolved active risks)

1. Microlink API 免費層 50 req/day per IP,流量大時 og:image 回退至 SVG fallback
2. dev/init_backup/ 已 commit 至公開 repo;目前為空快照無敏感資料,但未來 install 需注意
3. 治理框架(AGENTS + dev/ 五檔)套用效果待後續 session 觀察
4. PROJECT_MASTER_SPEC suggestion issued: Claude_20260502_1637 2026-05-02(架構決策已立,符合長期維護條件;待用戶決定是否建立)
5. §5j stale inode cache 例外屬首次記錄;再遇 VM stat 顯示 lock 但 Windows 已刪 → 直接 Tier 2 bypass,不再嘗試 VM 重試

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

1. UTC date: 2026-05-11
2. Session ID: Claude_20260511_0000
3. Completed: prompt.md 加語言分層規則(最高優先);FPFR 五標題改中文;Cowork 節 A-F → 一-六;【SSOT對齊】→【真源對齊】;【用語紀律】改書面語;guide.html 加情境 4 tab + 導讀 7→8 大組;README.md 加第零組 + 痛點表 + 安裝路徑修正;Tier 2 commit + push 成功(a69f39b)
4. Pending: GitHub Release 頁;情境 4 瀏覽器實測;第二份 Prompt 規劃
5. Next priorities (max 3): 見 Open Priorities
6. Risks / blockers: Microlink 免費層限制持續;v0.1.0 GitHub Release 頁仍缺
7. Files materially changed: prompts/01-claude-cowork-meta-instruction/prompt.md、guide.html、README.md
8. Validation summary: Tier 2 PowerShell commit + push 成功;origin/main HEAD = a69f39b;working tree clean
9. Fix Record: 無
10. Consolidation actions taken: 退役舊安裝路徑「Personal Preferences」(prompts/01/README.md);整合 SSOT/Patch-only 術語改為全中文表達
