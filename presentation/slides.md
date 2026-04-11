---
theme: default
title: "AI-Assisted Software Development"
info: |
  Janelia Research Campus — Scientific Software Group
  A survey of harnesses, frontier models, common practices, issues, and extraordinary examples
drawings:
  persist: false
transition: none
mdc: true
---

# AI-Assisted Software Development

Harnesses, Frontier Models, Common Practices, Issues, and What's Possible

<div class="pt-12">
  <div class="text-lg">Bill Katz</div>
  <div class="text-sm opacity-70">Scientific Computing Software</div>
  <div class="text-sm opacity-50">HHMI Janelia Research Campus</div>
</div>

---

# Companion Resource Page

This talk has a repo: **[`github.com/JaneliaSciComp/ai-assisted-dev`](https://github.com/JaneliaSciComp/ai-assisted-dev)**

In addition to this presentation which uses Slidev, there's a `resources` directory with an Awesome-style markdown page of links to AI-assisted software development resources.

It's in early development — mostly seeded with sources from this talk. The goal is a curated, searchable collection of links for AI-assisted development at Janelia.

**If time permits** — some wild ideas for where this could go:

- Rate and comment on resources (short one-liner Janelian reviews)
- Tag-based search across tools, approaches, and examples
- "Follow" individual Janelians to see what they find useful
- AI-powered search that combines the above to suggest resources

For now: explore the links, and contribute anything you've found helpful.

---

# Talk Roadmap

1. **The Ecosystem** — Frontier models, harnesses, and what's available at Janelia
2. **Approaches** — Common patterns for AI-assisted development
3. **Issues** — Context rot, model degradation, and the feedback loop
4. **Extraordinary Examples** — What people are actually building

---
layout: section
---

# Part I: The Ecosystem

Frontier Models & Harnesses

---

# Three Frontier Systems

| | **Claude** (Anthropic) | **GPT / Codex** (OpenAI) | **Gemini** (Google) |
|---|---|---|---|
| Model | Opus 4.6, Sonnet 4.6 | GPT-5.4 | 3.1 Pro, Flash |
| Context | 200K-1M tokens | 200K-1M | 1M tokens |
| Harness | **Claude Code & App**, **Cowork** | **Codex**, **ChatGPT** | **Gemini CLI**, **Antigravity** |

All support tool use, MCP, and agentic workflows.

Introduced: Claude Code (Feb 2025), OpenAI Codex (May 2025), Gemini CLI (June 2025)

**Early 2026**: Agentic systems (run in parallel) with advances in both models and harnesses, have **changed** the software development landscape.

---

# What is a Harness?

<div class="flex gap-8 items-center">
<div class="flex-1">

The **model** is the horse — raw power and capability.

The **harness** is the equipment that lets you direct the horse, keep the rider comfortable, and make the trip productive.

Saddle, reins, stirrups → context management, tool use, feedback loops

</div>
<div class="w-80">
<img src="/images/HorseHarness.jpg" class="rounded shadow" />
</div>
</div>


---

# Harnesses: The Orchestration Layer

A **harness** wraps a frontier model with everything it needs to do useful work:

<svg viewBox="0 0 700 200" xmlns="http://www.w3.org/2000/svg" class="w-full mt-2">
  <defs>
    <marker id="ah2" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
    <marker id="ah2rev" markerWidth="8" markerHeight="6" refX="0" refY="3" orient="auto">
      <polygon points="8 0, 0 3, 8 6" fill="#666"/>
    </marker>
  </defs>

  <!-- Developer -->
  <rect x="10" y="80" width="90" height="36" rx="6" fill="#dbeafe" stroke="#999" stroke-width="1.5"/>
  <text x="55" y="100" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Developer</text>

  <!-- Arrow: Developer → Harness -->
  <line x1="100" y1="98" x2="148" y2="98" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah2)"/>

  <!-- Harness (center) -->
  <rect x="150" y="70" width="100" height="56" rx="6" fill="#e0e7ff" stroke="#6366f1" stroke-width="2"/>
  <text x="200" y="94" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Harness</text>
  <text x="200" y="110" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">orchestration</text>

  <!-- Arrow: Harness → Tools -->
  <line x1="250" y1="82" x2="318" y2="35" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah2)"/>
  <!-- Tools -->
  <rect x="320" y="12" width="170" height="36" rx="6" fill="#f3f4f6" stroke="#999" stroke-width="1.5"/>
  <text x="405" y="33" font-family="sans-serif" font-size="11px" text-anchor="middle">Tools: files, shell, search</text>

  <!-- Arrow: Harness → Context -->
  <line x1="250" y1="98" x2="318" y2="98" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah2)"/>
  <!-- Context -->
  <rect x="320" y="80" width="170" height="36" rx="6" fill="#f3f4f6" stroke="#999" stroke-width="1.5"/>
  <text x="405" y="101" font-family="sans-serif" font-size="11px" text-anchor="middle">Context: files, docs, history</text>

  <!-- Bidirectional arrow: Harness ↔ Frontier Model -->
  <line x1="252" y1="114" x2="318" y2="165" fill="none" stroke="#666" stroke-width="1.5" marker-start="url(#ah2rev)" marker-end="url(#ah2)"/>
  <!-- Frontier Model -->
  <rect x="320" y="148" width="170" height="36" rx="6" fill="#dbeafe" stroke="#999" stroke-width="1.5"/>
  <text x="405" y="169" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Frontier Model</text>

  <!-- Arrow: Harness → Output -->
  <line x1="200" y1="126" x2="200" y2="155" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah2)"/>
  <!-- Output -->
  <rect x="150" y="158" width="100" height="32" rx="6" fill="#dcfce7" stroke="#999" stroke-width="1.5"/>
  <text x="200" y="177" font-family="sans-serif" font-size="11px" text-anchor="middle">Output</text>

  <!-- Arrow: Output → feedback loop back to Harness -->
  <path d="M 148,174 C 115,174 115,120 150,100" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah2)"/>
  <text x="100" y="142" font-family="sans-serif" font-size="9px" fill="#666" text-anchor="middle">verify &amp;</text>
  <text x="100" y="154" font-family="sans-serif" font-size="9px" fill="#666" text-anchor="middle">feedback</text>
</svg>

<div class="text-sm mt-2">

**Tools** — file editing, shell commands, web search, MCP integrations<br>
**Context** — what the model sees, when, and how much<br>
**Feedback loops** — verification, test results, human review fed back in

</div>

---

# Harness UX: Different Surfaces for Different Workflows

| UX Surface | What it's for | Claude | OpenAI | Google |
|---|---|---|---|---|
| **IDE** | Code in a familiar editor with AI inline | IDE plugin | Copilot | Gemini Code Assist |
| **CLI** | Interactive terminal sessions, agentic coding | Claude Code | Codex CLI | Gemini CLI |
| **Desktop App** | Project sidebar, parallel sessions, diff review | Claude App | Codex App | — |
| **Cloud Agent** | Async background tasks on your repos | Managed Agents / *Ultraplan | Codex Cloud | Jules |
| **Chat / Web** | Conversation-first, paste code in and out | claude.ai | ChatGPT | Gemini |

