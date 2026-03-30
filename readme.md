# AI Agent Markdown — Multi-Platform Sub-Agent Templates

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-CLI-orange)](https://github.com/anthropics/claude-code)
[![GitHub Copilot CLI](https://img.shields.io/badge/GitHub%20Copilot-CLI-blue)](https://github.com/features/copilot)
[![Gemini CLI](https://img.shields.io/badge/Gemini%20CLI-Google-green)](https://github.com/google-gemini/gemini-cli)

> **One sentence to connect everything:** Deploy these five specialist agent markdowns into any compatible AI CLI (Claude Code / GitHub Copilot / Gemini), and the orchestrator will automatically dispatch a complete development quality pipeline — **Code Reviewer → Security Engineer → Performance Optimizer → Documentation Writer → Malicious Software Analyst** — where each sub-agent owns its discipline, fires automatically on the right keyword trigger, and collaborates in sequence to deliver production-ready code without a single manual step.

---

## Table of Contents

- [What is this?](#what-is-this)
- [Project Structure](#project-structure)
- [Quick Start](#quick-start)
- [The 5 Agents at a Glance](#the-5-agents-at-a-glance)
- [Detailed Walkthrough — Each Agent](#detailed-walkthrough--each-agent)
  - [1. Senior Code Reviewer](#1-senior-code-reviewer)
  - [2. Security Engineer](#2-security-engineer)
  - [3. Performance Optimizer](#3-performance-optimizer)
  - [4. Documentation Writer](#4-documentation-writer)
  - [5. Malicious Software Analysis](#5-malicious-software-analysis)
- [Where Do `tools` Parameter Names Come From?](#where-do-tools-parameter-names-come-from)
  - [Claude Code CLI](#claude-code-cli)
  - [GitHub Copilot CLI](#github-copilot-cli)
  - [Gemini CLI](#gemini-cli)
- [The Multi-Agent Pipeline](#the-multi-agent-pipeline)

---

## What is this?

This repository provides **ready-to-use AI sub-agent definition files** for three major AI CLI platforms. Each agent is a Markdown file with a YAML frontmatter header that instructs the AI CLI:

| Frontmatter Field | Purpose |
|-------------------|---------|
| `name` | Unique identifier for the agent |
| `description` | When to automatically invoke it (keyword-based trigger) |
| `tools` | Which built-in tools this agent is allowed to call |
| `model` | Which AI model to use *(Gemini CLI / Claude Code)* |

The agent's system prompt follows the frontmatter — defining the agent's persona, step-by-step procedures, and structured output format.

**Install once → your AI CLI gains five specialized co-workers** that automatically review, secure, optimize, document, and threat-scan your code on every change.

---

## Project Structure

```
agents-markdown/
│
├── claude-code-cli/
│   └── agents/
│       ├── senior-code-reviewer.md          # Code review (SOLID/DRY/KISS)
│       ├── security-engineer.md             # OWASP + CVE security audit
│       ├── performance-optimizer.md         # Time complexity + quality
│       ├── documentation-writer.md          # Inline comments + doc sync
│       └── malicious-software-analysis.md   # SAST + malware detection
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
        ├── senior-code-reviewer.md          # Code review (SOLID/DRY/KISS)
        ├── security-engineer.md             # OWASP + CVE security audit
        ├── performance-optimizer.md         # Time complexity + quality
        ├── documentation-writer.md          # Inline comments + doc sync
        └── malicious-software-analysis.md   # Full SAST with Gemini 2.5 Pro
```

---

## Quick Start

### Claude Code CLI

```bash
# Global install (available in all projects)
cp claude-code-cli/agents/*.md ~/.claude/agents/

# Project-scoped install
cp claude-code-cli/agents/*.md /path/to/your/project/.claude/agents/
```

### GitHub Copilot CLI

```bash
# Global install (available in all projects)
mkdir -p ~/.copilot/agents
cp github-copilot-cli/agents/*.agent.md ~/.copilot/agents/

# Project-scoped install
mkdir -p /path/to/your/project/.github/agents
cp github-copilot-cli/agents/*.agent.md /path/to/your/project/.github/agents/
```

### Gemini CLI

```bash
# Global install
mkdir -p ~/.gemini/agents
cp gemini-cli/agents/*.md ~/.gemini/agents/
```

> **Required:** Gemini CLI sub-agents are an experimental feature and must be explicitly enabled. Add the following to `~/.gemini/settings.json`:
> ```json
> {
>   "experimental": { "enableAgents": true }
> }
> ```

After installation, agents **activate automatically** — no manual invocation needed. The AI CLI matches conversation context against each agent's `description` field and dispatches the appropriate specialist.

---

## The 5 Agents at a Glance

| Agent | Persona | Auto-Triggers On | Key Output |
|-------|---------|-----------------|------------|
| `senior-code-reviewer` | Principal Engineer, 35+ yrs | code written / modified / reviewed | Issue table + refactored code |
| `security-engineer` | Security Engineer, 35+ yrs | code changed, `OWASP`, `XSS`, `SQL`, `token`, `auth` | Vulnerability report + patched code |
| `performance-optimizer` | Perf & Quality Engineer | `optimize`, `slow`, `bottleneck`, `complexity`, `refactor` | Complexity analysis + optimized code |
| `documentation-writer` | Tech Docs Engineer | code finalized, `document`, `annotate`, `explain code` | Inline comments + README sync |
| `malicious-software-analysis` | Cybersecurity Researcher | `malware`, `backdoor`, `supply chain`, `scan`, `obfuscation` | SAST report + remediation list |

---

## Detailed Walkthrough — Each Agent

### 1. Senior Code Reviewer

```yaml
name: senior-code-reviewer
tools: Read, Glob, Grep                              # Claude Code
tools: read, search                                  # GitHub Copilot CLI
tools: read_file, glob, grep_search          # Gemini CLI
```

**Persona:** Principal Software Engineer with 35+ years of experience.

**When it fires:** Automatically after ANY code is written or modified, or when the words `review`, `best practice`, or `quality` appear.

**What it does:**
Performs a comprehensive code review on every modified file. Auto-detects the project language from file extensions and applies language-specific standards.

**Review Checklist:**

| Category | What it checks |
|----------|---------------|
| Architecture | SOLID, DRY (no duplicated logic), KISS (prefer simple), YAGNI (no speculative code) |
| Language idioms | Go: error wrapping / context propagation; TS: strict mode / no `any`; Python: type hints / PEP 8 |
| Anti-patterns | God functions (>40 lines), magic numbers, dead code, hidden coupling, deep nesting (>3 levels) |
| Naming | Self-documenting names only — no `x`, `tmp`, `data`, `res`, `obj` |

**Output format:**
```
## Code Review Report

### Issues Found
| File | Line | Severity (HIGH/MED/LOW) | Issue | Fix |
|------|------|--------------------------|-------|-----|

### Refactored Code
[Corrected version with explanation]
```

---

### 2. Security Engineer

```yaml
name: security-engineer
tools: Read, Write, WebSearch, WebFetch, Bash, Glob, Grep                               # Claude Code
tools: read, edit, search, execute, web                                                  # GitHub Copilot CLI
tools: read_file, write_file, glob, grep_search, run_shell_command, google_web_search, web_fetch  # Gemini CLI
```

**Persona:** Senior Information Security Engineer with 35+ years of experience.

**When it fires:** After ANY code change, and on keywords: `security`, `vulnerability`, `CVE`, `OWASP`, `injection`, `XSS`, `auth`, `SQL`, `token`, `password`.

**What it does:**
Fetches the **current year's** OWASP Top 10, CWE weaknesses, and live CVEs — then maps every function and dependency against them. Never uses cached or hardcoded security references.

**4-Step Execution:**

| Step | Action |
|------|--------|
| 1 | **Fetch live references** — OWASP Top 10 (current year), CWE, CVE databases |
| 2 | **Scan changed code** — map every function against all 10 OWASP categories |
| 3 | **Scan entire project** — all `.go`, `.ts`, `.js`, `.py`, `.java`, `.php` files |
| 4 | **Dependency audit** — `npm audit`, `pip-audit`, `go list -m all` |

**Output format:**
```
## Security Audit Report

### OWASP Top 10 (CURRENT_YEAR) — Fetched Live on DATE

### Vulnerabilities Found
| Severity | OWASP Category | CWE ID | CVE ID | File | Line | Description | Fix |

### Secure Code
[Patched version]
```

---

### 3. Performance Optimizer

```yaml
name: performance-optimizer
tools: Read, Write                   # Claude Code
tools: read, edit                    # GitHub Copilot CLI
tools: read_file, write_file         # Gemini CLI
```

**Persona:** Performance & Code Quality Engineer.

**When it fires:** After code is generated, and on keywords: `optimize`, `performance`, `complexity`, `refactor`, `slow`, `bottleneck`.

**What it does:**
Analyzes every function's time complexity and enforces four code quality dimensions: readability, maintainability, extensibility, and debuggability.

**Complexity Rules:**

| Complexity | Decision |
|------------|----------|
| O(1), O(log n), O(n), O(n log n) | Accepted |
| O(n²) | Allowed — must add a justification comment |
| O(2ⁿ) or worse | **REJECT** — must rewrite |

**Quality Standards:**

| Dimension | Rules |
|-----------|-------|
| Readability | Self-documenting names; functions ≤40 lines; no nested ternary; max 3-level nesting |
| Maintainability | No magic numbers (use named constants); explicit error handling with context |
| Debuggability | Structured logging at key decision points; error messages include what / why / where |

**Output format:**
```
## Performance & Quality Report

### Complexity Analysis
| Function | Current O() | Optimal O() | Action Required |

### Quality Issues
[File + Line + Issue + Suggested Fix]

### Optimized Code
[Rewritten version with explanation]
```

---

### 4. Documentation Writer

```yaml
name: documentation-writer
model: haiku                                                 # Claude Code — faster model
tools: Read, Write, Glob, Grep                               # Claude Code
tools: read, edit, search                                    # GitHub Copilot CLI
tools: read_file, write_file, glob, grep_search      # Gemini CLI
```

**Persona:** Technical Documentation Engineer.

**When it fires:** After all code is finalized, and on: `add comments`, `document`, `annotate`, `explain code`.

**What it does — two responsibilities:**

1. **Inline commenting** — adds comprehensive English comments to every file, function, and non-trivial logic block so any developer understands the code in under 60 seconds.
2. **Documentation sweep** — cross-references all `*.md` files against the current codebase and rewrites any outdated sections.

**Comment Requirements:**

| Scope | What to write |
|-------|--------------|
| File header | Package purpose, architecture, dependencies, usage example |
| Function header | Parameters, return values, side effects, time complexity |
| Inline | Explain WHY, not what; security-sensitive code must cite OWASP / CWE ID |

**Documentation Sweep (4 steps):**

| Step | Action |
|------|--------|
| 1 | Discover all `README.md`, `CHANGELOG.md`, `docs/**/*.md`, `.github/**/*.md` |
| 2 | Cross-reference each doc against current source code |
| 3 | Rewrite outdated function signatures, API examples, CLI flags |
| 4 | Completeness check — every public API must have summary, params, return, example |

**Absolute Rules:**
- All comments must be in English
- Never write obvious comments (`// increment i` for `i++`)
- Never modify source code to match docs — docs always follow code
- Mark removed APIs as `[DEPRECATED — removed in <version>]`

---

### 5. Malicious Software Analysis

```yaml
name: malicious-software-analysis
tools: Read, Bash, Glob, Grep, WebSearch, WebFetch                                             # Claude Code
tools: read, search, execute, web                                                              # GitHub Copilot CLI
tools: read_file, write_file, list_directory, grep_search, run_shell_command, google_web_search, web_fetch  # Gemini CLI
model: gemini-2.5-pro                                                                 # Gemini CLI specific
```

**Persona:** Senior Cybersecurity Researcher & Code Audit Expert.
**Threat Level:** MAXIMUM — all unknown or third-party code treated as hostile until proven otherwise.

**When it fires:** On keywords: `malware`, `security scan`, `code audit`, `backdoor`, `credential leak`, `suspicious code`, `supply chain attack`, `reverse shell`, `obfuscation`.

**What it does:**
Performs deep Static Application Security Testing (SAST) across the entire repository. Fetches live threat intelligence on every run before scanning a single line.

**5-Step Execution:**

**Step 1 — Live Threat Intelligence (mandatory before every scan):**

| Source | URL | Focus |
|--------|-----|-------|
| OWASP Top 10 | https://owasp.org/www-project-top-ten/ | Current year only |
| MITRE ATT&CK | https://attack.mitre.org/ | T1059, T1547, T1041, T1071 |
| CVE Database | https://www.cve.org/ / https://nvd.nist.gov/ | Libraries in this repo |
| ThreatFox IOC | https://threatfox.abuse.ch/ | Hardcoded IPs, domains, hashes |

**Step 2 — Enumerate all files:**
Every shell script, package manifest, config file, CI/CD pipeline, and obfuscated file.

**Step 3 — Static analysis across 5 detection categories:**

| Category | Signals Detected |
|----------|-----------------|
| Network & Remote Access | `/dev/tcp`, `nc -e`, `bash -i`, hardcoded IPs, DNS exfiltration |
| Dangerous System Calls | `eval(`, `exec(`, `os.system(`, `chmod 777`, `setuid`, cron writes |
| Obfuscation & Encoding | Base64 blobs, hex encoding, string splitting (`'cm'+'d'`), high-entropy names |
| Secrets & Credentials | API keys, `AKIA[0-9A-Z]{16}` (AWS), `-----BEGIN PRIVATE KEY-----` |
| Supply Chain | Typosquatting packages, `postinstall` shell hooks, `curl \| bash` without hash check |

**Step 4 — Dependency audit:**
`npm audit`, `pip-audit`, `go list -m all`, `bundle audit`, `cargo audit`

**Step 5 — Structured report:**
```
## Malicious Software Analysis Report
Overall Risk Level: CRITICAL / HIGH / MEDIUM / LOW

### Executive Summary
[2–3 sentence overall risk assessment]

### Findings
| File Path | Risk Type | Severity | Attack Vector | Fix |

### Recommended Actions
[Prioritized remediation list]
```

**Absolute Rule:** Flag when in doubt — never dismiss obfuscated code as benign without full deobfuscation. Every finding must include what the code does, how it enables an attack, and a concrete fix.

---

## Where Do `tools` Parameter Names Come From?

The `tools` field in each agent's frontmatter restricts which built-in tools the sub-agent may call. Each CLI platform defines its own tool vocabulary.

---

### Claude Code CLI

**Official References:**
- Sub-Agents documentation: [https://docs.anthropic.com/en/docs/claude-code/sub-agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- GitHub Repository: [https://github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)
- Settings & Configuration: [https://docs.anthropic.com/en/docs/claude-code/settings](https://docs.anthropic.com/en/docs/claude-code/settings)

The `tools` values in Claude Code agent frontmatter map **directly** to Claude Code's native built-in tool names — the same names used internally by the CLI in agentic mode:

| Tool Name | What it does |
|-----------|-------------|
| `Read` | Read file contents |
| `Write` | Create or overwrite a file |
| `Edit` | Make targeted string replacements in a file |
| `Bash` | Execute shell commands |
| `Glob` | Find files matching a glob pattern |
| `Grep` | Search file contents using regex (backed by ripgrep) |
| `WebSearch` | Search the web |
| `WebFetch` | Fetch a specific URL |
| `LS` | List directory contents |

**Install path:**

```
~/.claude/agents/<name>.md          # Global — available in all projects
<project>/.claude/agents/<name>.md  # Project-scoped
```

The `tools` field acts as a **security boundary** — a sub-agent declared with only `Read, Glob, Grep` cannot write files or run shell commands, even if the agent's system prompt instructs it to.

---

### GitHub Copilot CLI

**Official References:**
- Custom Agents Configuration: [https://docs.github.com/en/copilot/reference/custom-agents-configuration](https://docs.github.com/en/copilot/reference/custom-agents-configuration)
- Creating Custom Agents: [https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli)
- CLI Command Reference: [https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference)

The `.agent.md` format is used by the **standalone GitHub Copilot CLI** (invoked as `copilot`, e.g. `copilot --yolo`). The tool names below are the primary aliases defined in the official custom agents configuration reference. Aliases from other platforms (e.g. `Bash`, `Read`, `Grep` from Claude Code) are also recognized and silently mapped to the corresponding primary name.

> **Note:** `gh copilot suggest` / `gh copilot explain` (the old GitHub CLI extension) was **deprecated on 2025-10-25** and does not support custom agents. This repo targets the standalone GitHub Copilot CLI only.

| Tool Name | Recognized Aliases | What it does |
|-----------|-------------------|-------------|
| `execute` | `shell`, `Bash`, `powershell` | Execute shell commands |
| `read` | `Read`, `NotebookRead` | Read file contents |
| `edit` | `Edit`, `Write`, `MultiEdit`, `NotebookEdit` | Create or edit files |
| `search` | `Grep`, `Glob` | Search files and content |
| `web` | `WebSearch`, `WebFetch` | Web search and fetch URLs |
| `agent` | `custom-agent`, `Task` | Invoke another custom agent |
| `todo` | `TodoWrite` | Manage task lists |

**Install paths:**

```
<project>/.github/agents/<name>.agent.md   # Project-scoped
~/.copilot/agents/<name>.agent.md          # User-global (all projects)
```

> **Note:** The `--yolo` flag (alias for `--allow-all`) grants all tools execution permission without confirmation prompts. Unrecognized tool names in `tools:` are silently ignored — if all names are unrecognized, the agent falls back to inheriting all tools.

---

### Gemini CLI

**Official References:**
- GitHub Repository: [https://github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)
- Tools Documentation: [https://github.com/google-gemini/gemini-cli/blob/main/docs/tools.md](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools.md)
- Configuration Guide: [https://github.com/google-gemini/gemini-cli/blob/main/docs/configuration.md](https://github.com/google-gemini/gemini-cli/blob/main/docs/configuration.md)

The tool names come from Gemini CLI's core built-in tool set as defined in the official Google repository:

| Tool Name | What it does |
|-----------|-------------|
| `read_file` | Read file contents |
| `write_file` | Create or write to a file |
| `list_directory` | List directory contents |
| `grep_search` | Search files by content using regex (grep) |
| `run_shell_command` | Run shell commands |
| `google_web_search` | Search the web via Google Search |
| `web_fetch` | Fetch a specific URL |

**Install path:**

```
~/.gemini/agents/<name>.md
```

**Gemini CLI-specific feature:** The `model` field (`gemini-2.5-pro`) allows selecting a different model per agent. The malicious-software-analysis agent uses Gemini 2.5 Pro for its superior reasoning on complex threat patterns.

---

## The Multi-Agent Pipeline

> **The single unifying sentence:** By placing these five agent markdown files in your AI CLI's agent directory, the orchestrator will automatically dispatch each specialist in sequence — the **Senior Code Reviewer** enforces architecture and naming standards, the **Security Engineer** fetches live CVEs and maps every function to OWASP categories, the **Performance Optimizer** eliminates O(n²) bottlenecks and magic numbers, the **Documentation Writer** adds inline comments and keeps all README files synchronized with the live codebase, and the **Malicious Software Analyst** hunts for backdoors, credential leaks, and supply chain attacks using live MITRE ATT&CK intelligence — forming one seamless, fully automated development quality pipeline where five sub-agents work in concert so that every code change is reviewed, hardened, optimized, documented, and threat-scanned with zero manual intervention.

```
Code written / modified
        │
        ▼
┌─────────────────────────┐
│   Senior Code Reviewer  │  SOLID · DRY · KISS · YAGNI
│   tools: Read Glob Grep │  anti-patterns · naming standards
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│   Security Engineer     │  OWASP Top 10 (live) · CWE · CVE
│   tools: +WebSearch     │  dependency audit · full project scan
│          +WebFetch Bash │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│   Performance Optimizer │  time complexity O() · readability
│   tools: Read Write     │  maintainability · debuggability
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│   Documentation Writer  │  inline comments · file/fn headers
│   tools: +Glob Grep     │  README sync · completeness sweep
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  Malicious Software     │  SAST · MITRE ATT&CK · IOC feeds
│  Analysis               │  reverse shells · supply chain
│  tools: +Bash +Web*     │  obfuscation · credential leaks
└─────────────────────────┘
            │
            ▼
    Production-ready code
```

### How the orchestration works

Each agent's `description` field contains keyword triggers. When you write code or use a matching keyword in the AI conversation, the orchestrator:

1. Reads all agent descriptions in the agent directory
2. Matches your context against each agent's trigger keywords
3. Dispatches the relevant specialist(s) — in parallel or in sequence
4. Each specialist has access only to its declared `tools` (least-privilege enforcement)
5. Reports are returned to the main conversation

This means you never need to manually call an agent by name — the system routes automatically, each expert handles its domain, and the combined output covers the full quality lifecycle.

---

*Agents are designed to be modified. Fork this repository and customize trigger keywords, review checklists, and output formats to match your team's standards.*