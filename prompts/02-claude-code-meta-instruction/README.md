# 📖 使用說明

[English overview](README.en.md) · [繁中指令](prompt.md) · [中文指南](guide.html) · [English prompt](prompt.en.md) · [English guide](guide.en.html) · [主 README](../../README.md)

「專案式 AI Agent 全域指令」給能在你授權工作區內讀檔、改檔、執行工具與交付成果的 AI Agent 使用。

它不是要 AI 變慢，而是避免它太早動手：先讀範圍與規則；有證據才下結論；改完有方法核對；小事不加戲，一旦出錯會有較大影響的事情不裝作安全。

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

## 最短安裝方法

1. 複製 [prompt.md](prompt.md) 全文。
2. 先進入正確的專案／工作區。
3. 貼到上表對應的位置，儲存後重新開任務。
4. 先用一個小工作確認：要求 AI 讀專案規則，再修正一處小錯並讀回核對。

各工具的畫面與名稱會更新，請以官方當前文件為準：[Claude Code](https://code.claude.com/docs/en/memory)、[Codex](https://developers.openai.com/codex/guides/agents-md/)、[Cursor](https://docs.cursor.com/context/rules-for-ai)、[Antigravity](https://antigravity.google/docs/rules-workflows)。

## 不會令每件事變複雜

這份指令會按工作影響決定力度。明確的小修直接完成並讀回；涉及資料、機密、公開發佈或多個互相影響的改動，才會多做必要的核對與確認。

你不需要了解背後規則怎樣整理。只要把全文貼到工具內，用一件小而真實的工作開始即可。
