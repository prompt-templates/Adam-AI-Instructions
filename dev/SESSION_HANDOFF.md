# Session Handoff

<!-- Compactness budget: Current Baseline max 6 lines; Open Priorities max 5; Known Risks max 7; keep details in SESSION_LOG. -->

## Current Baseline

1. Version: v0.2.0(annotated tag 已 push;GitHub Release 頁已建立 + marked latest);HEAD = 7e370f4
2. Core features: 公開分享 Meta Instructions repo;首份 prompt(01-claude-cowork-meta-instruction)v0.2.0 含審計變更說明條款 + Cowork 補充 11A/11B/11C 三條反偷懶紅線
3. Regression baseline: working tree clean(剩 NEXT_SESSION_PROMPT.txt untracked);CHANGELOG / 主 README / docs/releases/v0.2.0.md 三檔同步反映 v0.2.0
4. Release / merge status: v0.2.0 完整發佈(tag + Release page + release notes 內部連結絕對 URL polish 已 7e370f4)
5. Active branch / environment: main(origin/main 同步;HEAD = 7e370f4)
6. External platforms in scope: GitHub Pages、Microlink API、GitHub Releases

## Layer Map

1. Product / System Layer: 公開分享 prompts 內容;GitHub Pages 靜態站;GitHub Releases 對外版本對話
2. Development Governance Layer: AGENTS.md SSOT + dev/ 工作流(2026-05-02 首裝;2026-05-12 完整 closeout 自動觸發本次由用戶反問才補)
3. Current task belongs to which layer: 兩層皆活躍
4. Known layer-boundary risks: 新規則(v0.2.0)跨 session 套用效果待觀察;AGENTS.md §4 closeout 觸發機制本 session 漏做暴露起手讀序未涵蓋治理 SSOT

## Mandatory Start Checklist

1. Read `dev/SESSION_HANDOFF.md`
2. Read `dev/SESSION_LOG.md`
3. Read `dev/CODEBASE_CONTEXT.md` (if exists)
4. Read `dev/PROJECT_MASTER_SPEC.md` (if exists)
5. Read `dev/OPERATIONAL_RUNBOOK.md` (if exists) — 環境限制 + Tier 1/2/3 策略 + lock recovery + §5j 例外
6. Read `AGENTS.md` (§1 startup sequence + §4 closeout 觸發詞)
7. Confirm working tree / file status: `git status` 應 clean(或只剩 NEXT_SESSION_PROMPT.txt untracked)
8. Run baseline checks: 訪問 https://prompt-templates.github.io/Adam-AI-Instructions/ 確認 Pages 正常
9. Confirm environment / dependency state: Microlink API 仍可用(免費層 50 req/day/IP);Windows MCP 工具(PowerShell + FileSystem)為動 git/gh/檔案刪除的首選
10. Confirm whether external platform alignment is required: 視任務內容
11. Search for related SSOT / spec / runbook before change: 治理規則查 AGENTS.md;環境策略查 OPERATIONAL_RUNBOOK;內容查 prompts/<id>/

## Open Priorities (max 5; one line per item)

1. 規劃第二份 Prompt(prompts/02-...)依現有結構
2. Pages deploy 後在瀏覽器實測 guide.html 情境 4(語言分層 tab)渲染
3. 觀察 v0.2.0 三條紅線 + 審計變更說明條款跨 session 套用效果
4. 新規則若再有改動必同步 CHANGELOG + 主 README 最近更新 + docs/releases/

## Known Risks / Blockers (max 7 unresolved active risks)

1. Microlink API 免費層 50 req/day per IP,流量大時 og:image 回退至 SVG fallback
2. v0.2.0 新規則跨 session 套用效果待觀察(尤其「審計變更說明」是否真能令推薦穩定)
3. AGENTS.md §4 closeout 本 session 由用戶反問才補做;session 起手讀序未含 AGENTS.md 是教訓,下次必先讀
4. dev/init_backup/ 已 commit 至公開 repo;目前為空快照無敏感資料,但未來 install 需注意
5. §5j stale inode cache 例外:再遇 VM stat 顯示 lock 但 Windows 已刪 → 直接 Tier 2 bypass,不再嘗試 VM 重試

## Regression / Verification Notes

1. Required checks: GitHub Pages 站台可訪問;互動指南 Hero 四情境可切換;v0.2.0 Release 頁絕對 URL 連結可點
2. Current failing checks: 無
3. Release / merge blocking conditions: 已過(§3c Phase 2 GitHub Release 頁要求,v0.2.0 已完成)

## Consolidation Watchlist

1. Rules currently duplicated across files: prompt.md(repo) vs cowork session local 副本 — session local 會於下次 session 自動同步,無 manual sync 風險
2. Areas showing accretive drift: README「最近更新」表格將持續增長,日後 >5 條需考慮分頁或只顯示最近
3. Candidate items for consolidation / retirement: 無

## Update Rule

This file and `dev/SESSION_LOG.md` must be updated at the end of every session.

If the session's changes affect behavior, acceptance criteria, specifications, runbooks, release conditions, or external platform integrations, query `dev/DOC_SYNC_CHECKLIST.md` (if it exists) for the complete scope of affected docs and update all listed entries.

If the session's fix involves adding a new rule, first check whether the existing definition should be integrated or outdated wording retired — avoid stacking without consolidating.

## Last Session Record (compact summary; details in SESSION_LOG)

1. UTC date: 2026-05-12
2. Session ID: Claude_20260512_0500
3. Completed: v0.2.0 規則加固落地(prompt.md +5 行:審計變更說明 + Cowork 11A/11B/11C);CHANGELOG +v0.2.0 條目;主 README +「最近更新」區塊;新建 docs/releases/v0.2.0.md;commit a2d12a0 + push;v0.2.0 annotated tag + GitHub Release 頁(gh release create --latest);release notes 連結改絕對 URL(commit 7e370f4 + gh release edit);還原 4 個損壞 working tree 檔案;載入 Windows-MCP 工具;memory feedback_windows_mcp_first.md 寫入;補做本次 closeout
4. Pending: 第二份 Prompt 規劃;情境 4 瀏覽器實測;新規則跨 session 套用觀察
5. Next priorities (max 3): 見 Open Priorities
6. Risks / blockers: 新規則跨 session 待觀察;closeout 漏做暴露起手讀序未涵蓋 AGENTS.md
7. Files materially changed: prompts/01-claude-cowork-meta-instruction/prompt.md、CHANGELOG.md、README.md、docs/releases/v0.2.0.md(new)
8. Validation summary: HEAD = 7e370f4;working tree clean(剩 NEXT_SESSION_PROMPT.txt untracked);GitHub Release published + marked latest;gh release view v0.2.0 內容核對通過
9. Fix Record: 前半段誤用 sandbox bash agent 操作 Windows-side filesystem,被 9p mount + .git/index.lock 反覆碰壁;載入 mcp__Windows-MCP__PowerShell + FileSystem 後 5 分鐘搞掂剩餘 git/gh/還原工作
10. Consolidation actions taken: 新增 prompt.md 4 條規則(第 108、200-202 行);無退役;docs/releases/v0.2.0.md 與 GitHub Release body 同源(絕對 URL)
