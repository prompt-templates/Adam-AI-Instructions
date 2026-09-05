# 專案式 AI Agent 全域指令

*Adam's AI Instructions*

> 最新發布：`v1.1.0`。中英文完整指令已同步發布；[查看這版改動](docs/releases/v1.1.0.md)。

[English](README.en.md) · [繁中完整全域指令](prompts/02-claude-code-meta-instruction/prompt.md) · [中文使用指南](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.html) · [English complete instruction](prompts/02-claude-code-meta-instruction/prompt.en.md) · [English guide](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.en.html)

當 AI 可以進入你的專案或工作區，讀檔、改檔、執行工具，甚至準備發佈內容，問題不再只是它答得好不好。你需要知道它看過甚麼、為何這樣做，以及完成後怎樣核對。

這份**完整全域指令**是給這類 AI Agent 的工作守則。把它放進你已授權的專案或工作區後，AI 會先理解眼前任務和已有規則，再開始工作；小事直接做好，牽涉資料、機密、發佈或多處互相影響時，會把風險、結果和核對方法講清楚。

它適合 Claude Code、OpenAI Codex、Cursor、Antigravity，以及其他能在授權工作區內持續工作的 AI Agent。一般網頁版聊天工具不在本專案的使用範圍內。

## 從常見原則，到可執行規則

![常見 AI 原則如何變成專案式 AI Agent 全域指令的可執行規則](prompts/02-claude-code-meta-instruction/images/prompt-02-principles-zh-hant.png)

你可能已見過 `Follow YAGNI principles`、`Keep it simple`、`Verify before acting`、`Plan before execution` 或 `Human in the loop`。它們方向正確，但通常沒有說明：何時適用、何時不能套用，以及 AI 要怎樣證明已做到。

專案式 AI Agent 全域指令不是要取代這些原則，也不聲稱獲任何公司或專家背書。這份指令把它們整理成可判斷、可執行、可驗收的工作規則：

| 熟悉的提示方向 | 這份指令令 Agent 實際做到 |
|---|---|
| `Follow YAGNI principles` / `Keep it simple` | 在使用者目標與明示範圍內，按後果、未知與可回復性決定力度；只做最小但足夠完成驗收的必要改動，不因持久化、同步或治理自動擴張任務。 |
| `Verify before acting` | 複雜任務先確認核心真源覆蓋；分開事實、推論與未核實內容。 |
| `Plan before execution` | 只有互相依賴、高影響或難以恢復的工作，才要求可驗收計劃。 |
| `Human in the loop` | 安全的本地工作可直接完成；推送、發布、刪除、權限與費用等外部動作另取明確授權。 |
| `Manage context` | 先限制搜尋和閱讀範圍，保留高訊號內容，避免把長規則和無關資料一併塞進脈絡。 |