*Ultraplan (Claude) is just planning in a cloud agent with nicer web UI.

Each vendor is converging on multiple surfaces — but the sweet spots differ.

---

# OpenAI Codex: Different Harnesses → Different UIs

<div class="relative mt-4" style="height: 420px;">
  <img src="/images/chatgpt-screenshot.png" class="absolute rounded shadow-lg border border-gray-600" style="left: 20px; top: 0px; width: 320px; z-index: 1;" />
  <div class="absolute text-sm font-bold opacity-70" style="left: 120px; top: 270px; z-index: 1;">ChatGPT App</div>
  <img src="/images/codex-cli-screenshot.png" class="absolute rounded shadow-lg border border-gray-600" style="left: 240px; top: 40px; width: 320px; z-index: 2;" />
  <div class="absolute text-sm font-bold opacity-70" style="left: 355px; top: 310px; z-index: 2;">Codex CLI</div>
  <img src="/images/codex-screenshot.png" class="absolute rounded shadow-lg border border-gray-600" style="left: 460px; top: 80px; width: 320px; z-index: 3;" />
  <div class="absolute text-sm font-bold opacity-70" style="left: 575px; top: 350px; z-index: 3;">Codex App</div>
</div>

---

# OpenAI Codex: Three Control Surfaces

One capability, three interfaces:

<svg viewBox="0 0 700 310" xmlns="http://www.w3.org/2000/svg" class="w-full mt-2">
  <defs>
    <marker id="ah5" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
  </defs>
  <!-- Codex Capability -->
  <rect x="270" y="0" width="160" height="36" rx="6" fill="#e0e7ff" stroke="#6366f1" stroke-width="2"/>
  <text x="350" y="22" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Codex Capability</text>
  <!-- Arrow → Cloud -->
  <line x1="300" y1="36" x2="120" y2="68" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah5)"/>
  <!-- Arrow → CLI -->
  <line x1="350" y1="36" x2="350" y2="68" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah5)"/>
  <!-- Arrow → App -->
  <line x1="400" y1="36" x2="580" y2="68" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah5)"/>

  <!-- Cloud Agent -->
  <rect x="20" y="70" width="160" height="36" rx="6" fill="#dbeafe" stroke="#3b82f6" stroke-width="1.5"/>
  <text x="100" y="92" font-family="sans-serif" font-size="11px" font-weight="bold" text-anchor="middle">Codex Cloud Agent</text>
  <!-- Cloud description -->
  <text x="100" y="125" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Remote worker</text>
  <text x="100" y="138" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">OpenAI-managed environments</text>
  <text x="100" y="151" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Background tasks, parallel execution</text>
  <text x="100" y="164" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Works against your repos</text>

  <!-- CLI -->
  <rect x="250" y="70" width="160" height="36" rx="6" fill="#dbeafe" stroke="#3b82f6" stroke-width="1.5"/>
  <text x="330" y="92" font-family="sans-serif" font-size="11px" font-weight="bold" text-anchor="middle">Codex CLI</text>
  <!-- CLI description -->
  <text x="330" y="125" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Local terminal interface</text>
  <text x="330" y="138" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Reads, edits, runs code in your dir</text>
  <text x="330" y="151" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Also launches cloud tasks</text>
  <text x="330" y="164" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">= local pair programmer + cloud console</text>

  <!-- App -->
  <rect x="500" y="70" width="160" height="36" rx="6" fill="#dbeafe" stroke="#3b82f6" stroke-width="1.5"/>
  <text x="580" y="92" font-family="sans-serif" font-size="11px" font-weight="bold" text-anchor="middle">Codex App</text>
  <!-- App description -->
  <text x="580" y="125" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Desktop command center</text>
  <text x="580" y="138" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Supervise parallel Codex threads</text>
  <text x="580" y="151" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Built-in worktrees, Git, automations</text>
  <text x="580" y="164" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">Organize work across projects</text>
</svg>

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://developers.openai.com/codex">developers.openai.com/codex</a>
</div>

---

# Claude's Two Surfaces → Same Engine, Different UX

<div class="relative mt-4" style="height: 420px;">
  <img src="/images/claude-code-screenshot.png" class="absolute rounded shadow-lg border border-gray-600" style="left: 60px; top: 0px; width: 380px; z-index: 1;" />
  <div class="absolute text-sm font-bold opacity-70" style="left: 195px; top: 290px; z-index: 1;">Claude Code (CLI)</div>
  <img src="/images/cowork-screenshot.png" class="absolute rounded shadow-lg border border-gray-600" style="left: 380px; top: 50px; width: 380px; z-index: 2;" />
  <div class="absolute text-sm font-bold opacity-70" style="left: 510px; top: 340px; z-index: 2;">Cowork (Desktop)</div>
</div>

---

# Claude: Comparison of Two Surfaces

<div class="flex gap-8 items-center">
<div class="flex-1">

