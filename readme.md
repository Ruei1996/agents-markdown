# AI Agent Markdown — Multi-Platform Sub-Agent Templates

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-CLI-orange)](https://github.com/anthropics/claude-code)
[![GitHub Copilot CLI](https://img.shields.io/badge/GitHub%20Copilot-CLI-blue)](https://github.com/features/copilot)
[![Gemini CLI](https://img.shields.io/badge/Gemini%20CLI-Google-green)](https://github.com/google-gemini/gemini-cli)

> **One sentence to connect everything:** Deploy these eight specialist agent markdowns into any compatible AI CLI (Claude Code / GitHub Copilot / Gemini), and your AI instantly gains two complete pipelines — the **Development Quality Pipeline** (Code Reviewer → Security Engineer → Performance Optimizer → Documentation Writer → Malicious Software Analyst) fires automatically on every code change; the **Product & Design Pipeline** (Sprint Product Owner → TPM Product Manager → UI/UX Designer) activates on demand when you plan a new feature or start a new project — eight sub-agents, each owning its domain, making your AI CLI a complete full-stack development partner.

---

## Table of Contents

- [What is this?](#what-is-this)
- [Project Structure](#project-structure)
- [Quick Start](#quick-start)
- [Agent Categories at a Glance](#agent-categories-at-a-glance)
  - [Category 1: Development Quality Pipeline (Auto-triggered)](#category-1-development-quality-pipeline-auto-triggered)
  - [Category 2: Product & Design Agents (Intent-triggered)](#category-2-product--design-agents-intent-triggered)
- [Development Quality Pipeline — Each Agent](#development-quality-pipeline--each-agent)
  - [1. Senior Code Reviewer](#1-senior-code-reviewer)
  - [2. Security Engineer](#2-security-engineer)
  - [3. Performance Optimizer](#3-performance-optimizer)
  - [4. Documentation Writer](#4-documentation-writer)
  - [5. Malicious Software Analysis](#5-malicious-software-analysis)
- [Product & Design Agents — Full SOP Tutorials](#product--design-agents--full-sop-tutorials)
  - [6. AI DLC Sprint Product Owner](#6-ai-dlc-sprint-product-owner)
  - [7. TPM Product Manager](#7-tpm-product-manager)
  - [8. UI/UX Designer](#8-uiux-designer)
- [Where Do `tools` Parameter Names Come From?](#where-do-tools-parameter-names-come-from)
  - [Claude Code CLI](#claude-code-cli)
  - [GitHub Copilot CLI](#github-copilot-cli)
  - [Gemini CLI](#gemini-cli)
- [The Multi-Agent Pipeline](#the-multi-agent-pipeline)
- [Cross-Platform Tool Name Reference](#cross-platform-tool-name-reference)

---

## What is this?

This repository provides **ready-to-use AI sub-agent definition files** for three major AI CLI platforms. Each agent is a Markdown file with a YAML frontmatter header that instructs the AI CLI:

| Frontmatter Field | Purpose |
|-------------------|---------|
| `name` | Unique identifier for the agent |
| `description` | When to automatically invoke it (keyword-based trigger, or user-initiated) |
| `tools` | Which built-in tools this agent is allowed to call (security boundary) |
| `model` | Which AI model to use *(Gemini CLI / Claude Code)* |
| `color` | Color label in Claude Code's UI *(Claude Code only)* |

The agent's system prompt follows the frontmatter — defining the agent's persona, step-by-step procedures, and structured output format.

**Install once → your AI CLI gains eight specialized co-workers** covering the complete workflow: code quality, security, performance, documentation, malware detection, product planning, project management, and UI/UX design.

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
│       ├── malicious-software-analysis.md   # SAST + malware detection
│       ├── ai-dlc-sprint-product-owner.md   # Sprint PRD generation (mandatory Q&A)
│       ├── tpm-product-manager.md           # User Stories + Backlog management
│       └── ui-ux-designer.md                # Interactive HTML/CSS prototype design
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
        ├── malicious-software-analysis.md   # Uses Gemini 2.5 Pro
        ├── ai-dlc-sprint-product-owner.md   # Uses Gemini 2.5 Pro
        ├── tpm-product-manager.md           # Uses Gemini 2.5 Pro
        └── ui-ux-designer.md                # Uses Gemini 2.5 Pro
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

## Agent Categories at a Glance

### Category 1: Development Quality Pipeline (Auto-triggered)

> Write code or use a matching keyword, and these five agents fire automatically in sequence — no manual steps required.

| Agent | Persona | Auto-Triggers On | Key Output |
|-------|---------|-----------------|------------|
| `senior-code-reviewer` | Principal Engineer, 35+ yrs | code written / modified / reviewed | Issue table + refactored code |
| `security-engineer` | Security Engineer, 35+ yrs | code changed, `OWASP`, `XSS`, `SQL`, `token`, `auth` | Vulnerability report + patched code |
| `performance-optimizer` | Perf & Quality Engineer | `optimize`, `slow`, `bottleneck`, `complexity`, `refactor` | Complexity analysis + optimized code |
| `documentation-writer` | Tech Docs Engineer | code finalized, `document`, `annotate`, `explain code` | Inline comments + README sync |
| `malicious-software-analysis` | Cybersecurity Researcher | `malware`, `backdoor`, `supply chain`, `scan`, `obfuscation` | SAST report + remediation list |

---

### Category 2: Product & Design Agents (Intent-triggered)

> These three agents activate when you describe a product idea, design requirement, or feature plan. Unlike Category 1, they are triggered by your explicit intent — not code events.

| Agent | Persona | Triggers On | Key Output |
|-------|---------|------------|------------|
| `ai-dlc-sprint-product-owner` | Sprint Product Owner | Describing an app or feature idea | 48-72h execution PRD (12 sections) |
| `tpm-product-manager` | Technical Product Manager | Design complete, need user stories | PRD.md + formatted User Stories |
| `ui-ux-designer` | Senior UI/UX Designer | Need component design, wireframe, design system | Interactive HTML/CSS prototypes in `design/` |

---

## Development Quality Pipeline — Each Agent

### 1. Senior Code Reviewer

```yaml
name: senior-code-reviewer
tools: Read, Glob, Grep                              # Claude Code
tools: read, search                                  # GitHub Copilot CLI
tools: read_file, glob, grep_search                  # Gemini CLI
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
tools: read_file, write_file, glob, grep_search              # Gemini CLI
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
- Never modify source code to match docs — **documents always follow code**
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

## Product & Design Agents — Full SOP Tutorials

> These three agents work differently from the development quality pipeline — they **do not wait passively for code changes**. Instead, they activate when you describe a product idea, design requirement, or feature plan. This section provides complete step-by-step instructions so any user can get started immediately.

---

### 6. AI DLC Sprint Product Owner

```yaml
name: ai-dlc-sprint-product-owner
tools: Write                             # Claude Code
tools: write_file                        # Gemini CLI
tools: write                             # GitHub Copilot CLI
model: opus                              # Claude Code
model: gemini-2.5-pro                    # Gemini CLI
```

#### When to Use

| Scenario | Description |
|----------|-------------|
| New side project idea | Want to ship an MVP in a weekend or 48-72 hours |
| New feature planning | Have an idea but unclear on scope — need to define the MVP fast |
| Pre-development alignment | Want to lock in priorities and technical direction before writing code |

#### How It Works

This agent uses a **mandatory two-phase workflow** — Phase 1 can never be skipped:

```
Phase 1: Structured Q&A (always runs)
    │
    ├── Category 1: Core Problem (3 questions) → waits for your answers
    ├── Category 2: User Profile (3 questions) → waits for your answers
    └── Category 3: Success Definition (3 questions) → waits for your answers
    │
    ▼
Phase 2: PRD Generation (after all answers received)
    └── Produces a complete 12-section PRD, saved as a .md file
```

> **Why can't Phase 1 be skipped?** If the agent generates the PRD directly, it makes assumptions it thinks are "reasonable" — but those assumptions often miss your actual priorities. The Q&A phase captures your real trade-off preferences (accuracy vs. speed vs. completeness), ensuring every decision in the PRD aligns with your specific needs.

#### Step-by-Step Instructions

**Step 1: Describe your idea**

Just describe your project in natural language — the agent auto-detects and activates:

```
User: I want to build a travel safety info tool that lets you look up
      flight restrictions, security alerts, and recent incidents between
      two locations, and export the result as a PDF
```

**Step 2: Answer Category 1 — Core Problem**

The agent asks three questions, one group at a time:

```
Q1. Why are you building this? What's wrong with existing solutions?
Q2. How painful is this problem? (Rate 1–10)
Q3. What happens if it goes unsolved?
```

Answer honestly — no technical jargon required.

**Step 3: Answer Category 2 — User Profile**

```
Q4. Who will use this tool? (List specific user types)
Q5. What tools do they currently use to solve this problem?
Q6. What do they care about most? Rank in order of priority:
    Speed / Completeness / Accuracy / Visual clarity
```

**Step 4: Answer Category 3 — Success Definition**

```
Q7. What does "success" look like for this tool?
Q8. What features must the MVP include? (Agent provides a checklist)
Q9. What does "done" mean to you?
    - Runs on localhost is enough
    - Needs to be deployed online (prefer free tier)
    - Needs a complete visual design
```

**Step 5: Receive your complete PRD**

After all three categories are answered, the agent automatically generates and saves the complete PRD, containing 12 sections:

| # | Section | Contents |
|---|---------|----------|
| 1 | Core Intent | One paragraph describing the problem and the cost of inaction |
| 2 | Target User | One sentence describing the primary user |
| 3 | **User Priority Ordering** | From Q6 — drives all feature trade-off decisions |
| 4 | MVP Features (max 5) | Each labeled Day 1/2/3, single item ≤8 hours |
| 5 | Non-Features | Explicitly out-of-scope items, prevents scope creep |
| 6 | Success Criteria | Measurable completion standards |
| 7 | Technical Constraints | Tech stack table, including free deployment options |
| 8 | **Data Source Strategy** | Data source, access method, and fallback per module |
| 9 | **Day-by-Day Execution Plan** | Time slot \| Task \| Expected output (3-column table) |
| 10 | **Key Technical Decisions** | Each decision with alternatives and trade-off rationale |
| 11 | Risk Mitigation | Risk \| Impact \| Mitigation strategy (3-column table) |
| 12 | **Folder Structure** | Complete frontend/backend directory tree for scaffolding |

#### Notes

- **Don't skip any category in the Q&A** — each question maps to a specific PRD section
- **Q6 priority ranking is critical** — it drives the trade-off logic throughout MVP Features
- **Q9 deployment requirement** — affects the deployment options in Technical Constraints (agent defaults to free-tier recommendations)
- **PRD save path** — tell the agent your preferred filename and path after the Q&A

---

### 7. TPM Product Manager

```yaml
name: tpm-product-manager
tools: Read, Write, Glob, Grep           # Claude Code
tools: read_file, write_file, glob,
       grep_search                       # Gemini CLI
tools: read, edit, search               # GitHub Copilot CLI
model: sonnet                            # Claude Code
model: gemini-2.5-pro                    # Gemini CLI
```

#### When to Use

| Scenario | Description |
|----------|-------------|
| Post-design handoff | Designer's mockup is ready — need to convert it into developer-executable user stories |
| Backlog management | Need to prioritize pending features and estimate story points |
| Acceptance criteria definition | Need to define clearly what "done" means (Definition of Done) |
| Requirements translation | Bridge the language gap between business requirements and technical implementation |

#### How It Works

```
Input: Design mockup / business requirement / verbal description
    │
    ├── Reads design documents from /design-spec/
    ├── Analyzes requirements, identifies technical constraints and open questions
    │
    ├── Output 1: /specs/PRD.md (feature requirements document)
    └── Output 2: /specs/user-stories/*.md (formatted User Stories)
```

#### Step-by-Step Instructions

**Step 1: Prepare design documents**

Place design mockups or requirement descriptions in the `/design-spec/` directory, or describe them directly in the conversation.

**Step 2: Trigger the agent**

Use any of the following:

```
User: The designer finished the mockup for "shopping cart checkout flow",
      create the corresponding user stories
```

```
User: Review the current backlog and prioritize each feature
      with story point estimates
```

```
User: We need to define acceptance criteria for the "user notification settings" feature
```

**Step 3: Review the generated User Stories**

The agent outputs formatted User Stories to `/specs/user-stories/`. Each story includes:

```markdown
## US-1.1 User can add item to cart

**Priority:** P0
**Story:** As a shopper, I want to click "Add to Cart" to add an item to my cart,
           so that I can check out multiple items at once.

**Acceptance Criteria:**
- Given I am on the product page
  When I click the "Add to Cart" button
  Then the item appears in the cart with quantity 1

- Given the item is already in the cart
  When I click "Add to Cart" again
  Then the cart quantity for that item increases by 1

**Story Points:** 2
**Dependencies:** None
**Design Reference:** /design-spec/product-page.png
**Technical Notes:** Requires POST /api/cart/items API, cart state stored in localStorage
```

#### Story Points Estimation Guide

| Points | When to use |
|--------|-------------|
| 1 | Simple UI tweak, config change, text update |
| 2 | Single component implementation, clear requirements |
| 3 | Multiple components or moderate complexity |
| 5 | Requires architectural consideration or extensive testing |
| 8 | Cross-system integration, major feature, or high uncertainty |

#### Priority Framework

| Level | Definition | Impact |
|-------|------------|--------|
| P0 | Core MVP feature — app cannot demo without it | Blocks other features |
| P1 | Significantly improves user experience | Differentiates from competitors |
| P2 | Adds polish and delight | Can defer to v2 |

#### Notes

- **Every User Story must be independently developable and testable** — stories that fail this test must be split
- **Open Questions must be explicitly marked** — the agent flags uncertain requirements as "Open Questions" rather than making assumptions
- **Design document path** — the agent defaults to reading from `/design-spec/`; specify an alternative path in the conversation if needed

---

### 8. UI/UX Designer

```yaml
name: ui-ux-designer
tools: Read, Write, Glob, Grep           # Claude Code
tools: read_file, write_file, glob,
       grep_search                       # Gemini CLI
tools: read, edit, search               # GitHub Copilot CLI
model: opus                              # Claude Code
model: gemini-2.5-pro                    # Gemini CLI
color: blue                              # Claude Code UI color label
```

#### When to Use

| Scenario | Description |
|----------|-------------|
| UI component design | Buttons, cards, forms, notifications, modals, etc. |
| Wireframing | Interactive flow sketches for a feature |
| Design system | Color tokens, typography scale, spacing system |
| User flow diagrams | Visual flows for multi-step interactions |
| High-fidelity prototypes | Interactive mockups ready to show stakeholders |

#### How It Works

```
User describes the design requirement
    │
    ▼
Agent analyzes the request
    │
    ├── Creates design/ folder if it doesn't exist
    └── Outputs interactive HTML/CSS prototype (always a visual file, never just text)
```

> **Core principle: Always output a previewable visual file.** This agent never gives you only text descriptions — every response must include at least one `.html` file saved in the `design/` folder, openable directly in a browser.

#### Step-by-Step Instructions

**Step 1: Trigger the agent**

Describe your design requirement — the agent auto-detects and activates:

```
User: Design a notification card component with success, warning,
      and error states that meets accessibility standards
```

```
User: Build a complete design system with color tokens,
      typography scale, and basic button components
```

```
User: Create an interactive wireframe for the user login flow
```

**Step 2: Review the design output**

The agent produces `.html` files in the `design/` folder, for example:

```
design/
├── notification-card.html      # Notification component (all 3 states)
├── design-system.html          # Design system documentation (interactive)
└── login-flow-wireframe.html   # Login flow wireframe
```

Open any file directly in a browser to preview. All component states (hover, focus, active, disabled) are fully interactive.

**Step 3: Verify the technical specifications**

Every design file conforms to these standards:

| Spec | Details |
|------|---------|
| Color system | `oklch()` color space — perceptually uniform, WCAG 2.2 contrast compliant |
| Typography | CSS custom property type scale from `xs` to `2xl` |
| Spacing | 4px base grid, `space-1` through `space-12` |
| Responsiveness | Container Queries (component-level), not just media queries |
| Animation | Includes `prefers-reduced-motion` fallback |
| Accessibility | WCAG 2.2 AA: contrast ratio, target size ≥24px, keyboard nav, ARIA |

#### 2026 Technology Standards

This agent uses 2026 best practices, not outdated CSS conventions:

| Technology | Description | Replaces |
|------------|-------------|---------|
| `oklch()` color space | Perceptually uniform, easier accessible palette design | `#hex`, `rgb()` |
| CSS Container Queries | Component-level responsiveness, independent of viewport | Media queries only |
| CSS Nesting | Maintainable nested styles, native browser support | SCSS/SASS nesting |
| View Transitions API | Native page/state transition effects | Manual JavaScript animations |
| WCAG 2.2 | Includes SC 2.5.8 pointer target size (≥24×24px) | WCAG 2.1 |

#### AI-Native Interface Support (2026)

If your product includes AI features, this agent can design:
- Conversational UI (chat interfaces)
- Streaming response progressive-display components
- Human-in-the-loop confirmation patterns
- AI confidence indicator visualizations
- AI-generated content disclosure labels

#### Notes

- **All output is saved to the `design/` folder** — never elsewhere
- **Always visual files** — "just output a CSS snippet" is not accepted; must be a standalone complete `.html` file
- **All component states required** — default / hover / focus / active / disabled / error / loading (all seven)
- **Developer-friendly** — every design file includes CSS custom property names and ARIA implementation notes for direct frontend reference

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
| `glob` | Find files matching a glob pattern |
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

> **The single unifying sentence:** By placing these eight agent markdown files in your AI CLI's agent directory, the orchestrator gains two complete pipelines — the **Product & Design Pipeline** (Sprint Product Owner → TPM Product Manager → UI/UX Designer) shapes the idea into a spec and prototype; the **Development Quality Pipeline** (Senior Code Reviewer → Security Engineer → Performance Optimizer → Documentation Writer → Malicious Software Analyst) then takes that implementation through automated review, security hardening, optimization, documentation, and threat scanning — eight sub-agents forming one seamless workflow from product idea to production-ready code.

```
User describes a project idea
        │
        ▼
┌─────────────────────────────┐
│  AI DLC Sprint Product Owner │  Mandatory Q&A (9 questions) → 12-section PRD
│  tools: Write                │  User priority ordering · Day-by-Day plan
└────────────┬────────────────┘
             │ PRD complete — development begins
             ▼
┌─────────────────────────────┐
│  TPM Product Manager         │  Design mockup → User Stories
│  tools: Read Write Glob Grep │  Backlog ordering · Story Points
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│  UI/UX Designer              │  Interactive HTML/CSS prototypes → design/
│  tools: Read Write Glob Grep │  WCAG 2.2 · oklch() · Container Queries
└────────────┬────────────────┘
             │ Design complete — implementation begins
             ▼
┌─────────────────────────────┐
│   Senior Code Reviewer       │  SOLID · DRY · KISS · YAGNI
│   tools: Read Glob Grep      │  Anti-pattern detection · naming standards
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│   Security Engineer          │  OWASP Top 10 (live) · CWE · CVE
│   tools: +WebSearch +Bash    │  Dependency audit · full project scan
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│   Performance Optimizer      │  Time complexity O() · readability
│   tools: Read Write          │  Maintainability · debuggability
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│   Documentation Writer       │  Inline comments · file/fn headers
│   tools: +Glob Grep          │  README sync · completeness sweep
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│  Malicious Software Analysis │  SAST · MITRE ATT&CK · IOC feeds
│  tools: +Bash +Web*          │  Reverse shells · supply chain · credential leaks
└─────────────────────────────┘
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

## Cross-Platform Tool Name Reference

| Function | Claude Code CLI | GitHub Copilot CLI | Gemini CLI |
|----------|----------------|-------------------|------------|
| Read file | `Read` | `read` (alias: `Read`) | `read_file` |
| Write file | `Write` | `edit` (alias: `Write`) | `write_file` |
| Search content | `Grep` | `search` (alias: `Grep`) | `grep_search` |
| Search files | `Glob` | `search` (alias: `Glob`) | `glob` |
| Run command | `Bash` | `execute` (alias: `Bash`) | `run_shell_command` |
| List directory | `LS` | `execute` (run `ls`) | `list_directory` |
| Web search | `WebSearch` | `web` (alias: `WebSearch`) | `google_web_search` |
| Fetch URL | `WebFetch` | `web` (alias: `WebFetch`) | `web_fetch` |

---

*Agents are designed to be modified. Fork this repository and customize trigger keywords, review checklists, and output formats to match your team's standards.*