[查看這些原則如何對照這份指令的完整規則與公開來源](prompts/02-claude-code-meta-instruction/README.md#從熟悉原則到可執行規則)。

## 裝上後，你會看到甚麼不同

例如你叫 AI 改一份 README，它不會一看題目就改。它會先找現有寫法、相關規則和可讀回的結果，再只改需要改的地方。

如果你要它處理研究、資料整理或準備發佈，它會分開已核實的事實、仍未確定的內容和真正需要你決定的選擇。刪除、覆寫、公開發佈、權限和費用，仍然由你最後確認。

這不是要把每件小事做成流程。清楚而可回復的小修可以直接完成；真正容易出錯或影響較大的工作，才需要多一層核對。

## 開始使用

1. 先在你的 AI 工具中開啟正確的專案或工作區。不要一開始就讓它看到不相干的個人資料夾。
2. 選擇你要的回覆語言，然後複製一份完整指令： [繁中完整全域指令](prompts/02-claude-code-meta-instruction/prompt.md) 或 [English complete instruction](prompts/02-claude-code-meta-instruction/prompt.en.md)。它就是要長期套用給 AI Agent 的全域工作規則，不是範例文字。
3. 把全文放進該工具為這個專案或工作區長期套用的指令／規則位置，儲存後開一個新任務。
4. 先用一件小而真實的工作試它，例如：「先讀這個專案的規則與測試方式，再修正 README 的一處錯字並讀回核對。」

這份 repo 只提供完整 meta instruction；各工具的設定檔、匯入方式和安裝位置，請依該工具或你的 Agent Handoff Kit 設定處理。

如果你想先看 AI 在常見情境下會怎樣回應，可直接看[中文使用指南](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.html)或 [English guide](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.en.html)。

## v1.1.0 更適合的任務

- **Workplace**：整理文件、查證資料、準備摘要或更新本地工作內容時，小事可直接完成；複雜工作先確認必要來源，獨立安全工作不會因局部缺口無故停下。
- **Creative**：創作、改稿、命名和視覺方向按題意、語氣、格式和禁忌驗收，不硬套工程流程；涉及真實聲稱仍會核對。
- **Coding agent**：讀待改位置與直接上下文，做最小足夠修改，工具卡住時先確認沒有半寫入，再用同等安全通道重試一次。
- **Governance**：規則修補先分清真源和責任範圍；高風險或多階段工作先做層級對焦與真源覆蓋檢查，對準後才進入全圖計劃和獨立反證；準備或試行也要核實自身條件。
- **反證審閱**：對可能影響安全、權限、資料完整性、公開邊界或跨表面承諾的方案，先找能推翻方案的反例，不把未查漏計劃包裝成完成品。

## 這份指令守住甚麼

- AI 改動前，先讀與任務有關的規則、檔案和直接上下文。
- 長任務或多階段工作會先分清最終成果、本輪產出、核心真源覆蓋和停止條件，再決定是否需要全圖計劃。
- 做研究時，分清來源、日期、事實、推論和未核實內容。
- 寫入資料後，讀回核對；不知道安全交付位置時，不會自作主張建立一套平行結構。
- 重要計劃會說明成功怎樣證明、失敗後留下甚麼狀態，以及怎樣恢復。
- 真正缺少核心資料或安全條件時，AI 會直接說明受阻，而不是交給你一份看似完整、其實不能安全採用的計劃。

## 它不會代你決定的事

這份指令不會取代工具本身的權限、沙盒、版本控制或備份，也不會把有一份 prompt 說成系統已經安全。

公開發佈、付款、推送、刪除、權限變更和其他不可逆操作，仍要由你清楚確認。它的作用是讓 AI 在你作決定前，把事情看得更清楚。

## 最新更新：v1.1.0

v1.1.0 合併重複規則，讓授權延續、局部受阻、任務粒度及答案格式更清楚；選項保留原有標識並避免重複呈現，準備或試行不會因名稱而自動取得可執行資格。[了解這版改動](docs/releases/v1.1.0.md)

## 更多資料

- [繁中使用說明](prompts/02-claude-code-meta-instruction/README.md)
- [English overview](prompts/02-claude-code-meta-instruction/README.en.md)
- [中文互動指南](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.html)
- [English interactive guide](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.en.html)
- [更新紀錄](CHANGELOG.md)

## 延伸閱讀：Agent Handoff Kit 與 Innovation Loop

這份指令本身已可單獨使用，負責 AI 在這一輪工作怎樣判斷、修改和核對。

如你的工作會跨很多次對話或換不同 Agent，可加用 [Agent Handoff Kit](https://adamchanadam.github.io/agent-handoff-kit/agent-handoff-kit-intro.html)，保存目前狀態、交接和收工資訊。長項目需要由想法走到研究、驗證和計劃時，可再了解 [Innovation Loop](https://github.com/Adamchanadam/agent-handoff-innovation-loop)。它們是按需要加入的延伸工具，不是開始使用這份指令的前提。

## 授權與回饋

本專案採 [MIT License](LICENSE)。如果實際使用情況和指南不同，歡迎回報工具名稱、指令放置位置和可重現情境；請不要貼出機密或私人檔案內容。
