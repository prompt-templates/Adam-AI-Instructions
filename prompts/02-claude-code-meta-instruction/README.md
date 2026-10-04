# 📖 使用說明

## v1.2.0 版本

`prompt.md` 與 `prompt.en.md` 是已發布的 v1.2.0 完整指令，取代 v1.1.0 成為最新公開基準。版本說明見 [v1.2.0 發布記錄](https://github.com/prompt-templates/Adam-AI-Instructions/releases/tag/v1.2.0)；上一版見 [v1.1.0 發布記錄](https://github.com/prompt-templates/Adam-AI-Instructions/releases/tag/v1.1.0)。

v1.2.0 明列 KISS、YAGNI 及「最少返工而完成使用者要求的成果」。使用者提出需求、使用成品及回饋；AI 負責研究、技術選擇、解難、驗收與交付。已授權安全工作持續做，局部缺口只阻擋依賴部分；沙盒外執行依平台允許的通道處理，不重問既有授權。請使用 [繁中全文](prompt.md) 或 [英文全文](prompt.en.md)，不必拼接補充條文。

## 使用說明

[English overview](README.en.md) · [繁中指令](prompt.md) · [中文指南](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.html) · [English prompt](prompt.en.md) · [English guide](https://prompt-templates.github.io/Adam-AI-Instructions/prompts/02-claude-code-meta-instruction/guide.en.html) · [主 README](../../README.md)

當 AI 可以進入你的專案或資料夾，問題不再只是它答得好不好。它可能未看清規則便改檔，未核實資料便下結論，或者做了一半便說任務完成。

「專案式 AI Agent 全域指令」是給這類 AI 的工作守則。它會先看清楚專案和任務，再做需要做的事；小修不用兜圈，牽涉資料、機密、發佈或多處互相影響的改動，會先說清範圍和影響，完成後讓你有方法核對。工具的權限和每次真正公開或不可逆的決定，仍然在你手上。

## 從熟悉原則到可執行規則

![常見 AI 原則如何變成專案式 AI Agent 全域指令的可執行規則](images/prompt-02-principles-zh-hant.png)

這份指令不提供研究、程式、法規或任何行業的內置知識。它規定 Agent 怎樣使用使用者要求、專案檔案、工具、權限和可核對來源。

你可能已見過 `Follow YAGNI principles`、`Keep it simple`、`Verify before acting`、`Plan before execution` 或 `Human in the loop`。這些原則有用，但單獨使用時，往往沒有說明適用條件、停止條件或例外。這份指令把它們深化成下列工作規則：

| 熟悉的提示方向 | 單句口號未說清的事 | 這份指令的落地方式 |
|---|---|---|
| `Follow YAGNI principles` / `Keep it simple` | 甚麼可省略，甚麼仍是本次交付必需。 | 在使用者目標與明示範圍內，按後果、未知與可回復性決定力度；只處理阻礙驗收、由修改造成或令交付矛盾的問題；作最小足夠的相關修改，不因持久化、同步或治理自動擴張任務。 |
| `Verify before acting` | 核實甚麼、來源衝突怎樣處理。 | 複雜任務先過真源覆蓋；區分來源、日期、事實、推論及未核實內容。 |
| `Plan before execution` | 小事會否也被迫寫長計劃；計劃怎樣才算可靠。 | 複雜工作先在內部對焦；重大影響、複雜相依需事先對齊或使用者要求時，才使用全圖計劃。 |
| `Human in the loop` | 哪些安全工作可自主做，哪些操作必須停下。 | 已授權、低風險、可回復、無外部副作用的步驟可直接執行；發布、權限、費用及其他外部動作取得相應明確授權；有效授權不重問，臨時產物例外見完整指令。 |
| `Manage context` | 怎樣避免長規則、搜尋結果和舊脈絡互相干擾。 | 來源明確便直接讀，未定位才搜尋／查索引；沿用有效證據，保存真實進度，恢復時不重啟已完成工作。 |

這些方向與 OpenAI、Anthropic、Google 的公開建議一致：規則要直接、有結構、避免重複，並保留完成工作所需的高訊號內容。這不是任何一方對這份指令的認證；它是把公開原則與實際 Agent 工作中的失敗模式整合成一份可使用的規則。參考：[OpenAI model guidance](https://developers.openai.com/api/docs/guides/latest-model)、[Anthropic context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)、[Google prompt design strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)。

## 它會怎樣幫你

v1.2.0 把技術判斷與執行責任交給 AI，保留必要安全保障；沿用有效證據與計劃，按當前風險安排核查，達到既定要求便交付並停止。

- **Workplace**：整理文件、查證資料、準備摘要或更新本地工作內容時，小事可直接完成；長任務先分清本輪真正產出。
- **Creative**：創作、改稿、命名和視覺方向按題意、語氣、格式和禁忌驗收，不硬套工程流程；涉及真實聲稱仍會核對。
- **Coding agent**：讀待改位置與直接上下文，做最小足夠修改，工具卡住時先確認沒有半寫入，再用已授權的安全方案繼續處理。
- **Governance**：規則修補先分清真源和責任範圍，沿用已確認的計劃；重大影響或複雜相依才展開全圖計劃，必要審閱按當前操作與聲稱的風險安排。
- **反證審閱**：對可能影響安全、權限、資料完整性、公開邊界或跨表面承諾的方案，先找能推翻方案的反例，不把未查漏計劃包裝成完成品。

這份 repo 只提供完整 meta instruction；各工具的設定檔、匯入方式和安裝位置，請依該工具或你的 Agent Handoff Kit 設定處理。不支援把一般網頁版 ChatGPT 或 Claude 對話當作可靠的專案代理工具。

## 貼入後，你會看到甚麼不同

- 改程式前，AI 先找相關檔案、既有規則與驗收方法。
- 研究不把估算寫成事實，會標出來源、日期、推論與未知。
- 新檔案不會擅自假定固定資料夾；先沿用專案或平台已指定的位置。
- 寫入後會讀回；出錯、中斷或衝突不能假裝成功。
- 複雜工作先做任務錨定與必要真源覆蓋；有歧義、風險或要求時才展示 🎯 層級對焦及圖表。
- 工具、沙盒、補丁或測試受阻時，AI 先診斷並確認有否半寫入，再選已授權、安全且有依據的方案；只有無法自行補齊的必要條件才交回使用者。
- 外部寫入、發佈、權限及費用等操作需要相應明確授權，有效授權不重問；本次可重建臨時產物只在完整指令的狹義例外內自行清理，機密仍須保護。
- 單檔小修保持簡短；一旦出錯會有較大影響的計劃要先經獨立反證，才可稱為可執行。
- 你不會先收到一份未查漏的半成品計劃；核心條件補不齊時，AI 會說明受阻部分及續行條件，並繼續獨立安全工作。

## 最短安裝方法

1. 複製 [prompt.md](prompt.md) 全文。
2. 先進入正確的專案／工作區。
3. 貼到你的工具用來長期套用專案指令或規則的位置，儲存後重新開任務。
4. 先用一個小工作確認：要求 AI 讀專案規則，再修正一處小錯並讀回核對。

各工具的畫面、名稱和長期指令位置會更新，請以該工具的官方當前文件或你的 Agent Handoff Kit 設定為準。

## 不會令每件事變複雜

這份指令會按工作影響決定力度。明確的小修直接完成並讀回；涉及資料、機密、公開發佈或多個互相影響的改動，才會多做必要的核對與確認。

你不需要了解背後規則怎樣整理。只要把全文貼到工具內，用一件小而真實的工作開始即可。
