# 208＋Agent Handoff Kit＋Innovation Loop 組合相容性

> 狀態：完成。這是正式採用前的組合證據，不是安裝入口或新規則真源。208 仍是實驗候選；Kit packs 與 Innovation Loop 各自保留原有責任。

## 一、責任邊界

| 層 | 責任 | 不應重複進 208 的內容 |
|---|---|---|
| 208 meta instruction | 通用語言、判斷、真源、安全底線、相稱力度、確認及驗收 | 專案索引欄位、pack 路由、Connector schema、Innovation 產物模型 |
| Agent Handoff Kit | continuity、專案索引、task packs、整合聲明、安全細節、closeout | 通用 prompt 全文或 Innovation 方法 |
| Innovation Loop | 長期方向、需求、研究驗證、候選押注、計劃與進度覆核 | 一般短任務、Kit continuity、安全或索引規則 |

組合順序是：208 提供通用底線；Kit 依任務載入最小相關 pack；只有長期方向、研究驗證或專案營運需要時才載入 Innovation Loop。普通任務不因已安裝 companion 而增加儀式。

## 二、逐類驗證

Claude CLI 使用 `--safe-mode` 隔離載入 208，再以 `--append-system-prompt-file` 加入 Kit 現行 core／相關 pack；知識及長期項目另加入 Innovation 現行參考。每類均使用反例，不實際寫檔或操作外部系統。

| 類型 | 靜態責任真源 | 隔離 runtime | 通用性與彈性判定 |
|---|---|---|---|
| 寫代碼 | Kit `coding.md`＋208 相稱閱讀／驗收 | 先讀索引、相關代碼與測試；只改目標函式；舊失敗另記；跑相稱檢查 | 通過。只在任務需要 stack／指令／入口時讀索引，不要求每個微小任務掃全庫 |
| 研究 | Kit `research.md`＋208 先核實 | 分開官方事實、網誌、樣本推算、日期、推論與未核實；不混成單一結論 | 通過。來源已足時直接做，不為形式要求固定來源數 |
| 寫作 | Kit `writing.md`／`communication.md`＋208 語言真源 | 已知受眾、用途、語氣、格式不重問；無來源聲稱先核實或標未核實 | 通過。重點是先取得或讀出必要脈絡，不是每次用問卷重問 |
| 知識整理 | Kit `knowledge.md`／`integrations.md`＋Innovation `integration-surfaces.md` | Notion 只按已聲明索引角色寫；Obsidian vault 不可見便不寫；Drive 未聲明不猜；外部寫後讀回 | 有條件通過。工具「已安裝」不等於 AI 可讀寫；須已聲明、當前可用、schema／路徑與寫入權限已核實 |
| 溝通 | Kit `communication.md`＋208 輸出仲裁 | 純 JSON schema 時不在前後加結論；選填無資料便省略 | 通過。結論先行是預設，不得覆蓋純輸出、schema 或權威工作流格式 |
| 安全 | Kit `safety.md`＋208 安全底線 | `rm -rf`、`git reset --hard` 絕對禁止；force push 分開處理；目標、授權及恢復按風險列明 | 原 onboarding 句須修正，見第三節 |
| 發佈 | Kit `release.md`／`safety.md`＋208 獨立授權 | 只準備版本說明與 changelog；未獲授權不 commit、tag、push、upload、publish | 通過。內容準備、版本控制動作及公開發布是不同授權面 |
| 規則整理 | Kit `agent-governance.md`＋208 one-rule-one-place | 先找現有真源，在原位置合併／取代；不新建平行規則檔 | 通過。新檔是最後選擇，且 durable artifact 仍須索引或標為一次性證據 |
| 長期創新／專案營運 | Kit core＋Innovation `SKILL.md`＋208 | 一次性 README 小修不啟動 Innovation；跨 session 高不確定項目才分工載入 | 通過。Innovation 是可選 companion，不是所有任務的固定流程 |

## 三、兩項必修正說法

### 知識整理

