# Adam's AI Instructions｜AI 治理指令庫

個人於日常使用 AI 工具(Claude Cowork、Claude Code、ChatGPT 等)過程中累積的治理指令(Meta Instructions)集合。

---

## 一、本資料庫內容

收錄個人於實際操作中,經反覆遇到問題與修正後沉澱出的 Meta Instruction 文本。每一份指令對應一類具體場景,用於約束 AI 在該場景下的行為,以提升輸出的一致性、可驗收性與可審計性。

套用後可獲得的具體好處:

- ✅ 偏好優先序:事實可驗收 > 穩定性 > 根因治理 > 完整性交付 > 最小改動
- ✅ AI 主動判斷並一次提交完整方案,減少反覆提問
- ✅ 動手修改前先輸出完整執行計劃(全圖優先規則):終點、影響範圍、可量指標、驗收方法,用戶 30 秒可批准、否決或修改 — 杜絕中途範圍偏離
- ✅ 核對不到的部分清楚標記為 UNVERIFIED,不會混淆已驗證與未驗證內容
- ✅ 修改以「精準錨點 + 修改前(BEFORE)/ 修改後(AFTER)+ 變更日誌」交付,方便直接貼換,合併零遺漏
- ✅ 同一規則只在單一定義塊存在,減少指令四散,出現自相矛盾

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
├── README.md                                   ← 本頁
└── prompts/
    └── 01-claude-cowork-meta-instruction/
        ├── README.md                           ← 該指令的介紹頁
        └── prompt.md                           ← 可直接複製使用的原文
```

每份指令獨立存放於各自資料夾,內含:

- `README.md`:文字介紹頁,說明該指令對應的痛點、規則內容、治理作用、適用情景。
- `guide.html`:互動式指南,含 SVG 視覺化說明,以瀏覽器開啟即可閱讀。
- `prompt.md`:Prompt 原文,可直接複製貼至 AI 工具的 system prompt、personal preferences、project instructions 等欄位。

---

## 四、使用方式

1. 從下文索引選取適用於自身工具的指令。
2. 閱讀該指令的 `README.md`,理解規則內容與適用情景。
3. 開啟 `prompt.md`,複製全文。
4. 貼至所用 AI 工具的對應欄位:
   - Claude Cowork:Settings → Personal Preferences。
   - Claude Code:`~/.claude/CLAUDE.md` 或項目根目錄 `CLAUDE.md`。
   - ChatGPT:Settings → Personalization → Custom Instructions。
   - 其他工具:System prompt、Project instructions、Custom instructions 等同類欄位。
5. 套用後觀察 AI 行為變化;若某條規則與個人習慣衝突,可自行刪改。

各指令的規則段落可獨立使用,毋須整套套用。

---

## 五、Prompt 索引

| # | 名稱 | 互動指南 | 文字介紹 | Prompt 原文 | 適用工具 |
|---|------|---------|---------|-------------|----------|
| 01 | Claude Cowork Meta Instruction | [guide.html](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/01-claude-cowork-meta-instruction/guide.html) | [README.md](prompts/01-claude-cowork-meta-instruction/README.md) | [prompt.md](prompts/01-claude-cowork-meta-instruction/prompt.md) | Claude Cowork(及一般 Claude 對話介面) |

> **建議閱讀順序**:先點擊「互動指南」(以瀏覽器開啟,含 SVG 視覺化說明),再參考「文字介紹」深入細節,最後複製「Prompt 原文」套用至所用 AI 工具。

未來將陸續加入其他工具與場景的指令版本。

---

## 六、授權與貢獻

- **授權**:本資料庫內容供任何用戶免費使用、修改、轉載;保留來源出處更佳。
- **回饋**:如發現規則描述有誤、有可改進之處,或有其他實戰情景可補充,歡迎提交 Issue 或 Pull Request。
- **免責聲明**:所有指令源於個人使用經驗,實際效果視乎所用 AI 模型版本、工具更新狀態、用戶使用習慣而異;請自行驗證後使用。
