# 2026-05-23 瘦身實驗記錄

這是歷史實驗記錄，不是安裝入口。

現行指令請先按工具名稱選：

- [對話型工具版本](../../../prompts/01-claude-cowork-meta-instruction/prompt.md)
- [代理式工具版本](../../../prompts/02-claude-code-meta-instruction/prompt.md)

---

## 一、為何做這個實驗

當時的對話型工具版本已累積到 20 節，內容開始過長。問題不是規則不夠，而是規則太散，AI 與人都較難快速抓到重點。

這次實驗要回答一個問題：

> 能否在不丟失核心規則的前提下，把指令壓得更短、更清楚？

---

## 二、測試了哪三個版本

| 版本 | 做法 | 風險 |
|---|---|---|
| A 保守 | 只剪冗餘句，結構幾乎不動 | 改動安全，但改善有限。 |
| B 中度 | 合併同類規則，保留清楚分節 | 改動較明顯，但仍容易追溯。 |
| C 激進 | 大幅重組，壓到更短 | 最短，但較容易把不同規則塞得太密。 |

最後採用的是 B 中度版本，成為 v0.7.0 的基礎。

---

## 三、怎樣驗證

實驗使用 8 個日常場景，逐條檢查規則是否仍能被觸發。

場景包括：

1. 單檔小修改
2. 多檔治理改動
3. 歧義指令
4. 可驗證事實提問
5. 創作類任務
6. 計算
7. JSON 輸出
8. 使用者指出錯誤後重做

完整測試表見 [test_cases.md](test_cases.md)。

---

## 四、結果

| 版本 | 規則覆蓋 | 閱讀負擔 | 整體判斷 |
|---|---|---|---|
| 原版本 | 覆蓋完整 | 偏重 | 可用，但不夠精煉。 |
| A 保守 | 覆蓋完整 | 略有改善 | 不足以解決根因。 |
| B 中度 | 覆蓋完整 | 明顯改善 | 採用。 |
| C 激進 | 覆蓋完整 | 最短 | 壓縮過度，長期維護風險較高。 |

實驗當時的分數與矩陣保留在 [evaluation_matrix.md](evaluation_matrix.md) 與 [comparison_report.md](comparison_report.md)。分數只代表當時測試條件，不代表永遠有效。

---

## 五、這份記錄的用途

這份記錄主要用來說明一件事：這套指令不是越加越多，而是會在規則變長時回頭剪裁。

它也留下可重用的驗證方法：先列場景，再逐條檢查規則是否仍能觸發。

---

## 六、檔案索引

| 檔案 | 內容 |
|---|---|
| [test_cases.md](test_cases.md) | 8 個測試場景與檢查點。 |
| [evaluation_matrix.md](evaluation_matrix.md) | 三個版本的評分矩陣。 |
| [comparison_report.md](comparison_report.md) | 為何採用 B 中度版本。 |
| [v_a_conservative.md](v_a_conservative.md) | A 保守版全文。 |
| [v_b_moderate.md](v_b_moderate.md) | B 中度版全文。 |
| [v_c_aggressive.md](v_c_aggressive.md) | C 激進版全文。 |

---

## 七、來源

- [Anthropic Claude Code memory documentation](https://code.claude.com/docs/en/memory)
- [Anthropic prompt engineering documentation](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices)