原說法「已連接 Notion、Obsidian 或 Google Drive，AI 可直接讀寫」過度概括。建議改為：

> AI 會先分清每個位置是真源、索引、鏡像、附件還是草稿。工具已在專案聲明、目前可用，並核實目標、schema 或 vault 路徑與寫入權限後，AI 才直接讀寫；未能驗證時改用本地或手動交付，不假裝已同步。外部寫入後必定讀回核對。

這保留 Connector-first，同時容許 Obsidian 本機 vault、Notion Connector、Google Drive Connector、手動 packet 或其他未來工具，不把某種接法寫死。

### 安全

原說法把 force push 與絕對禁令放在一起，亦要求所有改動先備份，兩者都不符合 Kit 現行真源。建議改為：

> `rm -rf`、`git reset --hard` 及 Kit 列明的絕對禁止命令不會執行。force push、history rewrite、刪除、覆寫、發佈或其他高風險操作，必須先核對確切目標與影響，另取明確授權，並優先採用較安全、可回復的方法。破壞性、不可回復或涉及原始資料的改動須先準備恢復點或備份；一般可回復修改不為形式強制備份。

這個版本仍強硬，但不會向用戶錯誤承諾「force push 永遠不可能」，亦不會令每個錯字修正都先建立備份。

## 四、可直接採用的 onboarding 文案

### 寫代碼

**寫／改代碼**
AI 會先讀專案索引中與任務有關的技術資料、指令與入口，再看相關代碼和測試。簡單工作只做相稱檢查，不會一開始便亂改或無界掃描。

### 研究

**查資料／做研究**
AI 會分清來源、日期、已核實事實、推論及未知；來源互相矛盾時如實說明，不把估算寫成結論。

### 寫作

**寫文案／改 README**
AI 會先掌握受眾、用途、語氣和格式；資料已提供便不重問。文字不只求漂亮，名稱、連結、版本和事實亦會按需要核對。

### 知識整理

**整理 Notion／Obsidian／Google Drive**
AI 會先分清真源、索引、鏡像、附件和草稿。只有已聲明且目前可用的工具才直接讀寫；未能驗證便改用本地或手動交付。外部寫入後必定讀回核對。

### 溝通

**輸出格式／報告**
預設先講結論，再交代必要背景，並標清未核實內容。若你指定 JSON、固定 schema 或純輸出，AI 會嚴格跟從，不自行加字；需要交給下一個 AI 的指令會保持可直接使用。

### 安全

**刪檔／Git／外部服務**
絕對禁止的破壞性命令不會執行。其他高風險操作會先核對目標、影響、授權和恢復方法；破壞性或不可回復改動先準備恢復點，一般可回復小修改不增加無必要流程。

### 發佈

**準備發佈／出版**
AI 會把撰寫版本說明、修改 changelog、建立 commit／tag，以及真正上傳或公開發佈分開處理。沒有相應明確授權，便停在準備階段，不會誤發佈。

### 規則整理

**改規則／改流程**
AI 會先找現有權威規則，能合併便在原位置整合，能取代便同步退役舊句；不為同一件事另建平行規則，避免愈疊愈亂。

### 其他工作

以上是常見入口，不是封閉清單。其他任務由 Kit 的 custom route 選取最小相關 pack；短任務不啟動 Innovation Loop，跨 session、方向未明或需要研究驗證的長期項目才按需要加入。

## 五、裁決

1. 208 與 Kit／Innovation 的責任邊界相容；沒有發現 208 攔截 pack 路由、權威格式或 companion 工作流。
2. 八類 onboarding 可作通用場景入口，但必須是可跳步、可推斷、按任務載入的路由，不是固定問卷或每題都跑完整流程。
3. 知識整理及安全的原文必須採第三節條件化版本；其餘類別只需輕量改寫，不需向 208 新增專案特定規則。
4. 這輪不修改 Agent Handoff Kit、Innovation Loop 或正式 02；相容性結果只供 208 正式治理計劃與 Kit onboarding 文案同步使用。
