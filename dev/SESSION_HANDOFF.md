# Session Handoff

<!-- Compactness budget: Current Baseline max 6 lines; Open Priorities max 5; Known Risks max 7; keep details in SESSION_LOG. -->

## Current Baseline

1. Version: v0.1.0(annotated tag 已 push;GitHub Release 頁尚未建)
2. Core features: 公開分享 Meta Instructions repo;首份 prompt(01-claude-cowork-meta-instruction)含原文 + 文字介紹 + 互動指南 HTML
3. Regression baseline: 互動指南 Hero 三情境(FPFR / 回覆骨架 / Patch)桌面與手機渲染通過實測;working tree clean
4. Release / merge status: v0.1.0 tag 已 push;GitHub Release 頁待建
5. Active branch / environment: main(origin/main 同步;HEAD = 5a49f68)
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

1. 建立 v0.1.0 GitHub Release 頁(§3c Phase 2 缺口;tag cd4621e 已 push)
2. 規劃第二份 Prompt(prompts/02-...)依現有結構
3. 觀察新治理(OPERATIONAL_RUNBOOK §1 強制讀 + .gitattributes LF 政策)跨 session 套用

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

1. UTC date: 2026-05-02
2. Session ID: Claude_20260502_1711
3. Completed: §1 強制 CODEBASE_CONTEXT.md 首裝(7 區段含 Microlink External Services);Cowork 設定路徑修正(Personal Preferences → Cowork → Global Instructions)+ 加截圖;吸納用戶上載 runbook 為 dev/OPERATIONAL_RUNBOOK.md(618 行,§5j 新加 stale inode cache 例外);AGENTS.md §1 強制讀 4 → 5 條;.gitattributes LF 政策落地;.gitignore 加 _*.txt(per runbook §5i);git add --renormalize 處理 README 全檔行尾
4. Pending: GitHub Release 頁;第二份 Prompt 規劃
5. Next priorities (max 3): 見 Open Priorities
6. Risks / blockers: Microlink 免費層限制;新治理跨 session 套用待觀察;§5j 例外首次記錄
7. Files materially changed: dev/CODEBASE_CONTEXT.md(new);dev/OPERATIONAL_RUNBOOK.md(new);AGENTS.md;README.md;.gitattributes(new);.gitignore;doc/ui_settings_cowork.jpg(new);dev/DOC_SYNC_CHECKLIST.md
8. Validation summary: working tree fully clean(零 staged 零 untracked);4 commits push 成功(79ab094 / aa399f3 / 1f4d3c5 / 5a49f68);origin/main HEAD = 5a49f68;Tier 2 Node.exe pattern 經本 session 多次驗證可靠
9. Fix Record: VM `git commit` 因 stale inode cache 持續失敗 → §5j 記錄 + 改用 Tier 2 從 Windows 側執行,4 commit 全部成功
10. Consolidation actions taken: 移除 README.md 第 59 行舊路徑「Personal Preferences」(換為實際介面位置「Cowork → Global Instructions」)