<svg viewBox="0 0 360 220" xmlns="http://www.w3.org/2000/svg" class="w-full">
  <style>
    .layer-label { font-family: sans-serif; font-size: 13px; text-anchor: middle; dominant-baseline: central; }
    .detail { font-family: sans-serif; font-size: 9px; text-anchor: middle; dominant-baseline: central; fill: #555; }
  </style>
  <!-- Claude Code layer (inner) -->
  <rect x="60" y="70" width="240" height="100" rx="12" fill="#dbeafe" stroke="#3b82f6" stroke-width="2"/>
  <text x="180" y="105" class="layer-label" font-weight="bold" fill="#1e40af">Claude Code</text>
  <text x="180" y="125" class="detail">CLI · Bash/Read/Write/Edit · CLAUDE.md</text>
  <text x="180" y="140" class="detail">Manual context · 1M tokens · Full control</text>

  <!-- Cowork layer (outer) -->
  <rect x="15" y="20" width="330" height="190" rx="16" fill="none" stroke="#8b5cf6" stroke-width="2.5" stroke-dasharray="6,3"/>
  <text x="180" y="45" class="layer-label" font-weight="bold" fill="#6d28d9">Cowork</text>
  <text x="180" y="195" class="detail" fill="#6d28d9">VM sandbox · Auto-context · Sub-agents · MCP connectors · Plugins</text>
</svg>

</div>
<div class="flex-1 text-sm">

**Cowork wraps Claude Code** with additional infrastructure for non-developers:

- Full **VM isolation** (host-native virtualization)
- **Automatic** context management — no `/compact` or `/clear`
- **Parallel sub-agents** for complex tasks
- **Three-tier permissions** (none → folder-scoped → explicit approval)
- MCP connectors, plugins, MCP Apps

Built with Claude Code in ~1.5 weeks — humans designed the architecture, agents wrote the code.

</div>
</div>

---

# Emerging Harness Patterns

<div class="flex gap-8 mt-2">
<div class="flex-1">

### Spec-Driven Development

Specs as the **source of truth** — agents code against contracts, not just prompts.

- **GitHub Spec Kit** — Open-source templates for Copilot, Claude Code, Gemini CLI, Cursor, Windsurf
- **Kiro** (Amazon/AWS) — IDE that translates natural language → requirements (EARS notation) → implementation plans → validated code

</div>
<div class="flex-1">

### AI-Powered Design & Prototyping

From **natural language or mockups** directly to working apps.

- **Google Stitch** — Voice-driven "vibe design" canvas, generates HTML/CSS/Tailwind, exports to Figma
- **Antigravity** (Google AI Studio) — Full-stack agent: text prompts → production-ready web apps with auth & data
- **Firebase Studio** — Screenshots or descriptions → working apps from framework templates

</div>
</div>

<div class="mt-4 text-sm opacity-70">

**The trend:** Harnesses are moving upstream — from code generation to requirements capture and UI design.

</div>

---

# Claude Code Auto Mode: Safety vs. Usability

Users approve **93%** of permission prompts — approval fatigue is real.

<div class="flex gap-6 items-center">
<div class="w-1/2">
<img src="/images/auto-mode-fig1.webp" class="rounded shadow" />
</div>
<div class="flex-1">

**Sandboxing** — high security, high maintenance

**Manual prompts** — users stop reading

**Auto mode** — classifiers automate safe decisions, flag dangerous ones

*Released March 24, 2026 — Team plan (research preview). Enterprise & API rolling out.*

</div>
</div>

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://www.anthropic.com/engineering/claude-code-auto-mode">anthropic.com/engineering/claude-code-auto-mode</a>
</div>

---

# Harness Engineering: Claude Code Auto Mode

A two-layer classifier system instead of "approve everything" or "block everything":

<svg viewBox="0 0 700 90" xmlns="http://www.w3.org/2000/svg" class="w-full mt-2">
  <defs>
    <marker id="ah4" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
  </defs>
  <!-- Tool Output -->
  <rect x="0" y="28" width="90" height="36" rx="6" fill="#f3f4f6" stroke="#999" stroke-width="1.5"/>
  <text x="45" y="50" font-family="sans-serif" font-size="10px" text-anchor="middle">Tool Output</text>
  <!-- Arrow → Input Layer -->
  <line x1="90" y1="46" x2="118" y2="46" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah4)"/>
  <!-- Input Layer -->
  <rect x="120" y="20" width="130" height="52" rx="6" fill="#dbeafe" stroke="#3b82f6" stroke-width="1.5"/>
  <text x="185" y="42" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Input Layer:</text>
  <text x="185" y="56" font-family="sans-serif" font-size="9px" text-anchor="middle">Prompt Injection Probe</text>
  <!-- Arrow → Claude -->
  <line x1="250" y1="46" x2="278" y2="46" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah4)"/>
  <text x="264" y="38" font-family="sans-serif" font-size="8px" fill="#666" text-anchor="middle">warns</text>
  <!-- Claude -->
  <rect x="280" y="28" width="70" height="36" rx="6" fill="#e0e7ff" stroke="#6366f1" stroke-width="2"/>
  <text x="315" y="50" font-family="sans-serif" font-size="11px" font-weight="bold" text-anchor="middle">Claude</text>
  <!-- Arrow → Output Layer (action) -->
  <line x1="350" y1="38" x2="408" y2="38" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah4)"/>
  <text x="379" y="30" font-family="sans-serif" font-size="8px" fill="#666" text-anchor="middle">action</text>
  <!-- Arrow ← Output Layer (block + explain) -->
  <line x1="410" y1="56" x2="352" y2="56" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah4)"/>
  <text x="379" y="70" font-family="sans-serif" font-size="8px" fill="#666" text-anchor="middle">block + explain</text>
  <!-- Output Layer -->
  <rect x="410" y="20" width="130" height="52" rx="6" fill="#fef3c7" stroke="#d97706" stroke-width="1.5"/>
  <text x="475" y="42" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Output Layer:</text>
  <text x="475" y="56" font-family="sans-serif" font-size="9px" text-anchor="middle">Transcript Classifier</text>
  <!-- Arrow → Execute -->
  <line x1="540" y1="46" x2="578" y2="46" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah4)"/>
  <text x="559" y="38" font-family="sans-serif" font-size="8px" fill="#666" text-anchor="middle">allow</text>
  <!-- Execute -->
  <rect x="580" y="28" width="80" height="36" rx="6" fill="#dcfce7" stroke="#16a34a" stroke-width="1.5"/>
  <text x="620" y="50" font-family="sans-serif" font-size="11px" font-weight="bold" text-anchor="middle">Execute</text>
</svg>

**What it catches:** scope escalation, credential exploration, unauthorized data sharing, security bypass attempts

**What it misses (17% false-negative rate):** ambiguous "blast radius" — e.g., does "clean up the PR" authorize a force-push?

Design choice: strip assistant messages from classifier input so the agent can't talk the classifier into approving dangerous actions.

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://www.anthropic.com/engineering/claude-code-auto-mode">anthropic.com/engineering/claude-code-auto-mode</a>
</div>

---

# Harness Design: Multi-Agent Patterns

Anthropic's Prithvi Rajasekaran on building long-running coding agents:

A single agent evaluating its own work is too optimistic. Solution: **three separate agents**, inspired by GANs:

<svg viewBox="0 0 650 100" xmlns="http://www.w3.org/2000/svg" class="w-full mt-2">
  <defs>
    <marker id="ah3" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
  </defs>
  <!-- Planner -->
  <rect x="10" y="25" width="140" height="50" rx="6" fill="#dbeafe" stroke="#3b82f6" stroke-width="1.5"/>
  <text x="80" y="44" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Agent 1:</text>
  <text x="80" y="60" font-family="sans-serif" font-size="12px" text-anchor="middle">Planner</text>
  <!-- Arrow: Planner → Generator -->
  <line x1="150" y1="50" x2="238" y2="50" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah3)"/>
  <text x="194" y="42" font-family="sans-serif" font-size="9px" fill="#666" text-anchor="middle">spec</text>
  <!-- Generator -->
  <rect x="240" y="25" width="140" height="50" rx="6" fill="#e0e7ff" stroke="#6366f1" stroke-width="1.5"/>
  <text x="310" y="44" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Agent 2:</text>
  <text x="310" y="60" font-family="sans-serif" font-size="12px" text-anchor="middle">Generator</text>
  <!-- Arrow: Generator → Evaluator -->
  <line x1="380" y1="42" x2="468" y2="42" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah3)"/>
  <text x="424" y="34" font-family="sans-serif" font-size="9px" fill="#666" text-anchor="middle">code</text>
  <!-- Arrow: Evaluator → Generator (critique) -->
  <line x1="470" y1="60" x2="382" y2="60" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah3)"/>
  <text x="424" y="76" font-family="sans-serif" font-size="9px" fill="#666" text-anchor="middle">critique</text>
  <!-- Evaluator -->
  <rect x="470" y="25" width="140" height="50" rx="6" fill="#fef3c7" stroke="#d97706" stroke-width="1.5"/>
  <text x="540" y="44" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Agent 3:</text>
  <text x="540" y="60" font-family="sans-serif" font-size="12px" text-anchor="middle">Evaluator</text>
