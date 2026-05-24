# Adam's AI Instructions｜AI 治理指令庫

個人於日常使用 AI 工具(Claude Cowork、Claude Code、ChatGPT 等)過程中累積的治理指令(Meta Instructions)集合。

---

## 一、本資料庫內容

收錄個人於實際操作中,經反覆遇到問題與修正後沉澱出的 Meta Instruction 文本。每一份指令對應一類具體場景,用於約束 AI 在該場景下的行為,以提升輸出的一致性、可驗收性與可審計性。

套用後可獲得的具體好處:

- ✅ 偏好優先序:事實可驗收 > 穩定性 > 根因治理 > 完整性交付 > 最小改動
- ✅ AI 主動判斷並一次提交完整方案,減少反覆提問
- ✅ 動手修改前先輸出完整執行計劃（全圖優先規則）：(1) 終點畫面、(2) 交付物、(3) 可量指標、(4) 驗收測試、(5) 目標連結，五區段一頁見全，收尾以「若不否決或修改，即開始執行」讓用戶 30 秒可決定批准、否決或修改
- ✅ 核對不到的部分清楚區分為「未核實」（曾嘗試核對但失敗）與「未適用」（真缺值或無資料），不會混淆已驗證與未驗證內容
- ✅ 修改以「精準錨點 + 修改前 / 修改後 + 變更日誌」補丁式交付，方便直接貼換，合併零遺漏
- ✅ 同一規則只在單一定義塊存在，減少指令四散、出現自相矛盾（防漂移）
- ✅ 判斷事實前必先核對（先讀後判）；用驗證代替推斷、用全貌代替片段，杜絕憑記憶猜測外部平台或檔案內容
- ✅ 治理改動先審核：修改治理規則、跨檔同步、刪除重命名等不可逆操作前必先計劃自檢與只讀審核，不預設一定修改檔案
- ✅ 創作類任務（設計、故事、詩、廣告文案、虛構等）自動豁免事實可驗收硬骨幹，保留語言分層與合作模式

每條規則均對應一次或多次實際發生的情況及修正方法。內容定位為個人經驗紀錄與分享,並非標準或最佳實踐宣稱。

---

## 二、適用對象

- 長期使用 Claude Cowork、Claude Code、ChatGPT 等 LLM 對話型工具的用戶。
- 涉及多檔案修改、長期文件維護、規則治理的用戶。
- 希望 AI 在多步驟任務中減少反覆確認、提升自主判斷的用戶。
- 重視輸出格式一致性與可驗收性的用戶。
- 非技術背景的用戶亦可使用:每份指令皆附中文介紹頁,以場景與行為描述為主,不要求程式背景。

---

## 三、目錄結構

```
Adam-AI-Instructions/
├── README.md                                   ← 本頁（總索引）
├── CHANGELOG.md                                ← 完整變更日誌
├── AGENTS.md                                   ← Claude Code / OpenAI Codex / Amp / Cursor 等 AGENTS.md 標準 agent 直接讀取的設定檔
├── LICENSE
│
├── prompts/                                    ← 各份 Meta Instruction 指令
│   ├── 01-claude-cowork-meta-instruction/      ← Claude Cowork / Codex / AGENTS.md 通用版（v0.7.0 — 12-節結構整合版）
│   │   ├── prompt.md                           ← Prompt 原文，可直接複製貼至 AI 工具
│   │   ├── README.md                           ← 該指令的文字介紹頁
│   │   └── guide.html                          ← 互動式 SVG 指南（GitHub Pages 可開啟）
│   │
│   └── 02-claude-code-meta-instruction/        ← Claude Code 場景特化版（第一至十二節與 01 同源 + 第十三節機密處理 + 第十四節 Windows 桌面附加 + 第十五節 Claude Code 場景工作流）
│       ├── prompt.md
│       ├── README.md
│       └── guide.html
│
└── docs/
    ├── releases/                               ← 各版本用戶面向發布說明
    │   ├── v0.7.3.md
    │   ├── v0.7.2.md
    │   ├── v0.7.1.md
    │   ├── v0.7.0.md
    │   └── ...（v0.2.0 起累積）
    │
    └── experiments/                            ← 治理改動數據驗證實驗報告
        └── 2026-05-23-pruning-experiment/      ← v0.7.0 12-節結構整合版的瘦身實驗
            ├── README.md                       ← 實驗主頁（一句結論 + 為何 B 勝出）
            ├── test_cases.md                   ← 8 場景 × 37 條規則檢查點
            ├── evaluation_matrix.md            ← 三版本 × 四輪評分矩陣
            ├── comparison_report.md            ← 多維對照 + 勝出宣告
            └── v_a/v_b/v_c_*.md                ← A 保守 / B 中度 / C 激進 三版本 prompt 全文
```

