# Adam's AI Instructions｜讓會動手的 AI 做事更穩

[English](README.en.md) · [繁中指令](prompts/02-claude-code-meta-instruction/prompt.md) · [中文指南](prompts/02-claude-code-meta-instruction/guide.html) · [English instruction](prompts/02-claude-code-meta-instruction/prompt.en.md) · [English guide](prompts/02-claude-code-meta-instruction/guide.en.html)

這不是一份叫 AI「乖乖聽話」的模板。

它是給會讀檔、改檔、執行工具、整理資料，甚至可以發佈成果的 AI Agent 一套工作底線：先弄清楚，再動手；該快時快，該停時停；交付後能讓人核對。

適合把 AI 用在真正工作的人。你不必是工程師，只要把指令放進自己已授權的專案或工作區。

> 一般網頁版 ChatGPT 與 Claude 對話不在本專案支援範圍。它們可以幫你想，但不能可靠地承擔本機專案、檔案操作與跨工作階段交付。

## 為何值得用

很多 AI 看似勤快，實際上會太早動手：還沒讀清楚專案便改檔；研究時把猜測當結論；把「已寫入檔案」當成「事情已完成」。

這份指令讓 AI 先把這些事做對：

- 寫／改程式前，先找專案規則、相關檔案與可用的驗收方式。
- 做研究時，分開來源、日期、事實、推論與未核實內容。
- 整理資料時，先辨認正式來源、工作區與交付位置；寫入後讀回核對。
- 遇到刪除、覆寫、發佈、權限、費用或機密，先說清影響並取得相應確認。
- 小修不做成審計；一旦出錯會有較大影響的方案，先找出可以推翻它的風險，才叫它可執行。

## 選擇你的指令語言

請選擇繁中或英文版本，貼到你正在使用的 Agent 工具內。兩份指令處理相同的工作邊界；分別只在 AI 的預設回覆語言。

| 工具 | 最簡單的放置方式 |
|---|---|
| Claude Code | 在專案根目錄放入 `CLAUDE.md`，貼入指令。 |
| OpenAI Codex | 在專案根目錄放入 `AGENTS.md`，貼入指令。 |
| Cursor | 最簡單是專案根目錄的 `AGENTS.md`；也可用 Project Rules。 |
| Antigravity | 建立 Workspace Rule，設定為常駐規則，貼入指令。 |

## 三分鐘開始

1. 開啟 [繁中指令原文](prompts/02-claude-code-meta-instruction/prompt.md)，複製全文。
2. 先在工具內開啟正確的專案／工作區；不要讓 AI 一開始就看到不相干的個人資料夾。
3. 依上表把全文貼到工具的指令位置，儲存後開一個新任務。
4. 用一件小而真實的工作試它，例如：「先讀這個專案的規則與測試方式，再修正 README 的一處錯字並讀回核對。」

各工具的當前官方設定說明：

- [Claude Code：CLAUDE.md](https://code.claude.com/docs/en/memory)
- [OpenAI Codex：AGENTS.md](https://developers.openai.com/codex/guides/agents-md/)
- [Cursor：Rules 與 AGENTS.md](https://docs.cursor.com/context/rules-for-ai)
- [Antigravity：Rules](https://antigravity.google/docs/rules-workflows)

## 為何它不會把工作變複雜

這份指令不是叫 AI 凡事停下來寫計劃。它先看工作是否清楚、能否安全回復、出錯會帶來甚麼影響。

所以，一處明確的小修可以直接完成並讀回；涉及資料、機密、公開發佈或多個互相影響的改動，才會多做必要的核對。你得到的是更少無謂來回，以及在重要時刻更清楚的證據和確認。

## 最新更新：v0.8.2

重要改動會先經過查漏，才可稱為可執行；小事仍保持直接。這讓你在批准 AI 動手前，更容易看見範圍、風險和怎樣核對結果。[了解這版改動](docs/releases/v0.8.2.md)

## 與 Agent Handoff Kit、Innovation Loop 一起用

這份指令管的是「這一輪 AI 怎樣做事」。

[Agent Handoff Kit](https://adamchanadam.github.io/agent-handoff-kit/agent-handoff-kit-intro.html) 管跨工作階段的狀態、交接與收工；[Innovation Loop](https://github.com/Adamchanadam/agent-handoff-innovation-loop) 管長項目的探索、研究驗證與計劃回流。三者可以一起用，但不需要每個短任務都建立額外文件。

最簡單的分工是：

| 你需要的事 | 用哪一層 |
|---|---|
| AI 這一輪先讀、再改、會核對、懂得停 | 專案式 AI Agent 全域指令 |
| 換了對話或換了 Agent，仍知道做到哪裡 | Agent Handoff Kit |
| 長項目需要由想法走到研究、驗證與計劃 | Innovation Loop |

## 不會替你做的事

- 不會繞過工具本身的權限、沙盒或企業政策。
- 不會把「有一份 prompt」說成資料已備份、權限已限制或外部平台已安全。
- 不會把一般聊天工具包裝成可靠的專案代理。
- 不會替你確認公開發佈、付款、推送、刪除或權限變更。

## 相關頁面

- [繁中指令說明](prompts/02-claude-code-meta-instruction/README.md)
- [English overview](prompts/02-claude-code-meta-instruction/README.en.md)
- [中文互動指南](prompts/02-claude-code-meta-instruction/guide.html)
- [English interactive guide](prompts/02-claude-code-meta-instruction/guide.en.html)
- [更新紀錄](CHANGELOG.md)

## 授權與回饋

本專案採 [MIT License](LICENSE)。如果實際使用情況和指南不同，歡迎回報工具名稱、指令放置位置與可重現情境；請不要貼出機密或私人檔案內容。
