# AI Agent Markdown — 多平台 Sub-Agent 範本集

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-CLI-orange)](https://github.com/anthropics/claude-code)
[![GitHub Copilot CLI](https://img.shields.io/badge/GitHub%20Copilot-CLI-blue)](https://github.com/features/copilot)
[![Gemini CLI](https://img.shields.io/badge/Gemini%20CLI-Google-green)](https://github.com/google-gemini/gemini-cli)

> **一句話串聯所有功能：** 只需將這五份 agent markdown 部署至相容的 AI CLI（Claude Code／GitHub Copilot／Gemini），AI 即可自動編排一條完整的開發品質流水線——**程式碼審查 → 資安工程師 → 效能優化 → 文件撰寫 → 惡意軟體分析**——五位專業 sub-agent 各司其職、依關鍵字自動觸發、接力協作，確保每一次程式碼變更都經過審查、強化、優化、記錄與威脅掃描，全程零人工干預。

---

## 目錄

- [這是什麼？](#這是什麼)
- [專案結構](#專案結構)
- [快速開始](#快速開始)
- [五大 Agent 一覽](#五大-agent-一覽)
- [各 Agent 詳細說明](#各-agent-詳細說明)
  - [1. Senior Code Reviewer — 資深程式碼審查員](#1-senior-code-reviewer--資深程式碼審查員)
  - [2. Security Engineer — 資安工程師](#2-security-engineer--資安工程師)
  - [3. Performance Optimizer — 效能優化工程師](#3-performance-optimizer--效能優化工程師)
  - [4. Documentation Writer — 技術文件工程師](#4-documentation-writer--技術文件工程師)
  - [5. Malicious Software Analysis — 惡意軟體分析師](#5-malicious-software-analysis--惡意軟體分析師)
- [`tools` 參數名稱從何而來？](#tools-參數名稱從何而來)
  - [Claude Code CLI](#claude-code-cli)
  - [GitHub Copilot CLI](#github-copilot-cli)
  - [Gemini CLI](#gemini-cli)
- [Multi-Agent 流水線架構](#multi-agent-流水線架構)

---

## 這是什麼？

本 Repository 提供適用於三大 AI CLI 平台的 **AI sub-agent 定義檔案**，每個 agent 都是一份帶有 YAML frontmatter 標頭的 Markdown 檔案，用來告訴 AI CLI：

| Frontmatter 欄位 | 用途 |
|-----------------|------|
| `name` | Agent 的唯一識別名稱 |
| `description` | **何時自動觸發**（關鍵字觸發機制） |
| `tools` | 此 agent 被授權使用哪些內建工具 |
| `model` | 指定使用哪個 AI 模型 *（Gemini CLI / Claude Code）* |

YAML frontmatter 之後是 agent 的系統提示詞（system prompt），定義了角色身份、逐步執行流程與結構化輸出格式。

**安裝一次 → AI CLI 立即獲得五位專業協作夥伴**，在每次程式碼變更時自動審查、強化、優化、記錄並掃描威脅。

---

## 專案結構

```
agents-markdown/
│
├── claude-code-cli/
│   └── agents/
│       ├── senior-code-reviewer.md          # 程式碼審查（SOLID/DRY/KISS）
│       ├── security-engineer.md             # OWASP + CVE 資安稽核
│       ├── performance-optimizer.md         # 時間複雜度 + 程式碼品質
│       ├── documentation-writer.md          # 行內註解 + 文件同步
│       └── malicious-software-analysis.md   # SAST + 惡意軟體偵測
│
├── github-copilot-cli/
│   └── agents/
│       ├── senior-code-reviewer.agent.md
│       ├── security-engineer.agent.md
│       ├── performance-optimizer.agent.md
│       ├── documentation-writer.agent.md
│       └── malicious-software-analysis.agent.md
│
└── gemini-cli/
    └── agents/
        ├── senior-code-reviewer.md          # 程式碼審查（SOLID/DRY/KISS）
        ├── security-engineer.md             # OWASP + CVE 資安稽核
        ├── performance-optimizer.md         # 時間複雜度 + 程式碼品質
        ├── documentation-writer.md          # 行內註解 + 文件同步
        └── malicious-software-analysis.md   # 完整 SAST，使用 Gemini 2.5 Pro
```

---

## 快速開始

### Claude Code CLI

```bash
# 全域安裝（所有專案皆可使用）
cp claude-code-cli/agents/*.md ~/.claude/agents/

# 專案範圍安裝
cp claude-code-cli/agents/*.md /path/to/your/project/.claude/agents/
```

### GitHub Copilot CLI

```bash
# 全域安裝（所有專案皆可使用）
mkdir -p ~/.copilot/agents
cp github-copilot-cli/agents/*.agent.md ~/.copilot/agents/

# 專案範圍安裝
mkdir -p /path/to/your/project/.github/agents
cp github-copilot-cli/agents/*.agent.md /path/to/your/project/.github/agents/
```

### Gemini CLI

```bash
# 全域安裝
mkdir -p ~/.gemini/agents
cp gemini-cli/agents/*.md ~/.gemini/agents/
```

安裝完成後，agents **自動啟動**，無需手動呼叫。AI CLI 會將對話情境與每個 agent 的 `description` 欄位進行關鍵字比對，自動派遣對應的專家。

---

## 五大 Agent 一覽

| Agent 名稱 | 角色身份 | 自動觸發關鍵字 | 主要產出 |
|-----------|---------|--------------|---------|
| `senior-code-reviewer` | 首席工程師，35+ 年資歷 | 程式碼寫入／修改／review | 問題清單 + 重構後程式碼 |
| `security-engineer` | 資安工程師，35+ 年資歷 | 程式碼變更、`OWASP`、`XSS`、`SQL`、`token` | 漏洞報告 + 修補後程式碼 |
| `performance-optimizer` | 效能品質工程師 | `optimize`、`slow`、`bottleneck`、`complexity` | 複雜度分析 + 優化後程式碼 |
| `documentation-writer` | 技術文件工程師 | 程式碼定稿、`document`、`annotate`、`explain code` | 行內註解 + README 同步 |
| `malicious-software-analysis` | 網路安全研究員 | `malware`、`backdoor`、`supply chain`、`scan` | SAST 報告 + 修復清單 |

---

## 各 Agent 詳細說明

### 1. Senior Code Reviewer — 資深程式碼審查員

```yaml
name: senior-code-reviewer
tools: Read, Glob, Grep                              # Claude Code
tools: read, search                                  # GitHub Copilot CLI
tools: read_file, glob, search_file_content          # Gemini CLI
```

**角色身份：** 擁有 35+ 年資歷的首席軟體工程師（Principal Software Engineer）。

**觸發時機：** 任何程式碼寫入或修改後自動觸發，或當對話中出現 `review`、`best practice`、`quality` 等詞彙時。

**功能說明：**
對每一個被修改的檔案執行全面程式碼審查。從副檔名自動偵測專案語言，並套用對應的語言規範。

**審查清單：**

| 類別 | 審查內容 |
|------|---------|
| 架構原則 | SOLID、DRY（禁止重複邏輯）、KISS（優先選擇簡單方案）、YAGNI（禁止臆測性程式碼） |
| 語言慣例 | Go：error wrapping / context 傳遞；TS：strict mode / 禁 `any`；Python：type hints / PEP 8 |
| 反模式偵測 | 上帝函式（>40 行）、魔法數字、死程式碼、隱性耦合、深度巢狀（>3 層） |
| 命名規範 | 僅允許自我說明式命名——禁止 `x`、`tmp`、`data`、`res`、`obj` |

**輸出格式：**
```
## Code Review Report

### Issues Found
| File | Line | Severity (HIGH/MED/LOW) | Issue | Fix |
|------|------|--------------------------|-------|-----|

### Refactored Code
[修正後的程式碼與說明]
```

---

### 2. Security Engineer — 資安工程師

```yaml
name: security-engineer
tools: Read, Write, WebSearch, WebFetch, Bash, Glob, Grep                               # Claude Code
tools: read, edit, search, execute, web                                                  # GitHub Copilot CLI
tools: read_file, write_file, glob, search_file_content, run_shell_command, google_web_search, web_fetch  # Gemini CLI
```

**角色身份：** 擁有 35+ 年資歷的資深資訊安全工程師（Senior Information Security Engineer）。

**觸發時機：** 任何程式碼變更後，以及對話中出現 `security`、`vulnerability`、`CVE`、`OWASP`、`injection`、`XSS`、`auth`、`SQL`、`token`、`password` 等詞彙時。

**功能說明：**
每次執行前，先即時抓取**當前年度**的 OWASP Top 10、CWE 弱點分類與最新 CVE，再將每個函式與相依套件逐一對照。絕不使用快取或硬編碼的安全參考資料。

**四步執行流程：**

| 步驟 | 動作 |
|------|------|
| 1 | **即時抓取安全參考資料** — OWASP Top 10（當年度）、CWE、CVE 資料庫 |
| 2 | **掃描已變更程式碼** — 將每個函式對照所有 10 個 OWASP 類別 |
| 3 | **掃描整個專案** — 所有 `.go`、`.ts`、`.js`、`.py`、`.java`、`.php` 檔案 |
| 4 | **相依套件稽核** — `npm audit`、`pip-audit`、`go list -m all` |

**輸出格式：**
```
## Security Audit Report

### OWASP Top 10 (CURRENT_YEAR) — Fetched Live on DATE

### Vulnerabilities Found
| Severity | OWASP Category | CWE ID | CVE ID | File | Line | Description | Fix |

### Secure Code
[修補後的程式碼]
```

---

### 3. Performance Optimizer — 效能優化工程師

```yaml
name: performance-optimizer
tools: Read, Write                   # Claude Code
tools: read, edit                    # GitHub Copilot CLI
tools: read_file, write_file         # Gemini CLI
```

**角色身份：** 效能與程式碼品質工程師（Performance & Code Quality Engineer）。

**觸發時機：** 程式碼產生後，以及對話中出現 `optimize`、`performance`、`complexity`、`refactor`、`slow`、`bottleneck` 等詞彙時。

**功能說明：**
分析每個函式的時間複雜度，並從可讀性、可維護性、可擴展性、可偵錯性四個維度強制執行程式碼品質標準。

**複雜度規則：**

| 複雜度 | 決策 |
|--------|------|
| O(1)、O(log n)、O(n)、O(n log n) | 接受 |
| O(n²) | 允許——但必須加上理由說明註解 |
| O(2ⁿ) 或更差 | **拒絕**——必須重寫 |

**品質標準：**

| 維度 | 規範 |
|------|------|
| 可讀性 | 自我說明式命名；函式 ≤40 行；禁止巢狀三元運算子；最大巢狀深度 3 層 |
| 可維護性 | 禁止魔法數字（使用具名常數）；附帶情境的明確錯誤處理 |
| 可偵錯性 | 在關鍵決策點記錄結構化 log；錯誤訊息包含「什麼失敗 / 為何失敗 / 在哪失敗」 |

**輸出格式：**
```
## Performance & Quality Report

### Complexity Analysis
| Function | Current O() | Optimal O() | Action Required |

### Quality Issues
[檔案 + 行號 + 問題 + 建議修正]

### Optimized Code
[優化後的版本與說明]
```

---

### 4. Documentation Writer — 技術文件工程師

```yaml
name: documentation-writer
model: haiku                                                 # Claude Code — 使用較快的模型
tools: Read, Write, Glob, Grep                               # Claude Code
tools: read, edit, search                                    # GitHub Copilot CLI
tools: read_file, write_file, glob, search_file_content      # Gemini CLI
```

**角色身份：** 技術文件工程師（Technical Documentation Engineer）。

**觸發時機：** 所有程式碼定稿後，以及對話中出現 `add comments`、`document`、`annotate`、`explain code` 等詞彙時。

**功能說明——兩大職責合一：**

1. **行內註解** — 為每個檔案、函式與非顯而易見的邏輯區塊加入完整的英文註解，讓任何開發者在 60 秒內理解程式碼。
2. **文件全域掃描** — 將所有 `*.md` 檔案與目前的程式碼庫交叉比對，重寫所有過時的段落以保持同步。

**註解規範：**

| 範圍 | 應寫入內容 |
|------|----------|
| 檔案標頭 | 套件用途、架構說明、相依套件清單、使用範例 |
| 函式標頭 | 參數、回傳值、副作用、時間複雜度 |
| 行內 | 解釋「為什麼」而非「做什麼」；安全敏感程式碼必須引用 OWASP 類別或 CWE ID |

**文件全域掃描（四步驟）：**

| 步驟 | 動作 |
|------|------|
| 1 | 探索所有 `README.md`、`CHANGELOG.md`、`docs/**/*.md`、`.github/**/*.md` |
| 2 | 將每份文件與目前原始碼交叉比對 |
| 3 | 重寫過時的函式簽章、API 範例、CLI 旗標 |
| 4 | 完整性檢查——每個公開 API 必須有摘要、參數說明、回傳值描述、使用範例 |

**絕對規則：**
- 所有註解必須以英文撰寫
- 禁止撰寫顯而易見的註解（如 `// increment i` 對應 `i++`）
- 禁止修改原始碼來配合文件——文件永遠跟隨程式碼
- 已移除的 API 標示為 `[DEPRECATED — removed in <version>]` 而非直接刪除

---

### 5. Malicious Software Analysis — 惡意軟體分析師

```yaml
name: malicious-software-analysis
tools: Read, Bash, Glob, Grep, WebSearch, WebFetch                                             # Claude Code
tools: read, search, execute, web                                                              # GitHub Copilot CLI
tools: read_file, write_file, list_directory, search_file_content, run_shell_command, google_web_search, web_fetch  # Gemini CLI
model: gemini-2.5-pro                                                                 # Gemini CLI 專屬
```

**角色身份：** 資深網路安全研究員暨程式碼稽核專家（Senior Cybersecurity Researcher & Code Audit Expert）。
**威脅等級：** 最高（MAXIMUM）——所有來源不明或第三方程式碼，在證明無害之前一律視為有敵意。

**觸發時機：** 對話中出現 `malware`、`security scan`、`code audit`、`backdoor`、`credential leak`、`suspicious code`、`supply chain attack`、`reverse shell`、`obfuscation` 等詞彙時。

**功能說明：**
對整個 Repository 執行深度靜態應用程式安全測試（SAST）。每次執行前強制即時抓取威脅情報，才開始掃描任何一行程式碼。

**五步執行流程：**

**步驟 1 — 即時威脅情報（每次執行前強制執行）：**

| 情報來源 | 網址 | 關注重點 |
|---------|------|---------|
| OWASP Top 10 | https://owasp.org/www-project-top-ten/ | 僅使用當年度版本 |
| MITRE ATT&CK | https://attack.mitre.org/ | T1059、T1547、T1041、T1071 |
| CVE 資料庫 | https://www.cve.org/ / https://nvd.nist.gov/ | 比對本 repo 使用的函式庫 |
| ThreatFox IOC | https://threatfox.abuse.ch/ | 比對程式碼中的硬編碼 IP、域名、雜湊值 |

**步驟 2 — 列舉所有檔案：**
涵蓋 Shell 腳本、套件 manifest、設定檔、CI/CD pipeline、以及疑似混淆的檔案。

**步驟 3 — 靜態分析五大偵測類別：**

| 類別 | 偵測訊號 |
|------|---------|
| 網路與遠端存取 | `/dev/tcp`、`nc -e`、`bash -i`、硬編碼 IP、DNS 外洩 |
| 危險系統呼叫 | `eval(`、`exec(`、`os.system(`、`chmod 777`、`setuid`、cron 寫入 |
| 混淆與編碼 | Base64 blob、十六進位編碼、字串拼接隱藏關鍵字（`'cm'+'d'`）、高熵名稱 |
| 敏感資訊與憑證 | API 金鑰、`AKIA[0-9A-Z]{16}`（AWS）、`-----BEGIN PRIVATE KEY-----` |
| 供應鏈攻擊 | 仿冒套件名稱（typosquatting）、`postinstall` shell hooks、無雜湊驗證的 `curl \| bash` |

**步驟 4 — 相依套件稽核：**
`npm audit`、`pip-audit`、`go list -m all`、`bundle audit`、`cargo audit`

**步驟 5 — 結構化報告：**
```
## Malicious Software Analysis Report
Overall Risk Level: CRITICAL / HIGH / MEDIUM / LOW

### Executive Summary
[2–3 句整體風險評估]

### Findings
| 檔案路徑 | 風險類型 | 嚴重等級 | 具體描述與攻擊向量 | 修復建議 |

### Recommended Actions
[優先修復清單]
```

**絕對規則：** 存疑即標記——禁止在未完整去混淆的情況下將程式碼認定為無害。每個發現必須包含：程式碼的行為、如何造成攻擊、以及具體的修復方式。

---

## `tools` 參數名稱從何而來？

每個 agent frontmatter 中的 `tools` 欄位，限制了該 sub-agent 可以呼叫哪些內建工具。每個 CLI 平台有自己的工具名稱詞彙表。

---

### Claude Code CLI

**官方參考資料：**
- Sub-Agents 說明文件：[https://docs.anthropic.com/en/docs/claude-code/sub-agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- GitHub Repository：[https://github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)
- 設定與配置：[https://docs.anthropic.com/en/docs/claude-code/settings](https://docs.anthropic.com/en/docs/claude-code/settings)

Claude Code agent frontmatter 中的 `tools` 值**直接對應** Claude Code 的原生內建工具名稱——與 CLI 在 agentic 模式下內部使用的名稱完全相同：

| 工具名稱 | 功能說明 |
|---------|---------|
| `Read` | 讀取檔案內容 |
| `Write` | 建立或覆寫檔案 |
| `Edit` | 對檔案進行精確字串替換 |
| `Bash` | 執行 Shell 指令 |
| `Glob` | 依 glob 模式搜尋檔案 |
| `Grep` | 以正規表示式搜尋檔案內容（底層使用 ripgrep） |
| `WebSearch` | 搜尋網路 |
| `WebFetch` | 抓取指定網址的內容 |
| `LS` | 列出目錄內容 |

**安裝路徑：**

```
~/.claude/agents/<name>.md          # 全域——所有專案皆可使用
<project>/.claude/agents/<name>.md  # 專案範圍
```

`tools` 欄位作為**安全邊界**——宣告為只有 `Read, Glob, Grep` 的 sub-agent，即使系統提示詞指示它寫入檔案或執行 Shell，也無法做到。

---

### GitHub Copilot CLI

**官方參考資料：**
- 自訂 Agent 設定：[https://docs.github.com/en/copilot/reference/custom-agents-configuration](https://docs.github.com/en/copilot/reference/custom-agents-configuration)
- 建立自訂 Agent 說明：[https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli)
- CLI 指令參考：[https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference)

`.agent.md` 格式適用於**獨立的 GitHub Copilot CLI**（以 `copilot` 指令執行，例如 `copilot --yolo`）。下列工具名稱為官方自訂 agent 設定文件中定義的主要別名。其他平台的別名（例如 Claude Code 的 `Bash`、`Read`、`Grep`）也可被識別，並自動對應至對應的主要名稱。

> **注意：** `gh copilot suggest` / `gh copilot explain`（舊版 GitHub CLI 擴充套件）已於 **2025-10-25 正式廢棄**，不支援自訂 agent。本 repo 僅針對獨立的 GitHub Copilot CLI。

| 工具名稱 | 可識別的別名 | 功能說明 |
|---------|------------|---------|
| `execute` | `shell`、`Bash`、`powershell` | 執行 Shell 指令 |
| `read` | `Read`、`NotebookRead` | 讀取檔案內容 |
| `edit` | `Edit`、`Write`、`MultiEdit`、`NotebookEdit` | 建立或編輯檔案 |
| `search` | `Grep`、`Glob` | 搜尋檔案與內容 |
| `web` | `WebSearch`、`WebFetch` | 網路搜尋與抓取 URL |
| `agent` | `custom-agent`、`Task` | 呼叫另一個自訂 agent |
| `todo` | `TodoWrite` | 管理任務清單 |

**安裝路徑：**

```
<project>/.github/agents/<name>.agent.md   # 專案範圍
~/.copilot/agents/<name>.agent.md          # 使用者全域（所有專案）
```

> **注意：** `--yolo` 旗標（等同於 `--allow-all`）允許所有工具直接執行，跳過所有確認對話框。`tools:` 欄位中無法識別的工具名稱會被靜默忽略——若所有名稱均無法識別，agent 將退回繼承所有工具的預設行為。

---

### Gemini CLI

**官方參考資料：**
- GitHub Repository：[https://github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)
- 工具說明文件：[https://github.com/google-gemini/gemini-cli/blob/main/docs/tools.md](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools.md)
- 設定指南：[https://github.com/google-gemini/gemini-cli/blob/main/docs/configuration.md](https://github.com/google-gemini/gemini-cli/blob/main/docs/configuration.md)

工具名稱來自 Google 官方 repository 中 Gemini CLI 的核心內建工具集：

| 工具名稱 | 功能說明 |
|---------|---------|
| `read_file` | 讀取檔案內容 |
| `write_file` | 建立或寫入檔案 |
| `list_directory` | 列出目錄內容 |
| `search_file_content` | 以正規表示式搜尋檔案內容（grep） |
| `run_shell_command` | 執行 Shell 指令 |
| `google_web_search` | 透過 Google Search 搜尋網路 |
| `web_fetch` | 抓取指定網址的內容 |

**安裝路徑：**

```
~/.gemini/agents/<name>.md
```

**Gemini CLI 專屬功能：** `model` 欄位（`gemini-2.5-pro`）允許為每個 agent 單獨指定模型。惡意軟體分析 agent 使用 Gemini 2.5 Pro，因其在複雜威脅模式推理上擁有更強的能力。

---

## Multi-Agent 流水線架構

> **一句話串聯所有功能：** 只需將這五份 agent markdown 放入 AI CLI 的 agent 目錄，協調器就會自動依序派遣每位專家——**資深程式碼審查員**強制執行架構與命名規範、**資安工程師**即時抓取 CVE 並將每個函式對照 OWASP 類別、**效能優化工程師**消除 O(n²) 瓶頸與魔法數字、**文件工程師**添加行內註解並讓所有 README 與即時程式碼庫保持同步、**惡意軟體分析師**利用即時 MITRE ATT&CK 情報追蹤後門、憑證洩漏與供應鏈攻擊——形成一條無縫接合的全自動開發品質流水線，五位 sub-agent 協力合作，確保每次程式碼變更都完整經過審查、強化、優化、記錄與威脅掃描，零人工干預。

```
程式碼寫入 / 修改
        │
        ▼
┌─────────────────────────┐
│   Senior Code Reviewer  │  SOLID · DRY · KISS · YAGNI
│   tools: Read Glob Grep │  反模式偵測 · 命名規範
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│   Security Engineer     │  OWASP Top 10（即時）· CWE · CVE
│   tools: +WebSearch     │  相依套件稽核 · 全專案掃描
│          +WebFetch Bash │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│   Performance Optimizer │  時間複雜度 O() · 可讀性
│   tools: Read Write     │  可維護性 · 可偵錯性
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│   Documentation Writer  │  行內註解 · 檔案/函式標頭
│   tools: +Glob Grep     │  README 同步 · 完整性掃描
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  Malicious Software     │  SAST · MITRE ATT&CK · IOC feeds
│  Analysis               │  反向 shell · 供應鏈攻擊
│  tools: +Bash +Web*     │  混淆偵測 · 憑證洩漏
└─────────────────────────┘
            │
            ▼
    生產環境就緒的程式碼
```

### 協調機制的運作原理

每個 agent 的 `description` 欄位包含關鍵字觸發條件。當你寫下程式碼或在 AI 對話中使用匹配的關鍵字時，協調器會：

1. 讀取 agent 目錄中所有 agent 的 description
2. 將你的對話情境與每個 agent 的觸發關鍵字進行比對
3. 派遣相關的專家——可以並行或依序執行
4. 每位專家只能使用其宣告的 `tools`（最小權限原則）
5. 報告回傳至主對話視窗

這意味著你完全不需要手動呼叫任何 agent——系統自動路由，每位專家負責自己的領域，五者合力覆蓋完整的品質生命週期。

---

## 三大平台工具名稱對照表

| 功能 | Claude Code CLI | GitHub Copilot CLI | Gemini CLI |
|------|----------------|-------------------|------------|
| 讀取檔案 | `Read` | `read`（別名：`Read`） | `read_file` |
| 寫入檔案 | `Write` | `edit`（別名：`Write`） | `write_file` |
| 搜尋程式碼 | `Grep` | `search`（別名：`Grep`） | `search_file_content` |
| 執行指令 | `Bash` | `execute`（別名：`Bash`） | `run_shell_command` |
| 列出目錄 | `LS` | `execute`（執行 `ls`） | `list_directory` |
| 搜尋網路 | `WebSearch` | `web`（別名：`WebSearch`） | `google_web_search` |
| 抓取網址 | `WebFetch` | `web`（別名：`WebFetch`） | `web_fetch` |
| 搜尋檔案 | `Glob` | `search`（別名：`Glob`） | `glob` |

---

*這些 agent 設計為可自由修改。Fork 本 Repository，根據你的團隊標準調整觸發關鍵字、審查清單與輸出格式。*