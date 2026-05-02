# Changelog

本資料庫的所有重要變更皆記錄於此檔案。

格式參考 [Keep a Changelog](https://keepachangelog.com/zh-TW/),版本號採用 [Semantic Versioning](https://semver.org/lang/zh-TW/)。

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
