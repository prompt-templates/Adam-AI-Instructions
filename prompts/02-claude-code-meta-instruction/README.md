# 📖 使用說明

[English overview](README.en.md) · [繁中指令](prompt.md) · [中文指南](guide.html) · [English prompt](prompt.en.md) · [English guide](guide.en.html) · [主 README](../../README.md)

當 AI 可以進入你的專案或資料夾，問題不再只是它答得好不好。它可能未看清規則便改檔，未核實資料便下結論，或者做了一半便說任務完成。

「專案式 AI Agent 全域指令」是給這類 AI 的工作守則。它會先看清楚專案和任務，再做需要做的事；小修不用兜圈，牽涉資料、機密、發佈或多處互相影響的改動，會先說清範圍和影響，完成後讓你有方法核對。工具的權限和每次真正公開或不可逆的決定，仍然在你手上。

## 從熟悉原則到可執行規則

![常見 AI 原則如何由 02 Prompt 變成可執行規則](images/prompt-02-principles-zh-hant.png)

這份指令不提供研究、程式、法規或任何行業的內置知識。它規定 Agent 怎樣使用使用者要求、專案檔案、工具、權限和可核對來源。

你可能已見過 `Follow YAGNI principles`、`Keep it simple`、`Verify before acting`、`Plan before execution` 或 `Human in the loop`。這些原則有用，但單獨使用時，往往沒有說明適用條件、停止條件或例外。02 把它們深化成下列工作規則：

| 熟悉的提示方向 | 單句口號未說清的事 | 02 的落地方式 |
|---|---|---|
| `Follow YAGNI principles` / `Keep it simple` | 甚麼可省略，甚麼仍是本次交付必需。 | 按後果、未知與可回復性決定力度；只處理阻礙驗收、由修改造成或令交付矛盾的問題；作最小而完整的相關修改。 |
| `Verify before acting` | 核實甚麼、來源衝突怎樣處理。 | 先讀真源與直接上下文；區分來源、日期、事實、推論及未核實內容。 |
| `Plan before execution` | 小事會否也被迫寫長計劃；計劃怎樣才算可靠。 | 只在依賴、高影響、難恢復或外部副作用等情況使用全圖計劃；計劃須有成功證據、反例與必要的獨立反證。 |
| `Human in the loop` | 哪些安全工作可自主做，哪些操作必須停下。 | 已授權、低風險、可回復、無外部副作用的步驟可直接執行；發布、刪除、權限、費用及其他外部動作另取明確授權。 |
| `Manage context` | 怎樣避免長規則、搜尋結果和舊脈絡互相干擾。 | 先以搜尋、索引和抽樣建立範圍，再讀直接相關內容；長期工作分開保存交接狀態。 |

這些方向與 OpenAI、Anthropic、Google 的公開建議一致：規則要直接、有結構、避免重複，並保留完成工作所需的高訊號內容。這不是任何一方對 02 的認證；02 是把公開原則與實際 Agent 工作中的失敗模式整合成一份可使用的規則。參考：[OpenAI model guidance](https://developers.openai.com/api/docs/guides/latest-model)、[Anthropic context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)、[Google prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)。

## 它會怎樣幫你

| 工具 | 最簡單安裝位置 |
|---|---|
| Claude Code | 專案根目錄 `CLAUDE.md` |
| OpenAI Codex | 專案根目錄 `AGENTS.md` |
| Cursor | 專案根目錄 `AGENTS.md` |
| Antigravity | Always-on Workspace Rule |

不支援把一般網頁版 ChatGPT 或 Claude 對話當作可靠的專案代理工具。

## 貼入後，你會看到甚麼不同

- 改程式前，AI 先找相關檔案、既有規則與驗收方法。
- 研究不把估算寫成事實，會標出來源、日期、推論與未知。
- 新檔案不會擅自假定固定資料夾；先沿用專案或平台已指定的位置。
- 寫入後會讀回；出錯、中斷或衝突不能假裝成功。
- 刪除、覆寫、發佈、權限、費用與機密有額外確認門檻。
- 單檔小修保持簡短；一旦出錯會有較大影響的計劃要先經獨立反證，才可稱為可執行。
- 你不會先收到一份未查漏的半成品計劃；核心條件補不齊時，AI 會直接說明受阻原因與繼續所需條件。

## 最短安裝方法

1. 複製 [prompt.md](prompt.md) 全文。
2. 先進入正確的專案／工作區。
3. 貼到上表對應的位置，儲存後重新開任務。
4. 先用一個小工作確認：要求 AI 讀專案規則，再修正一處小錯並讀回核對。

各工具的畫面與名稱會更新，請以官方當前文件為準：[Claude Code](https://code.claude.com/docs/en/memory)、[Codex](https://developers.openai.com/codex/guides/agents-md/)、[Cursor](https://docs.cursor.com/context/rules-for-ai)、[Antigravity](https://antigravity.google/docs/rules-workflows)。

## 不會令每件事變複雜

這份指令會按工作影響決定力度。明確的小修直接完成並讀回；涉及資料、機密、公開發佈或多個互相影響的改動，才會多做必要的核對與確認。

你不需要了解背後規則怎樣整理。只要把全文貼到工具內，用一件小而真實的工作開始即可。
