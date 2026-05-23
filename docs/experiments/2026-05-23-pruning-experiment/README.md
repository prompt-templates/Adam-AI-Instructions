# 🧪 2026-05-23 Meta Instruction 瘦身實驗

> ## 🏆 一句結論
>
> **「B 中度瘦身」勝出** — 正式發佈為 **v0.7.0 — 12-節結構整合版**。
>
> 📊 規則覆蓋率 **100%**　·　📉 字數 **−45%**（5500 → 3000）　·　📈 綜合分較 v0.6.1 提升 **15.5%**
>
> 👉 **即時試用**：[`prompts/01-claude-cowork-meta-instruction/prompt.md`](../../../prompts/01-claude-cowork-meta-instruction/prompt.md) — Claude Cowork / OpenAI Codex / AGENTS.md 通用版

---

## 🎯 為何做這個實驗

Anthropic Claude Code 官方 2026 best practices 明示：

> *「If your CLAUDE.md is too long, Claude ignores half of it because important rules get lost in the noise. Ruthlessly prune.」*

v0.6.1 累積至 20 節約 5500 字 — 已踩入官方警告區。本實驗回答一條問題：

🔎 **瘦身能否提升 AI 對規則的觸發準確度，而不犧牲覆蓋率？**

⚠️ 硬條件：**新版本效能不得差於現有版本**。任何維度退步即放棄整合。

---

## 🧬 實驗設計

### 三檔瘦身策略（A／B／C 是實驗代號，描述瘦身幅度）

| 版本 | 字數變化 | 節數變化 | 重組程度 | 例子保留 |
|---|---|---|---|---|
| A 保守 | -20% | 20 → 18 | 不重組，只剪冗餘句 | 90% |
| **B 中度** ⭐ | **-45%** | **20 → 12** | **合併同質節** | **50%** |
| C 激進 | -65% | 20 → 8 | 三層架構重組 | 30% |

### 📋 8 場景實測案例集（37 條獨立規則檢查點）

每場景列「應觸發規則清單」（核心 × 3 / 重要 × 2 / 一般 × 1）：

1. 單檔小修改（補丁式 + 不觸發全圖優先）
2. 多檔治理改動（觸發全圖優先 + 治理改動先審核 + 深度修補）
3. 歧義指令（歧義處理 + 不出題者）
4. 可驗證事實提問（先讀後判 + 外部平台核對）
5. 創作類任務（豁免規則）
6. 計算（四步法）
7. JSON 輸出（格式硬規則 + 真源對齊）
8. 用戶質疑（捷徑信號處理）

詳見 [test_cases.md](test_cases.md)。

### 📊 四輪實測維度

| # | 維度 | 量度方法 |
|---|---|---|
| 1 | 規則覆蓋率 | 逐版本逐場景檢查 37 條規則是否覆蓋 |
| 2 | 可讀性／尋取效率 | 模擬 AI 從版本中找出對應規則所需查節數 |
| 3 | 用戶優先序對位 | 按用戶現行優先序加權（事實 5：穩定 4：根因 3：完整 2：最小 1）|
| 4 | 官方對齊度 | 對照 Anthropic 五項關鍵指引 |

詳見 [evaluation_matrix.md](evaluation_matrix.md)。

---

## 🏆 實驗結果

### ✅ 規則覆蓋率 — 三檔全部 100%（硬條件達成）

| 版本 | 通過場景 | 總分 | 核心規則覆蓋 |
|---|---|---|---|
| 現有 v0.6.1 | 8 / 8 | 100 | 100% |
| A 保守 | 8 / 8 | 100 | 100% |
| **B 中度** ⭐ | **8 / 8** | **100** | **100%** |
| C 激進 | 8 / 8 | 100 | 100% |

### 📈 風險調整後綜合分排名

| 名次 | 版本 | 綜合分 | 較 v0.6.1 提升 |
|---|---|---|---|
| 🏆 1 | **v0.7.0 — 12-節結構整合版**（B 中度） | **87.8** | **+15.5%** |
| 🥈 2 | C 激進 | 85.0 | +11.8% |
| 🥉 3 | A 保守 | 78.2 | +2.9% |
| — | 現有 v0.6.1 | 76.0 | 基線 |

詳見 [comparison_report.md](comparison_report.md)。

---

## 💡 為何 B 勝出（五大理由）

**第一，B 在四維全部超越 v0.6.1，綜合分提升 15.5%**　A 只 +2.9%，C +11.8% 但風險係數扣減後反不及 B。

**第二，B 直擊用戶優先序最高的三項**　規則覆蓋 100%（事實可驗收）、合併幅度可控（穩定性）、徹底解決「規則散落 20 節太長」根因（根因治理）。

**第三，B 對官方「Ruthlessly prune」高度對齊但未過頭**　字數 3000 進入官方建議區間（< 4000），規則密度顯著提升，但保留主題分節，AI 尋取規則仍可循節找尋。

**第四，B 的重組風險低（係數 0.98）**　12 節仍清晰映射原 20 節主題。相反 C 將「先讀後判 + 治理改動 + 變更交付」擠成兩節、將執行環境 19 條擠成一節，雖總分 91.4 但「重組期漏帶舊規則」風險係數 0.93，調整後落敗於 B。

**第五，B 的完整性損失（70 分）在用戶優先序中排第四位，影響權重低**　損失的主要是部分例子和重複說明，**核心規則語意 100% 保留**。

---

## 🎁 實用價值

### 對個人用戶

- ✅ **AI 對規則觸發更穩定** — 12 節密度高、重點突出，AI 不易在長文中漏讀
- ✅ **記憶負擔減半** — 用戶自己讀 Meta Instruction 時亦更易掌握
- ✅ **長期可維護** — 合併同質節後，新增規則時較易判斷往哪一節加

### 對團隊／企業用戶

- ✅ **複製成本降低** — 3000 字較易貼入各種 AI 工具的 system prompt 欄位
- ✅ **培訓門檻降低** — 新成員理解規則所需時間減少
- ✅ **審計簡單** — 12 節對應 12 個治理主題，覆蓋率檢查容易

### 對 Meta Instruction 研究者

- 📌 **示範「不修不加、只剪只合併」的瘦身路徑** — 數據顯示擴張不等於改進，剪裁不等於損失
- 📌 **驗證 Anthropic 官方「Ruthlessly prune」實踐效果** — 實測數據支持官方主張
- 📌 **可複製的實驗方法** — 本實驗的測試案例集 + 評分矩陣可作為其他 Meta Instruction 瘦身的範本

---

## 📁 檔案索引

| 檔案 | 內容 |
|---|---|
| [test_cases.md](test_cases.md) | 8 場景 × 37 條規則檢查點 |
| [evaluation_matrix.md](evaluation_matrix.md) | 三版本 × 8 場景 × 四輪評分矩陣 |
| [comparison_report.md](comparison_report.md) | 四版本多維對照報告 + 勝出宣告 |
| [v_a_conservative.md](v_a_conservative.md) | A 保守版（20 → 18 節） |
| 🏆 [v_b_moderate.md](v_b_moderate.md) | **v0.7.0 — 12-節結構整合版**（實驗代號 B 中度，20 → 12 節）— **已採用** |
| [v_c_aggressive.md](v_c_aggressive.md) | C 激進版（20 → 8 節） |

🚀 **勝出版本已上線**：[prompts/01-claude-cowork-meta-instruction/prompt.md](../../../prompts/01-claude-cowork-meta-instruction/prompt.md)（v0.7.0）

---

## 📚 官方文件來源

- [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices)
- [Prompting best practices - Claude Docs](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices)