</svg>

- One agent alone ($9, 20 min) → broken, unusable code
- Three-agent harness ($200, 6 hrs) → fully working applications
- Models exhibit "context anxiety" — wrapping up early as context fills
- Context *resets* work better than context *compaction* for long tasks

*"Find the simplest solution possible, and only increase complexity when needed."*

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://www.anthropic.com/engineering/harness-design-long-running-apps">anthropic.com/engineering/harness-design-long-running-apps</a>
</div>

---

<style>
table { font-size: 0.8em; }
h1 { font-size: 1.4em !important; }
</style>

# Two Philosophies of Harness Design

| | **Claude Code** (Anthropic) | **Codex** (OpenAI) |
|---|---|---|
| Core idea | "Bash is all you need" | "The repo is the knowledge store" |
| Tools | Minimal: Bash, Read, Write, Edit, Glob, Grep | Sandboxed envs, linters, execution plans, observability |
| Context source | File system — model navigates with basic tools | Repository — if it's not checked in, it doesn't exist |
| Harness role | Thin wrapper; trust the model | Rigid architecture with enforced boundaries + automated cleanup |
| Demand on dev | Write good code; model figures it out | Push all knowledge into repo: docs, plans, decisions, specs |
| Key file | `CLAUDE.md` — project instructions | `AGENTS.md` as table of contents → structured `docs/` tree |

Both work. Different bets on where the intelligence lives.

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://openai.com/index/harness-engineering/">openai.com/index/harness-engineering</a>
</div>

---

# "Garbage Collection" for Technical Debt

OpenAI's team spent 20% of their week manually cleaning up "AI slop." That didn't scale.

Their solution: **encode taste as rules, then automate enforcement.**

<svg viewBox="0 0 700 110" xmlns="http://www.w3.org/2000/svg" class="w-full mt-2">
  <defs>
    <marker id="ah6" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
  </defs>
  <!-- Golden Principles -->
  <rect x="0" y="22" width="120" height="50" rx="6" fill="#fef3c7" stroke="#d97706" stroke-width="1.5"/>
  <text x="60" y="44" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Golden</text>
  <text x="60" y="58" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Principles</text>
  <!-- Arrow → Custom Linters -->
  <line x1="120" y1="36" x2="148" y2="36" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah6)"/>
  <!-- Arrow → Structural Tests -->
  <line x1="120" y1="58" x2="148" y2="58" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah6)"/>
  <!-- Custom Linters -->
  <rect x="150" y="16" width="110" height="30" rx="6" fill="#dbeafe" stroke="#3b82f6" stroke-width="1.5"/>
  <text x="205" y="35" font-family="sans-serif" font-size="10px" text-anchor="middle">Custom Linters</text>
  <!-- Structural Tests -->
  <rect x="150" y="50" width="110" height="30" rx="6" fill="#dbeafe" stroke="#3b82f6" stroke-width="1.5"/>
  <text x="205" y="69" font-family="sans-serif" font-size="10px" text-anchor="middle">Structural Tests</text>
  <!-- Arrow Linters → Agent Tasks -->
  <line x1="260" y1="31" x2="298" y2="42" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah6)"/>
  <!-- Arrow Tests → Agent Tasks -->
  <line x1="260" y1="65" x2="298" y2="52" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah6)"/>
  <!-- Recurring Agent Tasks -->
  <rect x="300" y="26" width="130" height="40" rx="6" fill="#e0e7ff" stroke="#6366f1" stroke-width="1.5"/>
  <text x="365" y="42" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Recurring</text>
  <text x="365" y="56" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Agent Tasks</text>
  <!-- Arrow → Cleanup PRs -->
  <line x1="430" y1="46" x2="468" y2="46" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah6)"/>
  <text x="449" y="80" font-family="sans-serif" font-size="8px" fill="#666" text-anchor="middle">scan for drift</text>
  <!-- Cleanup PRs -->
  <rect x="470" y="26" width="100" height="40" rx="6" fill="#f3f4f6" stroke="#999" stroke-width="1.5"/>
  <text x="520" y="50" font-family="sans-serif" font-size="10px" text-anchor="middle">Cleanup PRs</text>
  <!-- Arrow → Auto-merge -->
  <line x1="570" y1="46" x2="608" y2="46" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah6)"/>
  <text x="589" y="80" font-family="sans-serif" font-size="7px" fill="#666" text-anchor="middle">reviewed &lt;1 min</text>
  <!-- Auto-merge -->
  <rect x="610" y="28" width="80" height="36" rx="6" fill="#dcfce7" stroke="#16a34a" stroke-width="1.5"/>
  <text x="650" y="50" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Auto-merge</text>
</svg>

- Enforce architecture mechanically: dependency directions, naming conventions, file size limits
- Linter error messages written as remediation instructions for agents
- Technical debt paid continuously in small increments, not painful bursts
- Human taste captured once, enforced on every line of code going forward

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://openai.com/index/harness-engineering/">openai.com/index/harness-engineering</a>
</div>

---

# The Harness Layer Is Evolving Fast

Harnesses are getting smarter about what the model sees and how it acts.

Example: Anthropic's "Advanced Tool Use" (beta, March 2026)

| Problem | Solution | Impact |
|---|---|---|
| Too many tools loaded upfront | **Tool Search** — find tools on-demand | 85% fewer tokens |
| Too many round-trips to the model | **Programmatic Calling** — orchestrate in code | 37% fewer tokens |
| Schema alone isn't enough | **Tool Use Examples** — show, don't just describe | 72% → 90% accuracy |


<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://www.anthropic.com/engineering/advanced-tool-use">anthropic.com/engineering/advanced-tool-use</a>
</div>

---

# What's Available at Janelia

**OpenAI (HHMI Enterprise)**
- Organization-wide token pool for HQ+Janelia
- ChatGPT, Codex cloud agent, Codex CLI
- It's a big pool. HQ more ChatGPT-oriented.

**Anthropic (Claude)**
- Enterprise collaboration in progress
- Currently: Claude Max plans or API access
- Soon: Enterprise individualized "consumption" model (not Max)

