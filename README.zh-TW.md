# AI Agent Markdown — 多平台 Sub-Agent 範本集

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-CLI-orange)](https://github.com/anthropics/claude-code)
[![GitHub Copilot CLI](https://img.shields.io/badge/GitHub%20Copilot-CLI-blue)](https://github.com/features/copilot)
[![Gemini CLI](https://img.shields.io/badge/Gemini%20CLI-Google-green)](https://github.com/google-gemini/gemini-cli)

> **一句話串聯所有功能：** 只需將這八份 agent markdown 部署至相容的 AI CLI（Claude Code／GitHub Copilot／Gemini），AI 即可同時具備兩條完整的工作流水線——**開發品質流水線**（程式碼審查 → 資安工程師 → 效能優化 → 文件撰寫 → 惡意軟體分析）自動在每次程式碼變更時觸發；**產品與設計流水線**（Sprint 產品負責人 → TPM 產品經理 → UI/UX 設計師）在你發想新功能或啟動新專案時按需啟動——八位專業 sub-agent 各司其職，讓 AI CLI 成為你完整的全端開發夥伴。

---

## 目錄

- [這是什麼？](#這是什麼)
- [專案結構](#專案結構)
- [快速開始](#快速開始)
- [Agent 分類總覽](#agent-分類總覽)
  - [第一類：開發品質流水線（自動觸發）](#第一類開發品質流水線自動觸發)
  - [第二類：產品與設計 Agent（按需觸發）](#第二類產品與設計-agent按需觸發)
- [開發品質流水線——各 Agent 詳細說明](#開發品質流水線各-agent-詳細說明)
  - [1. Senior Code Reviewer — 資深程式碼審查員](#1-senior-code-reviewer--資深程式碼審查員)
  - [2. Security Engineer — 資安工程師](#2-security-engineer--資安工程師)
  - [3. Performance Optimizer — 效能優化工程師](#3-performance-optimizer--效能優化工程師)
  - [4. Documentation Writer — 技術文件工程師](#4-documentation-writer--技術文件工程師)
  - [5. Malicious Software Analysis — 惡意軟體分析師](#5-malicious-software-analysis--惡意軟體分析師)
- [產品與設計 Agent——完整使用 SOP](#產品與設計-agent完整使用-sop)
  - [6. AI DLC Sprint Product Owner — Sprint 產品負責人](#6-ai-dlc-sprint-product-owner--sprint-產品負責人)
  - [7. TPM Product Manager — 技術產品經理](#7-tpm-product-manager--技術產品經理)
  - [8. UI/UX Designer — 資深 UI/UX 設計師](#8-uiux-designer--資深-uiux-設計師)
- [`tools` 參數名稱從何而來？](#tools-參數名稱從何而來)
  - [Claude Code CLI](#claude-code-cli)
  - [GitHub Copilot CLI](#github-copilot-cli)
  - [Gemini CLI](#gemini-cli)
- [Multi-Agent 流水線架構](#multi-agent-流水線架構)
- [三大平台工具名稱對照表](#三大平台工具名稱對照表)

---

## 這是什麼？

本 Repository 提供適用於三大 AI CLI 平台的 **AI sub-agent 定義檔案**，每個 agent 都是一份帶有 YAML frontmatter 標頭的 Markdown 檔案，用來告訴 AI CLI：

| Frontmatter 欄位 | 用途 |
|-----------------|------|
| `name` | Agent 的唯一識別名稱 |
| `description` | **何時觸發**（自動關鍵字比對，或使用者主動呼叫） |
| `tools` | 此 agent 被授權使用哪些內建工具（安全邊界） |
| `model` | 指定使用哪個 AI 模型 *（Gemini CLI / Claude Code 支援）* |
| `color` | 在 Claude Code 介面中顯示的顏色標籤 *（Claude Code 專屬）* |

YAML frontmatter 之後是 agent 的系統提示詞（system prompt），定義了角色身份、逐步執行流程與結構化輸出格式。

**安裝一次 → AI CLI 立即獲得八位專業協作夥伴**，涵蓋程式碼品質、資安、效能、文件、惡意軟體偵測、產品規劃、專案管理、UI/UX 設計的完整工作鏈。

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
│       ├── malicious-software-analysis.md   # SAST + 惡意軟體偵測
│       ├── ai-dlc-sprint-product-owner.md   # Sprint PRD 生成（強制問答）
│       ├── tpm-product-manager.md           # User Story + Backlog 管理
│       └── ui-ux-designer.md                # HTML/CSS 互動式原型設計
│
├── github-copilot-cli/
│   └── agents/
│       ├── senior-code-reviewer.agent.md
│       ├── security-engineer.agent.md
│       ├── performance-optimizer.agent.md
│       ├── documentation-writer.agent.md
│       ├── malicious-software-analysis.agent.md
│       ├── ai-dlc-sprint-product-owner.agent.md
│       ├── tpm-product-manager.agent.md
│       └── ui-ux-designer.agent.md
│
└── gemini-cli/
    └── agents/
        ├── senior-code-reviewer.md
        ├── security-engineer.md
        ├── performance-optimizer.md
        ├── documentation-writer.md
        ├── malicious-software-analysis.md   # 使用 Gemini 2.5 Pro
        ├── ai-dlc-sprint-product-owner.md   # 使用 Gemini 2.5 Pro
        ├── tpm-product-manager.md           # 使用 Gemini 2.5 Pro
        └── ui-ux-designer.md                # 使用 Gemini 2.5 Pro
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

> **必要步驟：** Gemini CLI 的 sub-agent 功能目前為實驗性功能，需手動啟用。請在 `~/.gemini/settings.json` 中加入以下設定：
> ```json
> {
>   "experimental": { "enableAgents": true }
> }
> ```

安裝完成後，agents **自動啟動**，無需手動呼叫。AI CLI 會將對話情境與每個 agent 的 `description` 欄位進行關鍵字比對，自動派遣對應的專家。

---

## Agent 分類總覽

### 第一類：開發品質流水線（自動觸發）

> 寫下程式碼或使用對應關鍵字，以下五位 agent 自動依序啟動，無需任何手動操作。

| Agent 名稱 | 角色身份 | 自動觸發關鍵字 | 主要產出 |
|-----------|---------|--------------|---------|
| `senior-code-reviewer` | 首席工程師，35+ 年 | 程式碼寫入／修改／review | 問題清單 + 重構後程式碼 |
| `security-engineer` | 資安工程師，35+ 年 | 程式碼變更、`OWASP`、`XSS`、`SQL`、`token` | 漏洞報告 + 修補後程式碼 |
| `performance-optimizer` | 效能品質工程師 | `optimize`、`slow`、`bottleneck`、`complexity` | 複雜度分析 + 優化後程式碼 |
| `documentation-writer` | 技術文件工程師 | 程式碼定稿、`document`、`annotate`、`explain code` | 行內註解 + README 同步 |
| `malicious-software-analysis` | 網路安全研究員 | `malware`、`backdoor`、`supply chain`、`scan` | SAST 報告 + 修復清單 |

---

### 第二類：產品與設計 Agent（按需觸發）

> 這三位 agent 在你發起新功能規劃、產品設計或 UI 製作時啟動。與第一類不同，它們是在你主動描述需求時觸發，而非程式碼事件。

| Agent 名稱 | 角色身份 | 觸發時機 | 主要產出 |
|-----------|---------|---------|---------|
| `ai-dlc-sprint-product-owner` | Sprint 產品負責人 | 描述想做的 app 或功能 | 48-72h 執行計畫 PRD（12 個區塊） |
| `tpm-product-manager` | 技術產品經理 | 設計稿完成後、需要 user stories | PRD.md + 格式化 User Stories |
| `ui-ux-designer` | 資深 UI/UX 設計師 | 需要設計元件、線框稿、設計系統 | `design/` 資料夾中的 HTML/CSS 原型 |

---

## 開發品質流水線——各 Agent 詳細說明

### 1. Senior Code Reviewer — 資深程式碼審查員

```yaml
name: senior-code-reviewer
tools: Read, Glob, Grep                          # Claude Code
tools: read, search                              # GitHub Copilot CLI
tools: read_file, glob, grep_search              # Gemini CLI
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
tools: Read, Write, WebSearch, WebFetch, Bash, Glob, Grep          # Claude Code
tools: read, edit, search, execute, web                            # GitHub Copilot CLI
tools: read_file, write_file, glob, grep_search,
       run_shell_command, google_web_search, web_fetch             # Gemini CLI
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
model: haiku                                         # Claude Code — 使用較快的模型
tools: Read, Write, Glob, Grep                       # Claude Code
tools: read, edit, search                            # GitHub Copilot CLI
tools: read_file, write_file, glob, grep_search      # Gemini CLI
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
- 禁止修改原始碼來配合文件——**文件永遠跟隨程式碼（documents always follow code）**
- 已移除的 API 標示為 `[DEPRECATED — removed in <version>]` 而非直接刪除

---

### 5. Malicious Software Analysis — 惡意軟體分析師

```yaml
name: malicious-software-analysis
tools: Read, Bash, Glob, Grep, WebSearch, WebFetch                                              # Claude Code
tools: read, search, execute, web                                                               # GitHub Copilot CLI
tools: read_file, write_file, list_directory, grep_search,
       run_shell_command, google_web_search, web_fetch                                          # Gemini CLI
model: gemini-2.5-pro                                                                           # Gemini CLI 專屬
```

**角色身份：** 資深網路安全研究員暨程式碼稽核專家（Senior Cybersecurity Researcher & Code Audit Expert）。
**威脅等級：** 最高（MAXIMUM）——所有來源不明或第三方程式碼，在證明無害之前一律視為有敵意。

**觸發時機：** 對話中出現 `malware`、`security scan`、`code audit`、`backdoor`、`credential leak`、`suspicious code`、`supply chain attack`、`reverse shell`、`obfuscation` 等詞彙時。

**五步執行流程：**

**步驟 1 — 即時威脅情報（每次執行前強制執行）：**

| 情報來源 | 網址 | 關注重點 |
|---------|------|---------|
| OWASP Top 10 | https://owasp.org/www-project-top-ten/ | 僅使用當年度版本 |
| MITRE ATT&CK | https://attack.mitre.org/ | T1059、T1547、T1041、T1071 |
| CVE 資料庫 | https://www.cve.org/ / https://nvd.nist.gov/ | 比對本 repo 使用的函式庫 |
| ThreatFox IOC | https://threatfox.abuse.ch/ | 比對程式碼中的硬編碼 IP、域名、雜湊值 |

**步驟 3 — 靜態分析五大偵測類別：**

| 類別 | 偵測訊號 |
|------|---------|
| 網路與遠端存取 | `/dev/tcp`、`nc -e`、`bash -i`、硬編碼 IP、DNS 外洩 |
| 危險系統呼叫 | `eval(`、`exec(`、`os.system(`、`chmod 777`、`setuid`、cron 寫入 |
| 混淆與編碼 | Base64 blob、十六進位編碼、字串拼接隱藏關鍵字（`'cm'+'d'`）、高熵名稱 |
| 敏感資訊與憑證 | API 金鑰、`AKIA[0-9A-Z]{16}`（AWS）、`-----BEGIN PRIVATE KEY-----` |
| 供應鏈攻擊 | 仿冒套件名稱（typosquatting）、`postinstall` shell hooks、無雜湊驗證的 `curl \| bash` |

---

## 產品與設計 Agent——完整使用 SOP

> 以下三個 agent 與開發品質流水線不同——它們**不會被動等待程式碼變更**，而是在你主動描述產品構想、設計需求或功能規劃時介入。本節提供每個 agent 的完整使用步驟，讓任何人看完即可上手。

---

### 6. AI DLC Sprint Product Owner — Sprint 產品負責人

```yaml
name: ai-dlc-sprint-product-owner
tools: Write                             # Claude Code
tools: write_file                        # Gemini CLI
tools: write                             # GitHub Copilot CLI
model: opus                              # Claude Code
model: gemini-2.5-pro                    # Gemini CLI
```

#### 適用場景

| 場景 | 說明 |
|------|------|
| 發想新的 side project | 想在週末或 48-72 小時內完成一個 MVP |
| 新功能規劃 | 有一個想法但不確定範圍，需要快速定義 MVP |
| 開發前的需求釐清 | 在開始寫程式之前，想對齊優先順序與技術方向 |

#### 運作原理

此 agent 採用**強制兩段式工作流程**，不可跳過 Phase 1：

```
Phase 1：結構化問答（永遠執行）
    │
    ├── 類別 1：核心問題（3 題）→ 等待你的回答
    ├── 類別 2：用戶輪廓（3 題）→ 等待你的回答
    └── 類別 3：成功定義（3 題）→ 等待你的回答
    │
    ▼
Phase 2：PRD 生成（收到全部回答後）
    └── 產出含 12 個區塊的完整 PRD，儲存為 .md 檔案
```

> **為什麼不能跳過 Phase 1？** 若直接生成 PRD，AI 會做出它認為「合理」的假設，但這些假設往往不符合你的真實優先順序。透過問答，agent 能捕捉到你對「正確性 vs 速度 vs 完整性」的真實排序，讓 PRD 的取捨決策完全對齊你的需求。

#### 逐步使用教學

**步驟 1：說出你的想法**

只需用自然語言描述你的 project 構想，agent 會自動識別並啟動：

```
使用者：我想建一個旅行安全資訊查詢工具，可以查看兩地之間的飛航禁帶品、
        安全警示、近期事件，並匯出 PDF
```

**步驟 2：回答類別 1——核心問題**

Agent 會問你三個問題，一次一組：

```
Q1. 為什麼要做這個工具？現有解決方案哪裡不好？
Q2. 這個痛點有多痛？（1-10 分）
Q3. 如果不解決，後果是什麼？
```

如實回答即可，不需要技術語言。

**步驟 3：回答類別 2——用戶輪廓**

```
Q4. 誰會用這個工具？（列出具體用戶類型）
Q5. 他們現在用什麼工具解決這個問題？
Q6. 他們最在意什麼？請依優先順序排列：
    速度 / 完整性 / 正確性 / 視覺清晰
```

**步驟 4：回答類別 3——成功定義**

```
Q7. 這個工具「成功」的指標是什麼？
Q8. MVP 最少要有哪些功能？（agent 會提供功能選項清單）
Q9. 你對「完成」的定義是什麼？
    - localhost 可跑就好
    - 要部署上線（偏好免費方案）
    - 要有完整視覺設計
```

**步驟 5：收到完整 PRD**

回答完三組問題後，agent 自動生成並儲存完整 PRD 文件，包含 12 個區塊：

| # | 區塊名稱 | 內容說明 |
|---|---------|---------|
| 1 | Core Intent | 一段話說明解決的問題與不解決的後果 |
| 2 | Target User | 一句話描述目標用戶 |
| 3 | **用戶優先順序** | 來自 Q6，驅動所有 Feature 取捨 |
| 4 | MVP Features（最多 5 項） | 每項標注 Day 1/2/3，單項 ≤8 小時 |
| 5 | Non-Features | 明確不做的功能，防 scope creep |
| 6 | Success Criteria | 可量測的完成標準 |
| 7 | Technical Constraints | 技術選型表，含免費部署方案 |
| 8 | **Data Source Strategy** | 每個模組的資料來源、取得方式 |
| 9 | **Day-by-Day Execution Plan** | 時段 \| 工作項目 \| 預期產出（三欄表） |
| 10 | **Key Technical Decisions** | 每項決策含替代方案與取捨說明 |
| 11 | Risk Mitigation | 風險 \| 影響 \| 緩解策略（三欄表） |
| 12 | **Folder Structure** | 完整前後端目錄樹，可直接作為 scaffolding 參考 |

#### 注意事項

- **不要在問答中跳過任何類別** — 每道題都對應 PRD 中的特定區塊
- **Q6 的優先排序至關重要** — 它決定了 MVP Features 的取捨邏輯
- **Q9 的部署需求** — 影響 Technical Constraints 中的部署方案選擇（agent 預設推薦免費方案）
- **PRD 存檔路徑** — 可在問答結束時告訴 agent 你想要的檔名與路徑

---

### 7. TPM Product Manager — 技術產品經理

```yaml
name: tpm-product-manager
tools: Read, Write, Glob, Grep           # Claude Code
tools: read_file, write_file, glob,
       grep_search                       # Gemini CLI
tools: read, write, search               # GitHub Copilot CLI
model: sonnet                            # Claude Code
model: gemini-2.5-pro                    # Gemini CLI
```

#### 適用場景

| 場景 | 說明 |
|------|------|
| 設計完成後的交接 | 設計師的 mockup 完成，需要轉換成開發可執行的 user stories |
| Backlog 管理 | 需要為待辦功能排列優先順序並估算 story points |
| 驗收條件定義 | 需要明確定義「什麼叫做完成」（Definition of Done） |
| 需求釐清 | 商業需求與技術實作之間的語言翻譯 |

#### 運作原理

```
輸入：設計稿 / 商業需求 / 口頭描述
    │
    ├── 讀取 /design-spec/ 中的設計文件
    ├── 分析需求，識別技術限制與開放問題
    │
    ├── 輸出 1：/specs/PRD.md（功能需求文件）
    └── 輸出 2：/specs/user-stories/*.md（格式化 User Story）
```

#### 逐步使用教學

**步驟 1：準備設計文件**

將設計稿或需求描述放置於 `/design-spec/` 目錄，或直接在對話中描述。

**步驟 2：觸發 Agent**

用以下任一方式觸發：

```
使用者：設計師完成了「購物車結帳流程」的 mockup，
        幫我建立對應的 user stories
```

```
使用者：幫我審查目前的 backlog，為每個功能排列優先順序
        並估算 story points
```

```
使用者：我們需要為「使用者通知設定」功能定義驗收條件
```

**步驟 3：查看生成的 User Story**

Agent 在 `/specs/user-stories/` 產出格式化的 User Story，每個 story 包含：

```markdown
## US-1.1 使用者可以新增商品至購物車

**Priority:** P0
**Story:** As a 購物用戶, I want 點擊「加入購物車」將商品加入購物車,
           so that 我可以一次結帳多件商品.

**Acceptance Criteria:**
- Given 我在商品頁面
  When 我點擊「加入購物車」按鈕
  Then 商品出現在購物車清單中，數量顯示為 1

- Given 購物車中已有此商品
  When 我再次點擊「加入購物車」
  Then 購物車中該商品數量 +1

**Story Points:** 2
**Dependencies:** 無
**Design Reference:** /design-spec/product-page.png
**Technical Notes:** 需要 POST /api/cart/items API，購物車狀態存於 localStorage
```

#### Story Points 估算標準

| Points | 適用情境 |
|--------|---------|
| 1 | 簡單 UI 調整、設定變更、文字更新 |
| 2 | 單一元件實作，需求明確 |
| 3 | 需要多個元件或中等複雜度的功能 |
| 5 | 需要架構考量或大量測試的複雜功能 |
| 8 | 跨系統整合、主要功能或高度不確定性的項目 |

#### 優先順序框架

| 等級 | 定義 | 影響 |
|------|------|------|
| P0 | MVP 核心功能，缺了就無法 Demo | 阻斷其他功能開發 |
| P1 | 顯著提升用戶體驗 | 與競品差異化 |
| P2 | 增加精緻感與喜悅感 | 可延後到 v2 |

#### 注意事項

- **每個 User Story 必須可獨立開發與測試** — 不符合此原則的故事需要拆分
- **Open Questions 必須明確標示** — 任何不確定的需求，agent 會在文件中標記「Open Questions」而非自行假設
- **設計文件路徑** — agent 預設讀取 `/design-spec/`，若設計稿在其他路徑請在對話中告知

---

### 8. UI/UX Designer — 資深 UI/UX 設計師

```yaml
name: ui-ux-designer
tools: Read, Write, Glob, Grep           # Claude Code
tools: read_file, write_file, glob,
       grep_search                       # Gemini CLI
tools: read, write, search               # GitHub Copilot CLI
model: opus                              # Claude Code
model: gemini-2.5-pro                    # Gemini CLI
color: blue                              # Claude Code 介面顏色標籤
```

#### 適用場景

| 場景 | 說明 |
|------|------|
| UI 元件設計 | 按鈕、卡片、表單、通知、Modal 等元件 |
| 線框稿（Wireframe） | 功能的互動流程草圖 |
| 設計系統 | Color tokens、Typography scale、Spacing system |
| 使用者流程圖 | 多步驟操作的視覺化流程 |
| 高保真原型 | 可直接展示給 stakeholder 的互動稿 |

#### 運作原理

```
使用者描述設計需求
    │
    ▼
Agent 分析需求
    │
    ├── 建立 design/ 資料夾（如不存在）
    └── 產出 HTML/CSS 互動式原型（永遠是視覺檔案，不只是文字）
```

> **核心原則：永遠輸出可預覽的視覺檔案。** 此 agent 不會只給你文字描述——每次回應都必須包含至少一個存放在 `design/` 資料夾中的 `.html` 檔案，可直接用瀏覽器開啟預覽。

#### 逐步使用教學

**步驟 1：觸發 Agent**

描述你的設計需求，agent 會自動識別並啟動：

```
使用者：設計一個通知卡片元件，需要有成功、警告、錯誤三種狀態，
        並且要符合無障礙標準
```

```
使用者：幫我建立一個完整的設計系統，包含 color tokens、
        typography scale 和基礎按鈕元件
```

```
使用者：畫出使用者登入流程的互動線框稿
```

**步驟 2：查看輸出的設計檔案**

Agent 在 `design/` 資料夾中產出 `.html` 檔案，例如：

```
design/
├── notification-card.html      # 通知元件（含三種狀態）
├── design-system.html          # 設計系統文件（互動式）
└── login-flow-wireframe.html   # 登入流程線框稿
```

用瀏覽器直接開啟即可預覽，所有狀態（hover、focus、active、disabled）皆可互動。

**步驟 3：確認技術規格**

每個設計檔案包含以下標準：

| 規格類別 | 內容 |
|---------|------|
| 色彩系統 | 使用 oklch() 色彩空間，感知均勻，符合 WCAG 2.2 對比度要求 |
| 排版 | CSS custom properties 定義的 type scale，從 xs 到 2xl |
| 間距 | 4px 基礎格線，space-1 到 space-12 |
| 響應式 | Container Queries（元件級），非僅 media queries |
| 動畫 | 包含 `prefers-reduced-motion` 退場機制 |
| 無障礙 | WCAG 2.2 AA：對比度、target size ≥24px、鍵盤導航、ARIA |

#### 2026 技術標準

此 agent 使用的是 2026 最佳實踐，而非過時的 CSS 慣例：

| 技術 | 說明 | 取代 |
|------|------|------|
| `oklch()` 色彩空間 | 感知均勻，更容易做可及性調色 | `#hex`、`rgb()` |
| CSS Container Queries | 元件自身響應，不依賴視窗寬度 | 僅用 media queries |
| CSS Nesting | 可維護的巢狀樣式，原生支援 | SCSS/SASS nesting |
| View Transitions API | 頁面與狀態切換的原生過場效果 | JavaScript 手動動畫 |
| WCAG 2.2 | 含 SC 2.5.8 指標尺寸（≥24×24px） | WCAG 2.1 |

#### AI-Native 界面支援（2026）

若你的產品涉及 AI 功能，此 agent 可以設計：
- 對話式 UI（Chat interface）
- Streaming 回應的漸進顯示元件
- 人機確認流程（Human-in-the-loop patterns）
- AI 信心指標視覺化
- AI 生成內容的揭露標籤（AI disclosure labels）

#### 注意事項

- **所有輸出存放在 `design/` 資料夾** — 不在其他路徑
- **永遠是視覺檔案** — 不接受「只輸出 CSS 片段」，必須是可獨立開啟的完整 `.html`
- **元件狀態必須完整** — default / hover / focus / active / disabled / error / loading 七種狀態
- **開發者友善** — 每個設計檔案包含 CSS custom property 名稱與 ARIA 實作說明，讓前端工程師可直接參照實作

---

## `tools` 參數名稱從何而來？

每個 agent frontmatter 中的 `tools` 欄位，限制了該 sub-agent 可以呼叫哪些內建工具。每個 CLI 平台有自己的工具名稱詞彙表。

---

### Claude Code CLI

**官方參考資料：**
- Sub-Agents 說明文件：[https://docs.anthropic.com/en/docs/claude-code/sub-agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- GitHub Repository：[https://github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)
- 設定與配置：[https://docs.anthropic.com/en/docs/claude-code/settings](https://docs.anthropic.com/en/docs/claude-code/settings)

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

---

### Gemini CLI

**官方參考資料：**
- GitHub Repository：[https://github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)
- 工具說明文件：[https://github.com/google-gemini/gemini-cli/blob/main/docs/tools.md](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools.md)

| 工具名稱 | 功能說明 |
|---------|---------|
| `read_file` | 讀取檔案內容 |
| `write_file` | 建立或寫入檔案 |
| `list_directory` | 列出目錄內容 |
| `glob` | 依 glob 模式搜尋檔案 |
| `grep_search` | 以正規表示式搜尋檔案內容 |
| `run_shell_command` | 執行 Shell 指令 |
| `google_web_search` | 透過 Google Search 搜尋網路 |
| `web_fetch` | 抓取指定網址的內容 |

**安裝路徑：**

```
~/.gemini/agents/<name>.md
```

---

## Multi-Agent 流水線架構

```
使用者描述 project 構想
        │
        ▼
┌─────────────────────────────┐
│  AI DLC Sprint Product Owner │  強制問答（9 題）→ 12 區塊 PRD
│  tools: Write                │  用戶優先排序 · Day-by-Day 計畫
└────────────┬────────────────┘
             │ PRD 完成，開始開發
             ▼
┌─────────────────────────────┐
│  TPM Product Manager         │  設計稿 → User Stories
│  tools: Read Write Glob Grep │  Backlog 排序 · Story Points
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│  UI/UX Designer              │  HTML/CSS 互動原型 → design/
│  tools: Read Write Glob Grep │  WCAG 2.2 · oklch() · Container Queries
└────────────┬────────────────┘
             │ 設計完成，開始實作
             ▼
┌─────────────────────────────┐
│   Senior Code Reviewer       │  SOLID · DRY · KISS · YAGNI
│   tools: Read Glob Grep      │  反模式偵測 · 命名規範
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│   Security Engineer          │  OWASP Top 10（即時）· CWE · CVE
│   tools: +WebSearch +Bash    │  相依套件稽核 · 全專案掃描
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│   Performance Optimizer      │  時間複雜度 O() · 可讀性
│   tools: Read Write          │  可維護性 · 可偵錯性
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│   Documentation Writer       │  行內註解 · 檔案/函式標頭
│   tools: +Glob Grep          │  README 同步 · 完整性掃描
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│  Malicious Software Analysis │  SAST · MITRE ATT&CK · IOC feeds
│  tools: +Bash +Web*          │  混淆偵測 · 供應鏈攻擊 · 憑證洩漏
└─────────────────────────────┘
             │
             ▼
    生產環境就緒的程式碼
```

### 協調機制的運作原理

每個 agent 的 `description` 欄位包含觸發條件。系統的運作方式：

1. 讀取 agent 目錄中所有 agent 的 description
2. 將你的對話情境與每個 agent 的觸發條件進行比對
3. 派遣相關的專家——可以並行或依序執行
4. 每位專家只能使用其宣告的 `tools`（最小權限原則）
5. 報告回傳至主對話視窗

---

## 三大平台工具名稱對照表

| 功能 | Claude Code CLI | GitHub Copilot CLI | Gemini CLI |
|------|----------------|-------------------|------------|
| 讀取檔案 | `Read` | `read`（別名：`Read`） | `read_file` |
| 寫入檔案 | `Write` | `edit`（別名：`Write`） | `write_file` |
| 搜尋程式碼 | `Grep` | `search`（別名：`Grep`） | `grep_search` |
| 搜尋檔案 | `Glob` | `search`（別名：`Glob`） | `glob` |
| 執行指令 | `Bash` | `execute`（別名：`Bash`） | `run_shell_command` |
| 列出目錄 | `LS` | `execute`（執行 `ls`） | `list_directory` |
| 搜尋網路 | `WebSearch` | `web`（別名：`WebSearch`） | `google_web_search` |
| 抓取網址 | `WebFetch` | `web`（別名：`WebFetch`） | `web_fetch` |

---

*這些 agent 設計為可自由修改。Fork 本 Repository，根據你的團隊標準調整觸發關鍵字、審查清單與輸出格式。*
