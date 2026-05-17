# Changelog

本資料庫的所有重要變更皆記錄於此檔案。

格式參考 [Keep a Changelog](https://keepachangelog.com/zh-TW/),版本號採用 [Semantic Versioning](https://semver.org/lang/zh-TW/)。

---

## [0.6.0] - 2026-05-17

### 新增

新增第二份 prompt `02-claude-code-meta-instruction/`，定位為 Claude Code 全域指令版本，相對 01 補入兩條 Claude Code 場景常用的附加規則：

- **痛點一**：Claude Code 常處理含 `.env` / credentials / API key 的項目，AI 預設可能在回覆、git commit message、issue 描述、log 檔中複述機密值，造成不可逆的外洩。01 通用治理規則未直接覆蓋此場景。
- **痛點二**：Windows 環境下 `cmd /c rmdir` 家族指令、磁碟根目錄解析陷阱（引號處理錯誤令 `"C:\Project Files"` 解析為 `C:\`、環境變數展開出意外結果等）容易造成 catastrophic deletion。01 第二十節通用條已禁 `rm -rf` + 禁外部殼層執行檔案系統修改，但 Windows 平台特異變體值得獨立硬封殺。

### prompt 02 結構

- **第一至二十節**：與 01 [`prompt.md`](prompts/01-claude-cowork-meta-instruction/prompt.md) 為單一真源，逐字對齊；01 後續升版時 02 同步更新。
- **第二十一節 機密處理**：OS-agnostic 全平台通用；讀取機密檔案時以 `<REDACTED>` 替代複述、禁將機密值寫入 commit / issue / PR / log / 新建檔案 / 外部請求、機密相關變更須明確標示「請人工檢閱」。
- **第二十二節 執行環境特定附加（Windows 桌面）**：僅 Windows 桌面生效；`cmd /c rmdir` 家族零容忍（含所有混淆變體）+ 磁碟根目錄禁區 + 引號驗證 + 路徑歧義時不執行；macOS / Linux / 其他 AI Agent 環境自動跳過。

### 三件套齊備

- [`prompts/02-claude-code-meta-instruction/prompt.md`](prompts/02-claude-code-meta-instruction/prompt.md) — Prompt 原文，可直接複製貼至 `~/.claude/CLAUDE.md` 全域或項目根目錄 `CLAUDE.md`
- [`prompts/02-claude-code-meta-instruction/README.md`](prompts/02-claude-code-meta-instruction/README.md) — 文字介紹頁，說明痛點、規則、01 vs 02 如何選用
- [`prompts/02-claude-code-meta-instruction/guide.html`](prompts/02-claude-code-meta-instruction/guide.html) — 互動式 HTML 指南，含 SVG 視覺化說明 02 vs 01 差異

### root README 同步

- 第五節 Prompt 索引表加 02 行 + 加「01 vs 02 怎麼選」提示。
- 第六節 最近更新表加 v0.6.0 行。

### 適用對象擴展

- Claude Code 用戶（Windows / macOS / Linux 皆適用，Windows 桌面附加為條件式生效）
- OpenAI Codex / AGENTS.md 標準 agent 用戶（亦適用 02，視乎是否需要機密處理 + Windows 桌面附加）
- 已套 01 但想補入機密處理規則的用戶（可單獨抽取 02 第二十一節貼至 01 之後）

### 對應的用戶感受變化

套用 02 後：

- AI 讀 `.env` 後不再在回覆中複述具體 API key 值，改以 `<REDACTED>` + 「見 .env 第 N 行」表達。
- AI 不再建議將機密值寫入 git commit message、issue / PR 描述、log 檔、新建檔案。
- Windows 桌面下 AI 不再用 `cmd /c rmdir /s /q` 系列指令清理目錄，改用 native PowerShell / 工具原生 API；遇路徑解析歧義時主動停手不執行。
- macOS / Linux 用戶套 02 亦可使用，第二十二節 Windows 附加會自動跳過，其餘 21 節跨平台適用。

---

## [0.5.1] - 2026-05-16

### Hotfix

修正 v0.5.0 名實不一致 bug：

- **痛點**：v0.5.0 第二十節已 retitle 為「執行環境補充（Cowork / Codex / 同類 AI Agent 通用）」並補咗 Codex 安裝段，但主標題「# Claude Cowork 全域指令」仍 hardcode "Cowork"，同跨工具通用聲明矛盾。用戶 catch 到呢個 inconsistency，屬 v0.5.0 release 嘅 QC gap（淺層 marker check 過關但 cross-tool 一致性 audit 漏咗）。

### 修正

- **prompt.md 主標題** retitle 為「AI Agent 全域指令（Claude Cowork / OpenAI Codex / AGENTS.md 標準通用）」— 主標題層 cross-tool 統一。
- **prompt.md 第二十節第 15 條**「如在 Cowork Project 內則加持久化（更新 Project memory）」改 generic：「如環境支援 project / workspace 持久化（如 Cowork Project、Codex Project 等）則加持久化階段更新對應 memory」。
- **prompts/01 README 第七組描述** sync：章節名由「Cowork 環境特殊規則(A-F)」改為「執行環境特殊規則(Cowork / Codex / 同類 AI Agent 通用)」；涵蓋原文段落 reference 由「Cowork 專屬補充 A-F」改為「第二十節 執行環境補充」；適用對象描述補 OpenAI Codex / Amp / Cursor / Factory / Google Jules 等 AGENTS.md 標準 agent。
- **prompts/01 README 四階段工作流** 「Cowork Project 內加 PERSIST」改 generic：「環境支援 project / workspace 持久化時加 PERSIST，如 Cowork Project、Codex Project 等」。

### 治理層教訓（記錄入本 changelog 作 reference）

- v0.5.0 release 嘅 QC 階段只 check 個別 markers（創作豁免、執行硬規則、第二十節 retitle）嘅命中，**跳過咗全文一致性 audit**（主標題 vs 章節名 cross-tool 對齊）。
- 屬本 prompt 自身嘅「先讀後判」第 7 條（違反一條 = 當次判斷視為未成立）+「治理改動先審核」第 5 點（漂移風險評估）嘅 enforcement gap 活樣本。
- 同一討論串內已有第二次 QC 漏（之前 PowerShell line count 陷阱 + 今次主標題矛盾），按本 prompt 規則「升級為用戶明示介入」處理。

---

## [0.5.0] - 2026-05-15

### 改善

針對三類痛點作規則加固 + 結構緊湊化 + 跨工具兼容：

- **痛點一**：v0.4.0 對 creative / graphic design / story writing 等任務不友善——AI 為畫一張海報出五區段表格、為寫一首詩切「規劃→閱讀→修改→品質檢查」四階段、回覆骨架硬塞「🔎重點 + 交付清單」把抒情文變 to-do list。
- **痛點二**：AI 經常用「§3 / §1 / §12」呢類條款編號做句子主體叫用戶選擇，用戶無法一眼讀懂；雖 v0.4.0 已寫「不做句子主體」嘅 principle，但執行未夠硬。同類問題：回覆骨架（三行🔎重點 + 交付清單）係預設但 AI 經常省略，尤其長篇結構性報告場景。
- **痛點三**：本指令原意設計給 Claude Cowork，但 OpenAI Codex / Amp / Cursor / Factory / Google Jules 同樣採用 AGENTS.md 標準作 custom instruction 入口，本 prompt 95%+ 可直接通用，但 v0.4.0 章節名 hardcode "Cowork" 並無明文表態 cross-tool 兼容。
- **痛點四**：v0.4.0 整 296 行，部分研究指 meta instruction sweet point 約 200 行；雖未到 200，可透過內容緊湊化、合條、壓 sub-bullets 縮減認知負載。

### 新增

第一份指令 `01-claude-cowork-meta-instruction/prompt.md` 升級：

- **個人偏好** 加「創作類任務例外」一段：設計、故事、詩、廣告文案、純想像、虛構等不以事實可驗收為目標嘅任務，自動豁免全圖優先五區段、回覆骨架硬骨幹、四階段工作流、計算四步法、可量指標／驗收條件；語言分層、合作模式、用語紀律、回覆語體仍適用。
- **第六節下一步選擇題格式 bug 修正**：v0.4.0 嘅 quote block 連續 `>` 行冇 blank line 分隔，markdown render 結果 A/B/C 黐埋同一 paragraph；新版每選項之間加 `>` blank line 強制段落分隔。
- **第十七節用語紀律**加「執行硬規則」(a)(b) 兩條：條款編號必須前置中文白話描述對應事實，編號只可放括號或行尾次要標註；任何回覆必須啟動第五節回覆骨架（開首三行🔎重點 + 交付清單）；違反任一即當下 self-flag 改寫，不視為「下次注意」。
- **第二十節 retitle** 為「執行環境補充（Cowork / Codex / 同類 AI Agent 通用）」——明文宣示 cross-tool 兼容；prompts/01 README 安裝段同步補 OpenAI Codex 條目（`~/.codex/AGENTS.md` 全域 / 項目根 `AGENTS.md`）。

### 結構整理

- **整體緊湊化**：v0.4.0 296 行 → v0.5.0 248 行（-48 / -16.2%）；保所有規則內容、保 markdown 慣例；主要 saving 來自第十一節合「四類捷徑」單條、第十二節合 6 點自檢 inline、第十三節補丁式 8 bullets → 5、第二十節 22 條合 19 條（同類條合句）、第三節「不觸發」「觸發時禁止」list 緊湊化、反正例由 4 例壓 2 例。

### 對應的用戶感受變化

套用本版本後：

- 叫 AI 處理創作類任務（畫海報、寫詩、寫故事、廣告文案）時，AI 唔再硬塞五區段表格 / 四階段工作流 / 計算四步法；保留語言分層、合作模式、用語紀律。
- 揀 AI 嘅選擇題 (A/B/C) 時，每個選項分行清晰，唔再黐埋同一段。
- AI 用條款編號（§3 / §12 等）時，必先有中文白話描述對應規則，編號只放括號附註；違反即改寫。
- AI 任何回覆都會啟動「🔎重點 + 交付清單」骨架，唔再 long-form report 跳過骨架直入正文。
- 本指令明文兼容 OpenAI Codex / Amp / Cursor 等採用 AGENTS.md 標準嘅 AI agent，可放 `~/.codex/AGENTS.md` 全域或項目根 `AGENTS.md`。
- 整份 prompt.md 由 296 行壓至 248 行，AI 載入時 token saving + 認知負載降低。

---

## [0.4.0] - 2026-05-15

### 改善

針對指令結構嘅可讀性與規則收歸做一次大整理：

- **痛點一**：v0.3.0 用「【】」+ 漢字序號嘅章節格式，視覺上唔似標準 Markdown 文件；讀者掃文件、揾規則、引用章節時要逐段眼掃，無清晰嘅二級／三級階層。
- **痛點二**：「事實核對」「禁止憑記憶推斷」「禁止用代理訊號代替全貌」呢類關於「先驗證再判斷」嘅精神，散佈於三個位置（獨立章節、全圖優先規則、Cowork 補充 11C），冇統一上位定義；新規則一加就容易撞舊句、口徑漂移。
- **痛點三**：「治理改動先審核」呢類關於計劃自檢、強制只讀審核、唔可以把「填滿格式」當「已審核」嘅精神，v0.3.0 散佈於全圖優先規則內嵌段 + Cowork 補充 11D／11E／14A 三個 sub-letter 編號，難引用、難維護。

### 新增

第一份指令 `01-claude-cowork-meta-instruction/prompt.md` 升級結構：

- **整體 Markdown 階層化**：由「【】+ 漢字序號」格式轉為標準 Markdown `#`／`##`／`###` 階層；新增「# Claude Cowork 全域指令」主標題與「## 個人偏好」獨立小節。
- **章節重新編號**：採用「## 一、二、三、…」中文漢字序號二級標題，全文 20 個一級規則章節順序固定。
- **新增「## 十一、先讀後判（核心規則）」上位章節**：把 v0.3.0 嘅「事實核對」「禁止憑記憶推斷」精神升為上位核心，並新加五條：
  - 禁止用代理訊號代替全貌（版本控制改動時間、檔頭一句、搜尋命中次數、狀態檔自述不可當作「內容是否最新／正確／過期」嘅判斷依據）
  - 禁止用產出代替思考（未想清楚問題本質前，不可用「先提一個方案／先列選擇題／先交一份東西」迴避思考）
  - 用戶質疑視為「我此刻可能正用捷徑」嘅信號（必停下、真驗證，不換個方向再做同類片段式處理）
  - 由基礎做起、逐步推進、每步驗證穩固才繼續（不一次提大計劃／大批改動衝落去）
  - 違反任何一條：當次判斷視為未成立，回到真讀／真驗證重做
- **新增「## 十二、治理改動先審核（核心規則）」上位章節**：把 v0.3.0 全圖優先規則內嵌嘅計劃自檢段 + Cowork 補充 11D／11E／14A 收歸統一上位定義，並補入「規劃階段不得把『看似可執行』當成『已審核』」一句作 anti-shortcut 紅線。
- **Cowork 補充重整**：原 11A／11B／11C／11D／11E、14A 等 sub-letter 編號併入第十一節／第十二節後，Cowork 補充改用 sequential 1-22 編號；並加第 14 條交叉引用句：「一切判斷、分析、事實確認、改檔前閱讀的處理，統一依第十一節。一切『治理／長期／跨檔／外部平台』類改動的審核強度判斷，統一依第十二節。本節不再重複此兩條核心精神。」
- **「忌長篇大論、忌片斷語」加入「## 個人偏好」首句**：明確語氣偏好。
- **「## 十九、防漂移」維持核心規則地位**：章節編號重整後保留為十九，內容微調確認。

### 對應的用戶感受變化

套用本版本後：

- 揭開 prompt.md，章節階層一眼睇晒，揾規則同引用唔再要逐段眼掃。
- AI 處理任何「先讀後判」相關場景（事實核對、改檔前讀、判斷檔案狀態、回應用戶質疑）時，會引一個統一上位章節，不再喺三個位置撞口徑。
- AI 處理治理層任務嘅計劃自檢、強制只讀審核，由獨立上位章節定義，新規則加入時更易合併、退役舊句。
- AI 處理 Cowork 環境特殊任務（檔案系統、層次分類、變更前置、外部平台、工作流、範圍）時，編號連續、無 sub-letter，引用更直接。

---

## [0.3.0] - 2026-05-13

### 改善

針對一個治理層常見痛點作規則加固:

- **痛點**:用戶提出涉及治理規則、長期流程、跨檔同步、公開輸出邊界等任務時,AI 直接出修改計劃,把「填滿格式」當成「已充分審核」;結果第一份全圖計劃要求改檔案,但實際 AI 仍未真正看清同主題真源、漂移風險、閱讀覆蓋是否足夠。等於把問題包裝進計劃格式中推給用戶批准。

### 新增

第一份指令 `01-claude-cowork-meta-instruction/prompt.md` 強化「全圖優先規則」與「Cowork 補充」:

- 開首加上**用戶身份宣告**:「我不是開發人員,不堆砌技術詞與編號,跟我用日常話溝通」,讓 AI 從一開始即知道對方非技術用戶,避免堆砌術語。
- 全圖優先規則 加 **計劃自檢機制**:觸發後輸出 5 區段之前必先完成 6 項自檢(層次屬產品系統抑或治理、是否應先只讀審核、是否已有同主題真源、是否有不改檔即可達標的正路、漂移風險、閱讀覆蓋)。
- 全圖優先規則 加 **強制只讀審核**:涉及治理文件、安全規則、長期流程、標準作業流程、跨檔同步、公開輸出邊界、外部平台、跨真源任務時,第一份全圖計劃須以「只讀審核」作第一階段,不得預設一定會修改檔案。
- 「觸發時禁止」清單加兩條:在未完成計劃自檢前把第一份全圖寫成必然修改檔案的方案;在治理、安全、長期規則或跨真源任務中省略只讀審核階段而直接進入補丁。
- Cowork 補充「三、變更前置」加兩條紅線:
  - **11D** — 對治理文件、規則、安全、長期流程、標準作業流程、技能檔、公開輸出邊界或跨檔同步提出計劃前,必先完成計劃自檢。
  - **11E** — 若計劃自檢顯示資料未讀夠,第一份計劃只能是閱讀／審核計劃,不可包裝成修改或落地計劃。
- Cowork 補充「五、工作流與風險」加 **14A**:規劃階段不得直接把「看似可執行」當成「已審核」;涉及治理、安全、長期流程、跨檔同步、公開輸出、外部系統或三個以上檔案,必先把計劃設為只讀審核或分階段 gate。

### 對應的用戶感受變化

套用本版本後:

- 向 AI 提涉及治理規則、長期流程、跨檔修改的任務時,AI 不會跳過審核直接出修改計劃;會先審核確認漂移風險、同主題真源、閱讀覆蓋,再決定是否修改。
- 若資料未讀夠,AI 第一份計劃會是「閱讀或審核計劃」,不會包裝成修改計劃讓用戶誤批准。
- AI 不會把「填滿 5 區段格式」當成「已充分審核」;反而會自己先走 6 項自檢,自檢通過先輸出計劃。

---

## [0.2.0] - 2026-05-11

### 改善

針對兩個常見痛點作規則加固:

- **痛點一**:用戶問 AI「再 audit 一下,最佳選項是什麼」時,AI 可能基於新角度重新評估、得出不同推薦但不解釋為何前推薦失效,令用戶分不清前後哪個可信。
- **痛點二**:AI 為解當前 session 問題而草率新建臨時檔案、不查 sessionlog、靠盲猜推斷,等於把問題推延至下一 session,日後越變越複雜難解。

### 新增

第一份指令 `01-claude-cowork-meta-instruction/prompt.md` 新增四條規則:

- 「下一步選擇題」區段尾部加一條:**審計或覆核時若推薦變更,必須在新推薦旁明示原推薦的缺陷或失效點作對應對照;無缺陷則維持原推薦不變,不憑新角度而動搖。**
- Cowork 補充「三、變更前置」加三條紅線:
  - **11A** — 修改前必查當前 session 的 sessionlog 或同類前例,明示參照來源;無前例則明寫「無前例」並列關鍵假設。
  - **11B** — 禁止為解當前 session 問題而新建臨時檔案;新建檔案前必先檢查是否可改既有檔案,無可改才新建並說明原因。
  - **11C** — 禁止憑記憶推斷項目結構、檔案內容、規則細節、外部平台行為;必先讀證實,未證實即視為未核實。

### 對應的用戶感受變化

套用本版本後:

- 向 AI 提「audit 一下」「覆核一下」「最佳選項是什麼」這類問題時,AI 不會無理由變心;若推薦真要變,AI 會逐項講清原推薦哪裡失效。
- AI 不會為解眼前一個小問題而隨手新建檔案,把長期項目搞得越來越亂。
- AI 不會憑記憶亂答項目內結構或檔案內容,會先讀檔案確認。

---

## [0.1.0] - 2026-05-02

### 初始發佈

首次公開發佈。本資料庫旨在收錄個人於日常使用 AI 工具(Claude Cowork、Claude Code、ChatGPT 等)累積的治理指令(Meta Instructions)。

### 新增

- 主 README:介紹本資料庫的定位、適用對象、目錄結構、使用方式、Prompt 索引、授權與貢獻。
- 首份 Meta Instruction:`01-claude-cowork-meta-instruction`,完整集合包含三個檔案:
  - `prompt.md`:Prompt 原文,可直接複製使用。範例已涵蓋 Windows 與 macOS / Linux 雙平台。
  - `README.md`:文字介紹頁,將原文約 19 個規則塊歸納為 7 大組,每組以「對應問題、規則內容、治理作用、適用情景」四個切面說明。
  - `guide.html`:互動式 HTML 指南,含 6 個 SVG 視覺化(合作模式對比、FPFR 觸發判斷與 5 區段、補丁式變更結構、防漂移對比、計算四步法、四階段工作流)。
- `.gitignore`:忽略 macOS、Windows、Linux 系統檔案與常見編輯器產生的暫存檔。
- `CHANGELOG.md`:本檔案。

### 規則範圍(7 大組)

1. **哲學基礎**:偏好優先序、合作模式核心規則、核心原則。
2. **全圖優先規則(FPFR)**:多檔案 / 規則改動前先輸出 5 區段執行計劃。
3. **日常回覆品質**:回覆骨架、選擇題格式、語氣與用語紀律、語體一致、輸出控制。
4. **準確性護欄**:事實核對、SSOT 對齊、歧義處理。
5. **變更治理**:補丁式(Patch-only)變更、深度修補、防漂移、格式硬規則。
6. **計算規範**:四步法(逐位計算、判正負、展示步驟、代回驗算)。
7. **Cowork 環境特殊規則**:檔案系統與破壞性操作、層次分類、變更前置、外部平台與 API、工作流與風險、範圍與相容性。

### 跨平台相容性

本指令已通過 Windows 與 macOS / Linux 雙平台例子覆蓋驗證:

- 破壞性指令清單同時涵蓋 PowerShell(`Remove-Item -Recurse -Force`)與 POSIX shell(`rm -rf`)。
- 路徑 API 例子涵蓋 .NET、Node.js、Python、PowerShell、Bash / Zsh、Java、Go。
- 預設輸出目錄 `outputs/` 使用正斜線書寫,於兩大作業系統皆可解析。
