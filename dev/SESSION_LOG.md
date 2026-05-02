# Session Log

<!-- Entry size cap: ≤110 lines per `## YYYY-MM-DD` block (incl. verbatim handoff); per §4 relocate detail to `dev/SESSION_STATE_DETAIL.md` or `docs/releases/<version>.md` if exceeded -->
<!-- Archive: per §4a, entries move to `dev/archive/SESSION_LOG_YYYY_QN.md` when file > 400 lines OR oldest entry > 30 days -->

## 2026-05-02

- **ID:** Claude_20260502_1711
- **Summary:** 治理首裝補齊(CODEBASE_CONTEXT + OPERATIONAL_RUNBOOK)+ 工作樹 CRLF/LF 根治 + Tier 2 Node.exe pattern 驗證落地(4 commits;working tree clean)
- **Changed:** dev/CODEBASE_CONTEXT.md(new 74 行)、dev/OPERATIONAL_RUNBOOK.md(new 618 行)、AGENTS.md(§1 加 #5)、README.md(Cowork 路徑修正 + 截圖 + 行尾正常化)、.gitattributes(new)、.gitignore(加 _*.txt)、doc/ui_settings_cowork.jpg(new)、dev/DOC_SYNC_CHECKLIST.md(加 2 row)
- **Done:** §1 強制 CODEBASE_CONTEXT.md 首裝(7 區段;Microlink External Services UNVERIFIED + Test-verified 雙標記);Cowork 路徑修正(Personal Preferences → Cowork → Global Instructions)+ 加截圖;吸納用戶上載 GENERIC_OPERATIONAL_RUNBOOK 為 dev/OPERATIONAL_RUNBOOK §1d 填本 repo 值 + §5j 新增 stale inode cache 例外 lesson(本 session 親自驗證);AGENTS.md §1 強制讀 4 → 5 條;.gitattributes 加 `* eol=lf` + binary 標記;`git add --renormalize` 處理 README 全檔行尾;.gitignore 加 `_*.txt`(per runbook §5i)
- **QC:** working tree 完全 clean(`## main...origin/main`,零 staged 零 untracked);4 commits 全部 push 成功(79ab094 / aa399f3 / 1f4d3c5 / 5a49f68);origin/main HEAD = 5a49f68;Tier 2 Node.exe pattern 驗證可靠(commit + push from Windows side bypass VM stale inode cache)
- **Pending:** v0.1.0 GitHub Release 頁;第二份 Prompt 規劃
- **Next:** 1) v0.1.0 GitHub Release 頁建立(§3c Phase 2 缺口) 2) 第二份 Prompt 規劃(prompts/02-...) 3) 觀察新治理(OPERATIONAL_RUNBOOK §1 read + .gitattributes)跨 session 套用
- **Risks:** Microlink free tier 50 req/day per IP;v0.1.0 Release 頁仍缺(§3c Phase 2);OPERATIONAL_RUNBOOK 列入 §1 強制讀為首次,跨 session 套用待觀察

### Fix Record

- **Problem:** VM `git commit` 持續失敗,顯示 "Unable to create '.git/index.lock': File exists",但 `find` / `ls` / `rm` 皆顯示檔案不存在(Linux sandbox 之前 git add 失敗時遺留嘅 ghost lock)
- **Root Cause:** Linux kernel inode/dentry cache 殘留陳舊 metadata,在 Windows 端 `Remove-Item .git\index.lock` 成功後仍長期(>5 分鐘)未失效,超出 OPERATIONAL_RUNBOOK §5g 預測嘅 10–60s sync window
- **Fix:** 跳過 VM,改用 Tier 2 MCP Node.exe pattern 從 Windows 側執行 `git commit -F <msg>` + `git push`(Windows process 無 stale cache)
- **Verification:** 4 個 commit 全部由 Tier 2 pattern 完成 + push 成功;working tree 最終清零

### Consolidation Record

- Merged: 無
- Retired: README.md 第 59 行舊路徑「Personal Preferences」(被「Cowork → Global Instructions」取代)
- Why: 舊路徑非實際介面位置,屬事實錯誤需修正