每份指令獨立存放於各自資料夾，內含三件套：

- `prompt.md`：Prompt 原文，可直接複製貼至 AI 工具的 system prompt、personal preferences、project instructions 等欄位。
- `README.md`：文字介紹頁，說明該指令對應的痛點、規則內容、治理作用、適用情景。
- `guide.html`：互動式指南，含 SVG 視覺化說明，以瀏覽器開啟即可閱讀（亦可由 GitHub Pages 線上預覽）。

## 四、使用方式

1. 從下文索引選取適用於自身工具的指令。
2. 閱讀該指令的 `README.md`,理解規則內容與適用情景。
3. 開啟 `prompt.md`,複製全文。
4. 貼至所用 AI 工具的對應位置(下方逐工具列出步驟):

   **Claude Cowork**

   Settings → Cowork → Global Instructions(介面位置見下圖)。將複製的內容貼入該欄位,儲存即生效。

   ![Claude Cowork 設定介面 — Settings → Cowork → Global Instructions 欄位位置](doc/ui_settings_cowork.jpg)

   **Claude Code**(全平台)

   - 全域(套用至所有項目):
     - macOS / Linux:於個人資料夾下的 `.claude` 資料夾內,新建檔案 `CLAUDE.md`(完整路徑 `~/.claude/CLAUDE.md`)。
     - Windows:於 `C:\Users\<你的用戶名稱>\.claude\` 內新建檔案 `CLAUDE.md`。
   - 單一項目:於該項目根目錄新建檔案 `CLAUDE.md`,只影響該項目。
   - 將複製的 prompt 全文貼入該檔案,儲存後重新開啟 Claude Code 即生效。
   - 如資料夾或檔案不存在,自行新建即可。

   **OpenAI Codex**

   - 全域(套用至所有項目):
     - macOS / Linux:於個人資料夾下的 `.codex` 資料夾內,新建檔案 `AGENTS.md`(完整路徑 `~/.codex/AGENTS.md`)。
     - Windows:於 `C:\Users\<你的用戶名稱>\.codex\` 內新建檔案 `AGENTS.md`。
   - 單一項目:於該項目根目錄新建檔案 `AGENTS.md`,只影響該項目。
   - 將複製的 prompt 全文貼入該檔案,儲存後重新開啟 Codex 即生效。
   - 如資料夾或檔案不存在,自行新建即可。

   **其他 AGENTS.md 標準 agent**(Amp / Cursor / Factory / Google Jules 等)

   - 單一項目:於該項目根目錄新建檔案 `AGENTS.md`,將 prompt 全文貼入。AGENTS.md 為跨工具通用格式。
   - 全域:每個工具有自己的全域檔案位置,請參考各自的官方文件。

   **ChatGPT 或其他 LLM 對話介面**

   Settings → Personalization → Custom Instructions(或對應的「自訂指令」欄位),將 prompt 全文貼入儲存即生效。

5. 套用後觀察 AI 行為變化;若某條規則與個人習慣衝突,可自行刪改。

> **進階提示**(熟悉終端機的用戶可選看)
>
> - 已設定 `CLAUDE_CONFIG_DIR`(Claude Code)或 `CODEX_HOME`(OpenAI Codex)環境變數的用戶,安裝位置會隨環境變數指向的資料夾改變,以該位置為準。
> - OpenAI Codex 同時支援 `AGENTS.override.md`(優先於 `AGENTS.md`)作為覆寫檔。如你已有 `AGENTS.md` 而不想覆蓋,可改貼至 `AGENTS.override.md`。

各指令的規則段落可獨立使用,毋須整套套用。

---

> ## 🏆 最新：v0.7.0 — 12-節結構整合版
>
> 📊 經 8 場景 × 37 條規則檢查點實測勝出　·　規則覆蓋率 **100%**　·　字數 **−45%**　·　綜合分較 v0.6.1 提升 **15.5%**
>
> 🧪 [實驗報告（含三檔策略對比、評分矩陣、勝出依據）](docs/experiments/2026-05-23-pruning-experiment/)
>
> 👉 **直接使用**：[Cowork / Codex / AGENTS.md 通用版（prompt 01）](prompts/01-claude-cowork-meta-instruction/prompt.md)　·　[Claude Code 場景特化版（prompt 02，含機密處理 + Windows 桌面附加）](prompts/02-claude-code-meta-instruction/prompt.md)

---

## 五、Prompt 索引

| # | 名稱 | 互動指南 | 文字介紹 | Prompt 原文 | 適用工具 |
|---|------|---------|---------|-------------|----------|
| 01 | Claude Cowork Meta Instruction | [guide.html](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/01-claude-cowork-meta-instruction/guide.html) | [README.md](prompts/01-claude-cowork-meta-instruction/README.md) | [prompt.md](prompts/01-claude-cowork-meta-instruction/prompt.md) | Claude Cowork、Claude Code、OpenAI Codex、AGENTS.md 標準 agent(Amp / Cursor / Factory / Google Jules)、一般 Claude / ChatGPT 對話介面 |
| 02 | Claude Code Meta Instruction(含機密處理及 Windows 桌面附加) | [guide.html](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.html) | [README.md](prompts/02-claude-code-meta-instruction/README.md) | [prompt.md](prompts/02-claude-code-meta-instruction/prompt.md) | Claude Code(全平台);亦適用 OpenAI Codex / AGENTS.md 標準 agent;第十四節 Windows 桌面附加為條件式生效,macOS / Linux 自動跳過 |

> **建議閱讀順序**:先點擊「互動指南」(以瀏覽器開啟,含 SVG 視覺化說明),再參考「文字介紹」深入細節,最後複製「Prompt 原文」套用至所用 AI 工具。
>
> **01 vs 02 怎麼選**:純對話介面或 Cowork 為主用 01;Claude Code 為主、會接觸 `.env` / credentials 或在 Windows 桌面操作 shell 命令用 02。02 第一至十二節與 01 同源逐字，尾部新增第十三節機密處理 + 第十四節 Windows 桌面附加 + 第十五節 Claude Code 場景工作流共三節。

未來將陸續加入其他工具與場景的指令版本。

---

## 六、最近更新

本資料庫採用版本制管理重要變更。下方列出最近 5 次更新(按時間倒序);完整變更日誌見 [CHANGELOG.md](CHANGELOG.md),各版本詳細用戶面向發布說明見 [docs/releases/](docs/releases/)。

| 版本 | 日期 | 主要變更 |
|------|------|---------|
| [v0.8.0](docs/releases/v0.8.0.md) | 2026-05-24 | **Claude Code 場景特化升級**：prompt 02 新增第十五節「Claude Code 場景工作流」，整合 Anthropic 2026 官方 best practices 嘅 5 項實操（Plan mode 觸發／主動提驗收／Context 管理／CLI 優先／Subagent for investigation）+ 5 項失敗模式警示；保留 v0.7.0 12-節通用基礎，不重組既有 14 節 |
| [v0.7.3](docs/releases/v0.7.3.md) | 2026-05-23 | root README 全面對齊：第一節五區段名／中文措辭 + 加 3 條核心好處；第三節目錄樹完整重寫含 prompt 02、guide.html、docs/、CHANGELOG、AGENTS.md；第五節節號同步；移除多餘 horizontal rule |
| [v0.7.2](docs/releases/v0.7.2.md) | 2026-05-23 | 一般讀者導讀升級：root README 加 🏆 spotlight box 突出 v0.7.0 勝出地位 + 第六節 v0.7.0 行加 🏆 標；experiment 報告加 🏆 一句結論卡 + 各節功能性 emoji 視覺定位 + 排名 🏆🥈🥉 + ⭐ 標 B 中度行 |
| [v0.7.1](docs/releases/v0.7.1.md) | 2026-05-23 | Hotfix：root README 第五節 02 行節號同步 + prompts/02/guide.html 約 15 處節號重編 + prompts/01/guide.html 加結構更新 banner + 勝出版本正式命名「v0.7.0 — 12-節結構整合版」（簡稱 12-節結構整合版）|
| 🏆 [v0.7.0](docs/releases/v0.7.0.md) | 2026-05-23 | **v0.7.0 — 12-節結構整合版**　Meta Instruction 中度瘦身：20 節 → 12 節（字數 -45%），規則覆蓋率 100%，綜合分較 v0.6.1 提升 15.5%；首次配套發佈完整實驗報告（[docs/experiments/2026-05-23-pruning-experiment/](docs/experiments/2026-05-23-pruning-experiment/)）|
| [v0.6.1](docs/releases/v0.6.1.md) | 2026-05-17 | 改善 root README 第四節 + 02 README 第五節安裝指引:Claude Code / Codex / 其他 AGENTS.md agent 改用步驟化、非技術讀者友善的書面語版本;補上「確認是否生效」段同進階提示 |
| [v0.6.0](docs/releases/v0.6.0.md) | 2026-05-17 | 新增 prompt 02:Claude Code Meta Instruction(含機密處理及 Windows 桌面附加);第一至二十節與 01 同源逐字,新增第二十一節機密處理 + 第二十二節 Windows 桌面破壞性命令零容忍 |
| [v0.5.1](docs/releases/v0.5.1.md) | 2026-05-16 | Hotfix:修正主標題仍 hardcode "Cowork" 同跨工具通用聲明矛盾;主標題 retitle + Cowork Project 用詞 generic + prompts/01 README 第七組描述 sync |
| [v0.5.0](docs/releases/v0.5.0.md) | 2026-05-15 | 加「創作類任務例外」豁免、條款編號 + 回覆骨架執行硬規則、選擇題分行修正、明文兼容 OpenAI Codex / AGENTS.md 標準 agent;緊湊化 296→248 行 |
| [v0.4.0](docs/releases/v0.4.0.md) | 2026-05-15 | 結構升級為標準 Markdown 階層,新增「先讀後判」「治理改動先審核」兩條上位核心規則 |
| [v0.3.0](docs/releases/v0.3.0.md) | 2026-05-13 | 加固「治理層計劃自檢」「強制只讀審核」與「禁把看似可執行當已審核」規則 |
| [v0.2.0](docs/releases/v0.2.0.md) | 2026-05-11 | 加固「審計後推薦穩定性」與「禁 quick fix／必查 sessionlog／禁憑記憶」規則 |
| v0.1.0 | 2026-05-02 | 初次公開發佈,首份 Claude Cowork Meta Instruction |

---

## 七、授權與貢獻

- **授權**:本資料庫內容供任何用戶免費使用、修改、轉載;保留來源出處更佳。
- **回饋**:如發現規則描述有誤、有可改進之處,或有其他實戰情景可補充,歡迎提交 Issue 或 Pull Request。
- **免責聲明**:所有指令源於個人使用經驗,實際效果視乎所用 AI 模型版本、工具更新狀態、用戶使用習慣而異;請自行驗證後使用。