**Google (Gemini)**
- Limited Enterprise licenses (~$20/mo Pro) available through Support
- Licensing more fractured. Unsure about Ultra and above.
- Gemini CLI is free with personal Google accounts (1K requests/day)

<div class="text-lg absolute right-8 top-1/2 -translate-y-1/2 text-left">Disclaimer:<br/>As of Apr 2, 2026</div>

---
layout: section
---

# Part II: Common Approaches

Patterns for AI-Assisted Development

---

# Claude Best Practices: Explore → Plan → Code → Verify

The single highest-leverage pattern across all harnesses:

<svg viewBox="0 0 700 80" xmlns="http://www.w3.org/2000/svg" class="w-full mt-2">
  <defs>
    <marker id="ah7" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
  </defs>
  <!-- Explore -->
  <rect x="10" y="15" width="100" height="36" rx="6" fill="#dbeafe" stroke="#3b82f6" stroke-width="1.5"/>
  <text x="60" y="37" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Explore</text>
  <!-- Arrow → Plan -->
  <line x1="110" y1="33" x2="148" y2="33" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah7)"/>
  <!-- Plan -->
  <rect x="150" y="15" width="100" height="36" rx="6" fill="#e0e7ff" stroke="#6366f1" stroke-width="1.5"/>
  <text x="200" y="37" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Plan</text>
  <!-- Arrow → Code -->
  <line x1="250" y1="33" x2="288" y2="33" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah7)"/>
  <!-- Code -->
  <rect x="290" y="15" width="100" height="36" rx="6" fill="#fef3c7" stroke="#d97706" stroke-width="1.5"/>
  <text x="340" y="37" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Code</text>
  <!-- Arrow → Verify -->
  <line x1="390" y1="33" x2="428" y2="33" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah7)"/>
  <!-- Verify -->
  <rect x="430" y="15" width="100" height="36" rx="6" fill="#fce7f3" stroke="#db2777" stroke-width="1.5"/>
  <text x="480" y="37" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Verify</text>
  <!-- Arrow → Done -->
  <line x1="530" y1="33" x2="568" y2="33" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah7)"/>
  <!-- Done -->
  <rect x="570" y="15" width="80" height="36" rx="6" fill="#dcfce7" stroke="#16a34a" stroke-width="1.5"/>
  <text x="610" y="37" font-family="sans-serif" font-size="12px" font-weight="bold" text-anchor="middle">Done</text>
  <!-- Arrow: Verify → Code (tests fail, curved below) -->
  <path d="M 460,51 C 460,72 360,72 340,51" fill="none" stroke="#e11d48" stroke-width="1.5" marker-end="url(#ah7)"/>
  <text x="400" y="78" font-family="sans-serif" font-size="8px" fill="#e11d48" text-anchor="middle">tests fail</text>
</svg>

**Explore** — Read code, ask questions, understand the system. Use Plan Mode or Ask Mode.

**Plan** — Create an implementation plan *before* writing code. Edit the plan yourself if needed.

**Code** — Let the agent implement against the plan. Reference specific files and patterns.

**Verify** — Give the agent a way to check its own work: tests, screenshots, linters, build commands. This is the single highest-leverage thing you can do.

*Skip the plan for small, obvious tasks. Use it when scope is unclear or changes span multiple files.*

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://code.claude.com/docs/en/best-practices">code.claude.com/docs/en/best-practices</a>
</div>

---

# Claude Hierarchy of Instructions

<img src="/images/claude-hierarchy-instructions.png" class="mx-auto mt-auto mb-0" style="max-height: 92%; max-width: 98%; object-fit: contain;" />

---

# Common Failure Patterns (and Fixes)

Recognizing these early saves hours:

**The kitchen sink session** — One task, then something unrelated, then back to the first. Context fills with noise.
→ `/clear` between unrelated tasks.

**Correcting over and over** — Claude does it wrong, you correct, still wrong, correct again. Context polluted with failed approaches.
→ After two failed corrections, `/clear` and write a better initial prompt.

**The over-specified CLAUDE.md** — Too long, Claude ignores half of it. Important rules get lost.
→ Ruthlessly prune. If Claude already does it correctly without the rule, delete it.

**The trust-then-verify gap** — Plausible-looking code that doesn't handle edge cases.
→ Always provide verification. If you can't verify it, don't ship it.

**The infinite exploration** — "Investigate this" without scoping. Claude reads hundreds of files.
→ Scope narrowly, or delegate to a subagent so exploration doesn't consume your main context.

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://code.claude.com/docs/en/best-practices">code.claude.com/docs/en/best-practices</a>
</div>

---

# OpenAI Best Practices for AI-Assisted Coding

From OpenAI's internal engineering teams — but these generalize across harnesses:

**Start with a plan, then code** — Use "Ask mode" first to generate an implementation plan. Then switch to coding mode with that plan as input. Keeps the agent grounded.

**Structure prompts like GitHub Issues** — Include file paths, component names, diffs, and doc snippets. "Implement this the same way it's done in [module X]" improves results.

**Use the task queue as a backlog** — Fire off tangential ideas, partial work, incidental fixes. No pressure for a full PR in one go. Review when you're back in focus.

**Iterate on the environment, not the prompt** — Build errors? Fix the dev environment config, not the prompt. Startup scripts, env vars, and internet access reduce error rates significantly.

**"Best of N" for hard problems** — Generate multiple responses for a single task, review several iterations, combine the best parts.

**Keep tasks well-scoped** — Sweet spot: tasks that would take you about an hour or a few hundred lines of code.

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://cdn.openai.com/pdf/6a2631dc-783e-479b-b1a4-af0cfbd38630/how-openai-uses-codex.pdf">OpenAI: "How OpenAI uses Codex" (PDF)</a>
</div>

---

# How OpenAI Engineers Actually Use Codex

Seven use cases from OpenAI's internal teams (Security, Frontend, API, Infrastructure):

| Use Case | What they do |
|---|---|
| **Code understanding** | Paste a stack trace, ask where the auth flow lives — faster than grep |
| **Refactoring & migrations** | Swap legacy patterns across dozens of files, open the PR in minutes |
| **Performance optimization** | Flag hot paths, draft batched queries — "5 min prompt saves 30 min work" |
| **Test coverage** | Point at low-coverage modules overnight, wake up to unit-test PRs |
| **Development velocity** | Scaffold boilerplate, triage bugs, ship low-priority fixes from backlog |
| **Staying in flow** | Fire off drive-by fixes as background tasks, review PRs when free |
| **Exploration & ideation** | Explore alternative architectures, find similar bugs across codebase |

These patterns apply equally to Claude Code, Gemini CLI, and other harnesses.

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://cdn.openai.com/pdf/6a2631dc-783e-479b-b1a4-af0cfbd38630/how-openai-uses-codex.pdf">OpenAI: "How OpenAI uses Codex" (PDF)</a>
</div>