### DOC_SYNC Matrix Scan

| Change Category | Required Doc Updates | Status |
|---|---|---|
| Governance rule change(AGENTS.md §1 強制讀 +1 條) | INIT.md FILE 1 mirror;README if user-facing | N/A — 本 repo 無 INIT.md;§1 順序為內部治理,非 user-facing |
| External API / service change(Microlink 首次記錄) | CODEBASE_CONTEXT.md External Services block | ✓ Done — 本 session CODEBASE_CONTEXT.md 即包含 Microlink block,Doc-reviewed: UNVERIFIED + Test-verified: 2026-05-02 |
| New project doc added(CODEBASE_CONTEXT.md / OPERATIONAL_RUNBOOK.md) | DOC_SYNC_CHECKLIST.md 加 row | ✓ Row added — OPERATIONAL_RUNBOOK content + 政策檔 .gitattributes/.gitignore 兩 row |
| Repo-wide policy file changed(.gitattributes / .gitignore) | 政策檔本身;CODEBASE_CONTEXT.md Key Decisions;SESSION_LOG | ✓ Done — .gitattributes/.gitignore commit;CODEBASE_CONTEXT Key Decision 7 加;本 entry 述明 |

### Next Session Handoff Prompt (Verbatim)

```text
Read AGENTS.md first (governance SSOT), then follow its §1 startup sequence:
dev/SESSION_HANDOFF.md → dev/SESSION_LOG.md → dev/CODEBASE_CONTEXT.md (if exists) → dev/PROJECT_MASTER_SPEC.md (if exists) → dev/OPERATIONAL_RUNBOOK.md (if exists)

Current objective: 維護公開分享 Meta Instructions 的 GitHub repo;治理框架完整(AGENTS.md + dev/ 五檔);v0.1.0 已 tag 待補 Release 頁;working tree clean。

Pending priorities:
1. 建立 v0.1.0 GitHub Release 頁(§3c Phase 2 缺口)
2. 規劃第二份 Prompt(prompts/02-...)依現有結構
3. 觀察新治理(OPERATIONAL_RUNBOOK §1 read + .gitattributes)跨 session 套用

Key files changed this session:
- dev/CODEBASE_CONTEXT.md(new 74 行)
- dev/OPERATIONAL_RUNBOOK.md(new 618 行;§5j stale inode cache lesson)
- AGENTS.md(§1 加 #5);README.md(Cowork 路徑 + 截圖 + 行尾)
- .gitattributes(new);.gitignore(_*.txt);doc/ui_settings_cowork.jpg(new)
- Additional files: see SESSION_LOG Changed

Known risks/cautions:
- Microlink free tier 50 req/day per IP
- v0.1.0 已 tag 但 Release 頁仍缺(§3c Phase 2)
- §5j stale inode cache 例外:VM stat 顯示 lock 仍在但 Windows 已刪 → Tier 2 bypass

Validation status: working tree clean;origin/main HEAD = 5a49f68;4 commits pushed
Post-startup first action: 揀優先 — GitHub Release 頁 vs 02 Prompt
```

---

## 2026-05-02

