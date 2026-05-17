# 02｜Claude Code Meta Instruction（含機密處理及 Windows 桌面附加）

用於 Claude Code 全域指令的治理規則集。在 [01｜Claude Cowork Meta Instruction](../01-claude-cowork-meta-instruction/) 通用骨幹之上，補入兩條 Claude Code 場景常用的附加規則：機密處理（跨作業系統通用）與 Windows 桌面破壞性命令零容忍。

> 💡 **與 01 的關係**　第一至二十節與 01 為單一真源，逐字對齊；02 僅在尾部新增第二十一、二十二節。如只需通用治理規則，套 01 已足夠；如於 Claude Code 環境用、會接觸 `.env` / credentials、或在 Windows 桌面操作 shell 命令，建議套 02。

---

## 一、指令定位

此指令的設計目的：

- 在 Claude Code 環境下沿用 01 全套通用治理規則（語言分層、合作模式、全圖優先、補丁式變更、防漂移等），無需重組或刪減。
- 補入「機密處理」規則：規範讀取 `.env` / credentials 等含機密檔案時的處理方式，避免機密值寫入 commit、issue、log 或外部請求。
- 補入「Windows 桌面破壞性命令零容忍」規則：針對 Windows 環境特有的 `cmd /c rmdir` 家族指令、磁碟根目錄誤觸風險作硬封殺。

---

## 二、適用對象

- 在 Windows 桌面執行 Claude Code 的用戶。
- 用 Claude Code 處理含 `.env` / API key / credentials 的項目，希望 AI 不複述機密值至回覆、commit、log 的用戶。
- macOS / Linux 用戶亦可使用：第二十二節（Windows 桌面附加）會自動跳過，其餘 21 節跨平台適用。
- 已熟悉 01 的用戶：本指令第一至二十節與 01 完全同源，無需重新學習；只需了解新增第二十一、二十二節即可。

---

## 三、相對 01 新增的內容

| 新增節 | 內容摘要 | 適用範圍 |
|---|---|---|
| 第二十一節 機密處理 | 讀取機密檔案時以 `<REDACTED>` 替代複述；禁將機密值寫入 commit / issue / PR / log / 新建檔案 / 外部請求；機密相關變更須明確標示「請人工檢閱」 | 跨作業系統，所有 AI Agent 環境通用 |
| 第二十二節 執行環境特定附加（Windows 桌面） | `cmd /c rmdir` 家族零容忍（含所有變體與混淆形式）；磁碟根目錄禁區（`C:\`、`D:\` 等）；引號驗證；路徑歧義時不執行 | 僅 Windows 桌面生效；macOS / Linux / 其他 AI Agent 環境自動跳過 |

第一至二十節內容與 01 完全相同，治理規則細節請見 [01 README](../01-claude-cowork-meta-instruction/README.md)。

---

## 四、新增規則的對應痛點

| 痛點描述 | 對應規則 |
|---|---|
| Claude Code 讀 `.env` 後在回覆中複述 API key、token 值，造成機密外洩風險 | 第二十一節 機密處理 |
| AI 將機密值寫入 git commit message、issue 描述、debug log，導致 history 永久留痕 | 第二十一節 機密處理 |
| 用戶要求清空空資料夾，AI 以 `cmd /c rmdir /s /q` 執行；遇路徑解析錯誤誤刪同名父層 | 第二十二節 Windows 平台破壞性命令零容忍 |
| Windows `cmd` 跳脫處理錯誤令 `"C:\Project Files"` 解析為 `C:\` 根目錄，引致系統根級誤刪 | 第二十二節 Windows 路徑安全 |
| AI 套通用 `rm -rf` 禁令時，未考慮 Windows 對應指令族（`Remove-Item -Recurse -Force`、`rd /s /q`、`cmd /c rmdir /s /q` 等）有平台特異變體 | 第二十二節 補強第二十節通用條 |

---

## 五、使用方式

### 安裝至 Claude Code（推薦）

複製本資料夾 `prompt.md` 全文，貼至：

- **全域**：`~/.claude/CLAUDE.md`（macOS / Linux）或 `C:\Users\<你>\.claude\CLAUDE.md`（Windows）
- **項目層級**：項目根目錄 `CLAUDE.md`

### 安裝至 OpenAI Codex / Amp / Cursor / Factory / Google Jules 等 AGENTS.md 標準 agent

複製 `prompt.md` 全文，貼至：

- **全域**：`~/.codex/AGENTS.md`（OpenAI Codex；其他工具參考其各自文件）
- **項目層級**：項目根目錄 `AGENTS.md`

第二十二節 Windows 桌面附加在 macOS / Linux 環境會自動跳過（節內已寫明範圍限定）。

### 安裝至 Claude Cowork

如只需通用治理規則，建議改用 [01](../01-claude-cowork-meta-instruction/)；02 第二十二節 Windows 桌面內容在 Cowork 環境無對應 shell 場景。如仍想統一用 02，貼至 Cowork Settings → Global Instructions 亦可，多出的節會自動跳過。

### 安裝至 ChatGPT / 一般 LLM 對話介面

複製 `prompt.md` 全文，貼至 Settings → Personalization → Custom Instructions 或對應自訂指令欄位。

---

## 六、選擇 01 還是 02

| 場景 | 建議 |
|---|---|
| Claude Cowork 為主、Claude Desktop / 一般對話 | 01 |
| Claude Code 為主、會接觸機密檔案 | 02 |
| Claude Code 為主、Windows 桌面用 | 02 |
| Claude Code 為主、macOS / Linux 用 | 02（第二十二節自動跳過） |
| OpenAI Codex / AGENTS.md 標準 agent | 01 或 02 皆可，視乎是否需要機密處理 + Windows 桌面附加 |
| 純對話介面（ChatGPT 等），無檔案系統存取 | 01 |

---

## 七、維護與同步說明

第一至二十節以 [01 prompt.md](../01-claude-cowork-meta-instruction/prompt.md) 為單一真源，02 維護時必須與 01 逐字對齊；如 01 後續升版（加新規則、改條款編號等），02 第一至二十節同步更新，避免跨檔漂移。第二十一、二十二節為 02 獨有，獨立維護。

---

## 八、回饋與授權

- **授權**：MIT 授權；詳見 repo 根目錄 [LICENSE](../../LICENSE)。
- **回饋**：發現規則描述有誤、有可改進之處、或有其他 Claude Code 場景痛點可補充，歡迎提交 Issue 或 Pull Request 至 [repo](https://github.com/prompt-templates/Adam-AI-Instructions)。
- **免責**：所有指令源於個人使用經驗，實際效果視乎所用 AI 模型版本、工具更新狀態、用戶使用習慣而異；請自行驗證後使用。