---

# Case Study: gstack — A Shareable Skills Library

<div class="text-sm">

Garry Tan (YC CEO) open-sourced **23 slash-command skills** built on the **SKILL.md standard** — works with any agent that supports it (Codex CLI, Claude Code, Gemini CLI, Cursor, Factory Droid).

</div>

<div class="flex gap-6 mt-1">
<div class="flex-1">

**Think → Plan → Build → Review → Test → Ship → Reflect**

| Role | Skill |
|---|---|
| YC Office Hours | `/office-hours` — reframes problem before coding |
| CEO / Founder | `/plan-ceo-review` — challenges scope |
| Eng Manager | `/plan-eng-review` — locks architecture |
| Staff Engineer | `/review` — finds bugs that pass CI |
| QA Lead | `/qa` — real browser testing |
| Release Engineer | `/ship` — tests, coverage audit, PR |
| Security Officer | `/cso` — OWASP + STRIDE audits |

</div>
<div class="flex-1">

**Why it matters:**

- Skills are **Markdown files** in `.agents/skills/` — portable, forkable, composable
- Agent-agnostic via the **SKILL.md standard** (`--host codex`, `--host auto`)
- Encodes **process as code** — the sprint structure is the product
- Supports 10–15 parallel agent sessions
- 62K+ stars, 8K+ forks, MIT licensed

**The pattern:** Capture your team's engineering taste once, let agents enforce it on every line of code.

</div>
</div>

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://github.com/garrytan/gstack">github.com/garrytan/gstack</a>
</div>

<style scoped>
p, li { font-size: 0.85em; line-height: 1.4; margin: 0.15em 0; }
table { font-size: 0.8em; }
th, td { padding: 0.2em 0.5em; }
h1 { margin-bottom: 0.1em; }
</style>

---

# Claude Skills: Progressive Disclosure Architecture

Skills are specialized folders (instructions, scripts, resources) that teach Claude to perform tasks repeatably — available across Claude.ai, Claude Code, and the API.

<svg viewBox="0 0 700 120" xmlns="http://www.w3.org/2000/svg" class="w-full mt-2">
  <defs>
    <marker id="ah9" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
  </defs>
  <!-- Step 1 -->
  <rect x="0" y="20" width="180" height="50" rx="6" fill="#dcfce7" stroke="#16a34a" stroke-width="1.5"/>
  <text x="90" y="40" font-family="sans-serif" font-size="11px" font-weight="bold" text-anchor="middle">1. Metadata scan</text>
  <text x="90" y="56" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">~100 tokens per skill</text>
  <!-- Arrow -->
  <line x1="180" y1="45" x2="228" y2="45" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah9)"/>
  <text x="204" y="36" font-family="sans-serif" font-size="8px" fill="#666" text-anchor="middle">match?</text>
  <!-- Step 2 -->
  <rect x="230" y="20" width="200" height="50" rx="6" fill="#fef3c7" stroke="#d97706" stroke-width="1.5"/>
  <text x="330" y="40" font-family="sans-serif" font-size="11px" font-weight="bold" text-anchor="middle">2. Full instructions</text>
  <text x="330" y="56" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">&lt;5K tokens — SKILL.md loaded</text>
  <!-- Arrow -->
  <line x1="430" y1="45" x2="478" y2="45" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah9)"/>
  <text x="454" y="36" font-family="sans-serif" font-size="8px" fill="#666" text-anchor="middle">needed?</text>
  <!-- Step 3 -->
  <rect x="480" y="20" width="200" height="50" rx="6" fill="#e0e7ff" stroke="#6366f1" stroke-width="1.5"/>
  <text x="580" y="40" font-family="sans-serif" font-size="11px" font-weight="bold" text-anchor="middle">3. Bundled resources</text>
  <text x="580" y="56" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">scripts, files, code — on demand</text>
  <!-- Benefit label -->
  <text x="350" y="100" font-family="sans-serif" font-size="10px" fill="#555" text-anchor="middle" font-style="italic">Multiple skills stay available without overwhelming the context window</text>
</svg>

<div class="flex gap-8 mt-2">
<div class="flex-1">

**Official skills:** docx, pdf, pptx, xlsx, algorithmic-art, canvas-design, mcp-builder, webapp-testing, skill-creator

</div>
<div class="flex-1">

**Community:** [awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) — curated directory of skills, tools, and resources

</div>
</div>

<style scoped>
p, li { font-size: 0.85em; line-height: 1.4; margin: 0.15em 0; }
h1 { margin-bottom: 0.2em; }
</style>

---

# Providing Large Codebase Context to AI

Two dominant patterns for helping AI understand codebases too large for any context window:

<div class="flex gap-6 mt-2">
<div class="flex-1">

<div class="text-lg font-bold">RAG (Retrieval-Augmented Generation)</div>

Embed code chunks as vectors, retrieve by semantic similarity at query time.

Used by: GitHub Copilot (code search + RAG), Augment Code (knowledge graph + RAG)

<div class="my-1"><span class="text-green-600">✓</span> Automated — no human curation needed</div>
<div class="my-1"><span class="text-green-600">✓</span> Scales to large, changing codebases</div>
<div class="my-1"><span class="text-red-500">✗</span> Chunking destroys structural relationships</div>
<div class="my-1"><span class="text-red-500">✗</span> Finds *similar-looking* code, not *architecturally-related* code</div>

</div>
<div class="flex-1">

<div class="text-lg font-bold">Hierarchical Maps (llms.txt / CLAUDE.md)</div>

Human-curated indexes at multiple levels of detail. Agent navigates from summaries to specifics.

Used by: Claude Code (docs map), llmstxt.org standard, CLAUDE.md files

<div class="my-1"><span class="text-green-600">✓</span> Preserves structure and relationships</div>
<div class="my-1"><span class="text-green-600">✓</span> Agent navigates purposefully, not blindly</div>
<div class="my-1"><span class="text-red-500">✗</span> Requires curation and maintenance</div>
<div class="my-1"><span class="text-red-500">✗</span> Coverage depends on author effort</div>

</div>
</div>