- **ID:** Claude_20260502_1637
- **Summary:** 互動指南 Hero 三情境互動改造 + Facebook og:image 動態載入 + 治理框架首裝 + README 好處清單迭代(內容層 + 治理層雙活躍)
- **Changed:** prompts/01-claude-cowork-meta-instruction/guide.html、README.md、AGENTS.md(new)、CLAUDE.md(new)、GEMINI.md(new)、dev/SESSION_HANDOFF.md(new)、dev/SESSION_LOG.md(new)、dev/DOC_SYNC_CHECKLIST.md(new)
- **Done:** Hero 三標籤互動情境(FPFR / 回覆骨架 / Patch 變更);FPFR AFTER 改用真實 5 區段 markdown 結構(### 編號標題 + 表格 + 列表 + 收尾框);回覆骨架加入「下一步揀一條」A/B/C + 推薦;Patch 標籤名由「補丁式變更」改為「Patch 變更」;Facebook 卡片改為全寬 link preview(72×72 圓形相片)並用 Microlink API 動態載入個人檔案 og:image,失敗則 SVG fallback;Section 1 哲學基礎刪除重複 SVG,改加 hyperlink 指向 Hero 情境 1;README 痛點清單改寫為 6 條 ✅ 套用後好處,FPFR 條目用英文規則名 + 5 點編號;治理框架首裝 7 個檔案(§5a 雙階段確認流程通過 INSTALL_ROOT_OK + INSTALL_WRITE_OK)
- **QC:** Chrome MCP 實地驗證 Hero 三情境桌面渲染通過;手機 viewport(force 380px)響應式正常;Facebook 卡片 og:image 載入成功(秋天森林相片);每次 commit 後自行驗證;working tree clean;origin/main HEAD 與本機一致(ff18056)
- **Pending:** v0.1.0 GitHub Release 頁從 tag 建立;第二份 Prompt(prompts/02-...)規劃;CODEBASE_CONTEXT.md 將於下個 session 啟動時自動生成,需在生成時補入 Microlink API External Services block
- **Next:** 1) 從 v0.1.0 tag 創建 GitHub Release 頁面 2) 準備第二份 Prompt 3) 下個 session 啟動時生成 CODEBASE_CONTEXT.md 並記錄 Microlink API
- **Risks:** Microlink API 免費層 50 req/day per IP,流量大時 og:image 回退至 SVG;治理框架首裝,跨 session 套用效果待觀察;§3c Phase 2 規定 release 須有 GitHub Release 頁,目前 v0.1.0 缺

### Consolidation Record

- Merged: 無
- Retired: Section 1 哲學基礎內「合作模式對比 SVG」(因與 Hero 情境 1 訊息重複)
- Why: 防漂移 — 同一概念兩處視覺化造成讀者重複閱讀;Hero 互動版本更具體更生動,Section 1 改用文字 + hyperlink 指回 Hero

### DOC_SYNC Matrix Scan

| Change Category | Required Doc Updates | Status |
|---|---|---|
| External API / service change(本 session 加入 Microlink API client-side 呼叫) | CODEBASE_CONTEXT.md External Services block | ⚠ Skipped(CODEBASE_CONTEXT.md 尚未存在;將於下個 session 啟動時依 §1 自動生成,屆時須補 Microlink block) |

### Next Session Handoff Prompt (Verbatim)

```text
Read AGENTS.md first (governance SSOT), then follow its §1 startup sequence:
dev/SESSION_HANDOFF.md → dev/SESSION_LOG.md → dev/CODEBASE_CONTEXT.md (if exists) → dev/PROJECT_MASTER_SPEC.md (if exists)

Current objective: 維護公開分享 Meta Instructions 的 GitHub repo;首份 prompt v0.1.0 已發佈;互動指南 + 治理框架皆就緒。

Pending priorities:
1. 從 v0.1.0 tag 創建正式 GitHub Release 頁面
2. 準備第二份 Prompt(prompts/02-...)依現有結構
3. CODEBASE_CONTEXT.md 於下個 session 啟動時自動生成,需補入 Microlink API External Services block

Key files changed this session:
- prompts/01-claude-cowork-meta-instruction/guide.html(Hero 三情境互動 + Facebook og:image)
- README.md(套用後好處 6 條清單,含 FPFR 顯眼條目)
- AGENTS.md / CLAUDE.md / GEMINI.md(治理 SSOT 與橋接)
- dev/SESSION_HANDOFF.md / SESSION_LOG.md / DOC_SYNC_CHECKLIST.md(治理工作流)

Known risks/cautions:
- Microlink API 免費層 50 req/day per IP,流量大時 og:image 回退 SVG
- v0.1.0 已 tag 但 GitHub Release 頁尚未建立(§3c Phase 2 缺)

Validation status: working tree clean;origin/main HEAD = ff18056;Pages 已驗證
Post-startup first action: 確認 GitHub Pages 站台正常,並決定優先處理 GitHub Release 還是第二份 Prompt
```
