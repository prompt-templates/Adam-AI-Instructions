# Codebase Context

<!-- Stable project facts; update only when stack / External Services / Key Decisions change. -->
<!-- Lean version — 本 repo 為 docs/prompts 分享庫,非軟件項目;Stack / Build & Run 區段刻意精簡。 -->

## Stack

- 內容載體:Markdown(README、prompt 原文)+ HTML(互動指南,單檔內嵌 CSS / JS)
- 託管:GitHub Pages(GitHub-hosted,自動由 main 分支發佈)
- 外部依賴(client-side):Microlink API(動態載入 Facebook 連結預覽 og:image)
- 無建置工具鏈、無套件管理(non-Node、non-Python),純靜態檔案

## Directory Map

```
Adam-AI-Instructions/
├── README.md                                   ← 入口頁,Prompt 索引
├── AGENTS.md / CLAUDE.md / GEMINI.md           ← 治理 SSOT 與橋接
├── CHANGELOG.md
├── LICENSE
├── doc/                                        ← 截圖等輔助素材
├── dev/                                        ← 治理工作流檔案(本資料夾)
│   ├── SESSION_HANDOFF.md
│   ├── SESSION_LOG.md
│   ├── DOC_SYNC_CHECKLIST.md
│   ├── CODEBASE_CONTEXT.md                     ← 本檔
│   └── init_backup/                            ← §5a 首裝快照
└── prompts/
    └── 01-claude-cowork-meta-instruction/
        ├── README.md                           ← 該指令文字介紹
        ├── prompt.md                           ← 可直接複製套用的原文
        └── guide.html                          ← 互動式指南
```

## Key Entry Points

- 公眾入口:`README.md` → `## 五、Prompt 索引` 表格
- Pages 站台:`https://prompt-templates.github.io/Adam-AI-Instructions/`
- 互動指南:`prompts/01-claude-cowork-meta-instruction/guide.html`
- 治理規則 SSOT:`AGENTS.md`(`CLAUDE.md` / `GEMINI.md` 為單行橋接)

## Build & Run

- 無建置步驟。任何 `.md` / `.html` 改動 push 至 `main` 後,GitHub Pages 自動重建並發佈
- 本機預覽:用瀏覽器直接開 `prompts/<id>/guide.html`(file:// 協定可運行,Microlink API 仍可呼叫)

## External Services

### Microlink API

- Base URL: `https://api.microlink.io/`
- Version: 公開 free tier(無顯式 version path;以 root endpoint 配 query param 為主)
- Auth: 無(free tier 公開存取;產品有 paid tier 可用 API key,本 repo 未用)
- Required params: `url`(URL-encoded 目標頁面;呼叫處見 `prompts/01-claude-cowork-meta-instruction/guide.html` 第 1450–1471 行)
- Forbidden params: NA — 本 repo 只用 root endpoint + `url` 參數,其他參數未啟用
- Response path: `data.image.url`(主要)或 `data.logo.url`(備援);兩者皆缺則保留 SVG fallback
- Official docs: `https://microlink.io/docs/api/getting-started/overview`
- Doc-reviewed: UNVERIFIED(本 session 由現有 guide.html 反推記錄,未直接核對官方文檔)
- Test-verified: 2026-05-02(Claude_20260502_1637 — 上 session 實測 Facebook 卡片 og:image 載入成功)
- Notes: 免費層 50 req/day per IP;超出時 fetch 失敗,前端靜默 catch 並維持 SVG fallback。日後若改 API 呼叫代碼,須先重新核對官方文檔並更新 Doc-reviewed。

## Key Decisions

1. **治理框架首裝(2026-05-02)**:採 AGENTS.md 為 SSOT,CLAUDE.md / GEMINI.md 單行橋接;dev/ 工作流負責 session handoff 與防漂移。背景:跨 session 維護同步需治理基線,§5a 雙確認流程通過後落地。
2. **prompts/ 目錄結構**:每份指令獨立資料夾,固定三檔(`README.md` 文字介紹、`prompt.md` 可複製原文、`guide.html` 互動指南)。第二份 prompt 沿用此結構。
3. **互動指南設計**:Hero 區用三情境 tab(FPFR / 回覆骨架 / Patch 變更)展示套用前後對比;單檔內嵌 CSS / JS,無外部 framework 依賴。
4. **og:image 動態策略**:Facebook 卡片用 Microlink API client-side 抓 og:image;失敗則靜默回退 SVG,不阻塞頁面渲染。免費層流量風險記於 §3c 監控清單。
5. **Release 條件**:annotated tag + GitHub Release 頁兩者皆需備齊(§3c Phase 2);v0.1.0 已 tag 但 Release 頁仍缺,屬 Open Priority。
6. **環境限制 SSOT(2026-05-02)**:`dev/OPERATIONAL_RUNBOOK.md` 列入 AGENTS.md §1 強制讀 #5,涵蓋 Tier 1/2/3 執行策略、Cross-VM permission boundary、git lock recovery、FUSE sync delay、§5j stale inode cache 例外。所有 agent(Claude / Codex / Gemini)session start 自動讀。
7. **行尾政策(2026-05-02)**:`.gitattributes` 設 `* text=auto eol=lf`,LF 強制統一(stored + working tree);binary 檔案明確標記;Tier 2/3 temp 輸出 `_*.txt` 列入 `.gitignore`(per runbook §5i)。

## AI Maintenance Log

| Session ID | UTC Date | Action |
|---|---|---|
| Claude_20260502_1711 | 2026-05-02 | 首次生成本檔(§1 規則),反推 Microlink API 至 External Services(Doc-reviewed: UNVERIFIED, Test-verified: 2026-05-02)。同 session 後續加 Key Decision 6(OPERATIONAL_RUNBOOK 列入 §1 強制讀)+ Key Decision 7(.gitattributes LF 政策 + .gitignore _*.txt)。 |