<div class="flex justify-end">
<svg viewBox="0 0 500 90" xmlns="http://www.w3.org/2000/svg" class="mt-1" style="width: 55%;">
  <defs>
    <marker id="ah10" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
  </defs>
  <!-- Map hierarchy: Root Index → Summaries → Full Code -->
  <rect x="5" y="12" width="120" height="36" rx="6" fill="#e0e7ff" stroke="#6366f1" stroke-width="1.5"/>
  <text x="65" y="28" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Root Index</text>
  <text x="65" y="40" font-family="sans-serif" font-size="8px" fill="#555" text-anchor="middle">titles + links</text>
  <line x1="125" y1="30" x2="163" y2="30" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah10)"/>
  <rect x="165" y="12" width="140" height="36" rx="6" fill="#fef3c7" stroke="#d97706" stroke-width="1.5"/>
  <text x="235" y="28" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Repo Summaries</text>
  <text x="235" y="40" font-family="sans-serif" font-size="8px" fill="#555" text-anchor="middle">headings + descriptions</text>
  <line x1="305" y1="30" x2="343" y2="30" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah10)"/>
  <rect x="345" y="12" width="140" height="36" rx="6" fill="#dcfce7" stroke="#16a34a" stroke-width="1.5"/>
  <text x="415" y="28" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Full Code / Docs</text>
  <text x="415" y="40" font-family="sans-serif" font-size="8px" fill="#555" text-anchor="middle">on demand</text>
  <text x="250" y="75" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle" font-style="italic">Maps: progressive detail — agent reads only what it needs</text>
</svg>
</div>

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://llmstxt.org">llmstxt.org</a> · <a href="https://simonwillison.net/2025/Oct/24/claude-code-docs-map/">Simon Willison on Claude Code's docs map</a> · <a href="https://code.claude.com/docs/en/claude_code_docs_map.md">Claude Code docs map</a>
</div>

<style scoped>
p, li { font-size: 0.82em; line-height: 1.35; margin: 0.15em 0; }
h1 { margin-bottom: 0.1em; }
</style>

---
layout: section
---

# Part III: Issues

Context Rot, Model Degradation, and the Feedback Loop

---

# Context Rot: Death by a Thousand Tokens

As a session grows, the model's effective intelligence degrades — not because it gets dumber, but because signal gets buried in noise.

<svg viewBox="0 0 700 80" xmlns="http://www.w3.org/2000/svg" class="w-full mt-2">
  <defs>
    <marker id="ah8" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
  </defs>
  <!-- Fresh session -->
  <rect x="0" y="10" width="120" height="42" rx="6" fill="#dcfce7" stroke="#16a34a" stroke-width="1.5"/>
  <text x="60" y="27" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Fresh session</text>
  <text x="60" y="41" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">high signal</text>
  <!-- Arrow + label below -->
  <line x1="120" y1="31" x2="168" y2="31" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah8)"/>
  <text x="144" y="66" font-family="sans-serif" font-size="7px" fill="#666" text-anchor="middle">outputs accumulate</text>
  <!-- Mid session -->
  <rect x="170" y="10" width="130" height="42" rx="6" fill="#fef3c7" stroke="#d97706" stroke-width="1.5"/>
  <text x="235" y="27" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Mid session</text>
  <text x="235" y="41" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">compaction triggers</text>
  <!-- Arrow + label below -->
  <line x1="300" y1="31" x2="348" y2="31" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah8)"/>
  <text x="324" y="66" font-family="sans-serif" font-size="7px" fill="#666" text-anchor="middle">summaries replace detail</text>
  <!-- Late session -->
  <rect x="350" y="10" width="140" height="42" rx="6" fill="#fed7aa" stroke="#ea580c" stroke-width="1.5"/>
  <text x="420" y="27" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Late session</text>
  <text x="420" y="41" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">original intent blurred</text>
  <!-- Arrow + label below -->
  <line x1="490" y1="31" x2="538" y2="31" fill="none" stroke="#666" stroke-width="1.5" marker-end="url(#ah8)"/>
  <text x="514" y="66" font-family="sans-serif" font-size="7px" fill="#666" text-anchor="middle">assumptions compound</text>
  <!-- Drift -->
  <rect x="540" y="10" width="130" height="42" rx="6" fill="#fecaca" stroke="#dc2626" stroke-width="1.5"/>
  <text x="605" y="27" font-family="sans-serif" font-size="10px" font-weight="bold" text-anchor="middle">Drift</text>
  <text x="605" y="41" font-family="sans-serif" font-size="9px" fill="#555" text-anchor="middle">model works against you</text>
</svg>

<div class="flex gap-8 mt-1">
<div class="flex-1">

**What rots:**
- Original intent and constraints get summarized away
- Failed approaches stay in context, biasing toward same mistakes
- Tool outputs crowd out your instructions
- After compaction: summary of a summary

</div>
<div class="flex-1">

**What helps:**
- Start fresh (`/clear`) for genuinely new tasks
- Keep sessions focused on one goal
- Front-load constraints in CLAUDE.md (survives compaction)
- Use subagents so main context stays clean

</div>
</div>

---

# Context Rot in Practice

A real pattern that wastes hours:

<svg viewBox="0 0 720 195" xmlns="http://www.w3.org/2000/svg" class="w-full mt-2">
  <style>
    .box { rx: 6; ry: 6; stroke: #999; stroke-width: 1.5; }
    .label { font-family: sans-serif; font-size: 11px; text-anchor: middle; dominant-baseline: central; }
    .arrow { fill: none; stroke: #666; stroke-width: 1.5; marker-end: url(#arrowhead); }
    .warn-box { rx: 6; ry: 6; stroke: #e67e22; stroke-width: 2; }
    .fail-box { rx: 6; ry: 6; stroke: #e74c3c; stroke-width: 2; }
  </style>
  <defs>
    <marker id="arrowhead" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <polygon points="0 0, 8 3, 0 6" fill="#666"/>
    </marker>
  </defs>

  <!-- Column 1: down -->
  <rect x="20" y="10" width="180" height="32" class="box" fill="#dbeafe"/>
  <text x="110" y="26" class="label" font-weight="bold">Task: "Fix login bug"</text>
  <line x1="110" y1="42" x2="110" y2="56" class="arrow"/>

  <rect x="20" y="56" width="180" height="32" class="box" fill="#f3f4f6"/>
  <text x="110" y="72" class="label">Agent reads 12 files</text>
  <line x1="110" y1="88" x2="110" y2="102" class="arrow"/>

  <rect x="20" y="102" width="180" height="32" class="box" fill="#fee2e2"/>
  <text x="110" y="118" class="label">Fix #1 — wrong approach</text>
  <line x1="110" y1="134" x2="110" y2="148" class="arrow"/>

  <rect x="20" y="148" width="180" height="32" class="box" fill="#fef9c3"/>
  <text x="110" y="164" class="label">You: "No, try X instead"</text>

  <!-- Arrow right from col 1 to col 2 -->
  <line x1="200" y1="164" x2="270" y2="164" class="arrow"/>

  <!-- Column 2: up -->
  <rect x="270" y="148" width="180" height="32" class="box" fill="#f3f4f6"/>
  <text x="360" y="164" class="label">Agent reads 8 more files</text>
  <line x1="360" y1="148" x2="360" y2="134" class="arrow"/>

  <rect x="270" y="102" width="180" height="32" class="box" fill="#fee2e2"/>
  <text x="360" y="118" class="label">Fix #2 — closer but off</text>
  <line x1="360" y1="102" x2="360" y2="88" class="arrow"/>

  <rect x="270" y="56" width="180" height="32" class="box" fill="#fef9c3"/>
  <text x="360" y="72" class="label">You: "Issue is in auth.ts"</text>

  <!-- Arrow right from col 2 to col 3 -->
  <line x1="450" y1="72" x2="520" y2="72" class="arrow"/>

  <!-- Column 3: down -->
  <rect x="520" y="56" width="180" height="32" class="warn-box" fill="#ffedd5"/>
  <text x="610" y="72" class="label" font-weight="bold">Compaction triggers</text>
  <line x1="610" y1="88" x2="610" y2="102" class="arrow"/>

  <rect x="520" y="102" width="180" height="32" class="fail-box" fill="#fecaca"/>
  <text x="610" y="118" class="label" font-weight="bold">Fix #3 — repeats #1</text>
</svg>

Context is now ~80% failed attempts. The model is optimizing against polluted history.

**The fix:** After two failed corrections, `/clear` and write a single, precise prompt incorporating what you've learned. Five minutes of prompt writing beats thirty minutes of correction loops.

---

# Model Degradation: Why Does It Feel Dumber Sometimes?

The model is a black box. When quality seems to drop, the cause is rarely what you think.

**It's probably not the model:**
- **Context pollution** — noise accumulated over a long session drowns out your intent
- **Prompt ambiguity** — your request is clear to you but underspecified for the model
- **Compaction artifacts** — after auto-compaction, the model lost critical details
- **Task complexity creep** — what started small became multi-file, multi-concern

**It might be the model:**
- **Model version changes** — providers update models without notice; behavior shifts
- **Capacity-dependent routing** — some providers route to smaller models under load
- **Regression in specific domains** — a new model version may improve overall but regress on your particular use case

When in doubt: start a fresh session and test with a clean prompt.

---

# The Feedback Loop: Anthropic Is Listening

Anthropic tracks user satisfaction signals from conversations — including frustration.

When you curse at Claude, that interaction is flagged as a **negative satisfaction signal**. Claude doesn't change its behavior in response to cursing, but the data feeds back into model evaluation and training priorities.

What Anthropic captures:
- Thumbs up/down on responses
- Conversation-level sentiment (including profanity as frustration signal)
- Retry and regeneration patterns
- Session abandonment timing

**Why this matters for developers:**
- Your frustration literally shapes the next model version
- Specific, constructive feedback (thumbs down + explanation) is far more actionable than cursing
- The 👎 button is your most powerful tool for improving AI coding assistants

*The models are trained on what we collectively tolerate and reject.*

---
layout: section
---

# Part IV: Extraordinary Examples

What People Are Actually Building

---

<style scoped>
h1 { font-size: 1.3em !important; }
p, li { font-size: 0.85em; }
ul { margin-top: 0.1em; }
p { margin-bottom: 0.2em; }
</style>

# The Claude Code Leak → Agent-Driven Rewrites

A missing `.npmignore` shipped 512K lines of unobfuscated TypeScript in the npm package. What happened next:

**The leak (March 31, 2026):**
- Anthropic: "a release packaging issue caused by human error, not a security breach"
- Sigrid Jin (@realsigridjin), exhausted after running two Korean hackathons in SF, cloned the repo, went to sleep
- Woke up to massive attention — and his girlfriend (a copyright lawyer) begging him to take it down

**The pivot:**
- Team decision: "What if we have agents **rewrite the entire thing in Python**? Surely that's more legal..."
- Clean-room Python rewrite using **oh-my-codex** (OmX), an AI workflow tool built on OpenAI Codex
- Board a plane to South Korea
- Mid-flight, one team member decides Python is too slow — starts rewriting **all of it into Rust**

**The result: "claw-code"**
- **50K GitHub stars in two hours** — fastest-growing repo in GitHub history
- Anthropic filed **8,100+ DMCA takedowns**
- The knock-off now has more stars than the original Claude Code repo

---

<style scoped>
h1 { font-size: 1.3em !important; }
table { font-size: 0.78em; }
table td, table th { padding: 0.25em 0.8em; }
table tr:nth-child(even) { background: rgba(255,255,255,0.05); }
p { font-size: 0.8em; margin-bottom: 0.3em; }
</style>

# OpenAI's Zero-Handwritten-Code Experiment

An OpenAI team built and shipped a product with **0 lines of manually-written code**.

| Metric | Value |
|---|---|
| Hand-written code | 0 lines |
| Agent-generated code | ~1 million lines |
| PRs merged | ~1,500 |
| Engineers | 3 (later 7) |
| Throughput | 3.5 PRs / engineer / day |
| Estimated speedup | ~10x vs hand-coding |
| Duration | 5 months (from empty repo, ~Sep 2025 – Feb 2026) |

The product has internal daily users and external alpha testers. It ships, deploys, breaks, and gets fixed — all by agents.

Engineers spent 20% of time cleaning up "AI slop" → solved by automated "garbage collection" (golden principles + recurring agent cleanup tasks).

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://openai.com/index/harness-engineering/">openai.com/index/harness-engineering</a>
</div>

---

<style scoped>
p, li { font-size: 0.85em; line-height: 1.4; margin: 0.15em 0; }
h1 { font-size: 1.3em !important; margin-bottom: 0.2em; }
</style>

# Pretext: AI-Friendly Iteration Against Browser Ground Truth

Cheng Lou's **Pretext** — a JS library that measures and lays out multiline text *without* DOM manipulation, using pure computation.

<div class="flex gap-8 mt-2">
<div class="flex-1">

**The problem:** Measuring text in the browser requires triggering expensive DOM reflows — a bottleneck for any UI that needs text height, line counts, or variable-width layouts.

**The approach:**
- `prepare()` measures text segments once using the canvas font engine as ground truth (~19ms for 500 texts)
- `layout()` computes height, lines, and wrapping with pure arithmetic (~0.09ms for 500 texts)
- No DOM in the hot path — works with Canvas, SVG, or WebGL

</div>
<div class="flex-1">

**Why it's here — the development process:**

Parallel agents trained against real browser rendering for weeks, iterating over and over until output matched Safari, Chrome, and Firefox exactly.

Browser engines provide pixel-perfect ground truth → agents iterate and verify autonomously in parallel → humans focus on architecture, agents grind on correctness.

**Result:** Supports all languages, emoji, bidi text, `pre-wrap`, shrink-wrap sizing, and text flowing around floats.

</div>
</div>

<div class="text-xs opacity-50 absolute bottom-4 right-8">
<a href="https://github.com/chenglou/pretext">github.com/chenglou/pretext</a>
</div>

---
layout: center
---

# Resources & Discussion

**GitHub**: [`JaneliaSciComp/ai-assisted-dev`](https://github.com/JaneliaSciComp/ai-assisted-dev)

Explore the curated resource list and contribute links.
