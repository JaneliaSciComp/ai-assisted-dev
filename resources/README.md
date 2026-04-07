# AI-Assisted Software Development Resources

A curated collection of tools, frameworks, articles, and examples for AI-assisted software development, maintained by the Janelia Research Campus community.

## Table of Contents

- [Harnesses & Tools](#harnesses--tools)
  - [IDE-Integrated](#ide-integrated)
  - [Terminal / Agent-Based](#terminal--agent-based)
  - [Skills & Extensions](#skills--extensions)
  - [Cloud / Autonomous Agents](#cloud--autonomous-agents)
  - [Spec-Driven Development](#spec-driven-development)
  - [AI-Powered Design & Prototyping](#ai-powered-design--prototyping)
  - [Sandboxing & Containment](#sandboxing--containment)
- [Frontier Models](#frontier-models)
- [Approaches & Best Practices](#approaches--best-practices)
- [Extraordinary Examples](#extraordinary-examples)
- [Articles & Blog Posts](#articles--blog-posts)
- [Videos & Talks](#videos--talks)
- [Benchmarks & Evaluation](#benchmarks--evaluation)

---

## Harnesses & Tools

### IDE-Integrated

*AI assistants that work within your editor.*

- [GitHub Copilot](https://github.com/features/copilot) — AI pair programmer integrated into VS Code, JetBrains, and other editors. `tags: ide, autocomplete, github`
- [Cursor](https://www.cursor.com/) — AI-native code editor built on VS Code with deep model integration. `tags: ide, editor, agentic`
- [Windsurf](https://windsurf.com/) — AI-powered IDE (formerly Codeium) with agentic "Cascade" flows. `tags: ide, editor, agentic`
- [Cline](https://github.com/cline/cline) — Open-source autonomous coding agent as a VS Code extension. `tags: ide, open-source, agentic`

### Terminal / Agent-Based

*CLI tools where you give the AI a task and it works autonomously.*

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — Anthropic's CLI agent for agentic coding with Claude. File editing, shell access, Git integration. `tags: cli, agentic, anthropic`
- [Codex CLI](https://github.com/openai/codex) — OpenAI's open-source terminal coding agent built in Rust. `tags: cli, agentic, openai, open-source`
- [Codex (Cloud)](https://openai.com/codex/) — OpenAI's cloud-based async coding agent with sandboxed environments. `tags: cloud, agentic, openai`
- [Gemini CLI](https://github.com/google-gemini/gemini-cli) — Google's open-source terminal agent with Gemini 2.5 Pro. Free tier: 1K requests/day. `tags: cli, agentic, google, open-source, free`
- [Aider](https://aider.chat/) — Open-source AI pair programming in the terminal. Works with multiple models. `tags: cli, open-source, multi-model`
- [Pi](https://pi.dev/) — Minimal, extensible terminal coding agent by Mario Zechner. Works with 15+ AI providers, customizable via TypeScript extensions and skills. `tags: cli, agentic, open-source, multi-model, extensible`
- [Amp](https://ampcode.com/) — Coding agent by Sourcegraph. CLI-based, pay-as-you-go with frontier models. `tags: cli, agentic, sourcegraph, multi-model`

### Skills & Extensions

*Shareable skill libraries and configuration packs that extend agent capabilities.*

- [gstack](https://github.com/garrytan/gstack) — Garry Tan's (YC CEO) open-source skill library: 23 slash-command skills encoding a full sprint process (office hours, CEO/eng/design review, QA, ship, security audits). Built on the SKILL.md standard — works across Codex CLI, Claude Code, Gemini CLI, Cursor, Factory Droid. 62K+ stars. `tags: skills, process, open-source, multi-agent`
- [GitHub Spec Kit](https://github.com/speckit) — Open-source templates for spec-driven development across Copilot, Claude Code, Gemini CLI, Cursor, Windsurf. `tags: specs, templates, open-source, multi-agent`
- [awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) — Curated directory of Claude Skills, tools, and resources. Skills use a progressive disclosure architecture (metadata scan → full instructions → bundled resources) for token efficiency. `tags: skills, claude, curated-list, community`

### Cloud / Autonomous Agents

*Systems designed to work with minimal user interaction beyond specs or task descriptions.*

- [Devin](https://devin.ai/) — AI software engineering agent by Cognition with web-based IDE for monitoring. Assigns tickets, writes code, opens PRs. `tags: cloud, agent, ide`
- [OpenHands](https://github.com/All-Hands-AI/OpenHands) — Open-source platform for AI software agents. `tags: agent, open-source`
- [mini-SWE-agent](https://github.com/SWE-agent/mini-swe-agent) — 100-line Python agent that solves GitHub issues. Successor to SWE-agent, scores >74% on SWE-bench verified. By Princeton/Stanford. `tags: agent, research, open-source, lightweight`

### Spec-Driven Development

*Tools that emphasize specifications as the source of truth for AI-generated code.*

- [GitHub Spec Kit](https://github.com/github/spec-kit) — Open-source toolkit for spec-driven development. Templates for Copilot, Claude Code, Gemini CLI, Cursor, Windsurf. Specs become contracts that agents code against. `tags: spec-driven, open-source, github, workflow`
- [Kiro](https://kiro.dev/) — Amazon/AWS AI-powered IDE built around spec-driven development. Translates natural language into requirements (EARS notation), generates implementation plans, validates against specs. `tags: spec-driven, ide, aws, amazon`

### AI-Powered Design & Prototyping

*AI tools for UI design, prototyping, and full-stack app generation.*

- [Google Stitch](https://stitch.withgoogle.com/) — AI-native UI design canvas from Google Labs. Voice-driven "vibe design," generates HTML/CSS/Tailwind, exports to Figma. Free. `tags: design, ui, google, free`
- [Antigravity](https://aistudio.google.com/) — Full-stack coding agent in Google AI Studio. Turns text prompts into production-ready web apps with persistent data, auth, and external services. `tags: full-stack, google, cloud, agent`
- [Firebase Studio](https://firebase.studio/) — Google's app prototyping agent. Natural language, mockups, or screenshots to working apps using popular framework templates. `tags: prototyping, google, cloud`

### Sandboxing & Containment

*Tools for isolating and constraining AI agents to prevent unintended system changes.*

- [jai](https://jai.scs.stanford.edu/) — Lightweight Linux sandbox for AI agents from Stanford SCS. Contains agents to a working directory with copy-on-write overlays — no Docker required. `tags: sandbox, security, open-source, containment, stanford`

---

## Frontier Models

*The large language models powering AI-assisted development.*

- [Claude (Anthropic)](https://www.anthropic.com/claude) — Opus 4.6, Sonnet 4.6, Haiku 4.5. 200K context. Strong code quality and instruction following. `tags: commercial, api`
- [GPT / Codex (OpenAI)](https://openai.com/) — GPT-4.1, o3/o4-mini reasoning models. 1M context (Codex). Broad ecosystem. `tags: commercial, api`
- [Gemini (Google)](https://ai.google.dev/) — Gemini 2.5 Pro. 1M token context window. Free CLI access. `tags: commercial, api, free-tier`

---

## Approaches & Best Practices

*Guides, patterns, and strategies for effective AI-assisted coding.*

- [Best Practices for Claude Code](https://code.claude.com/docs/en/best-practices) — Comprehensive guide from Anthropic: explore-plan-code-verify workflow, CLAUDE.md best practices, context management, subagents, common failure patterns. `tags: best-practices, anthropic, claude-code, workflow`
- [How OpenAI Uses Codex](https://cdn.openai.com/pdf/6a2631dc-783e-479b-b1a4-af0cfbd38630/how-openai-uses-codex.pdf) — OpenAI's internal use cases and best practices from their own engineering teams: code understanding, refactoring, performance optimization, testing, staying in flow. `tags: best-practices, openai, codex, use-cases`

---

## Extraordinary Examples

*Remarkable demonstrations of what's possible with AI-assisted development.*

- [Pretext](https://github.com/chenglou/pretext) — Cheng Lou's JS library for measuring and laying out multiline text without DOM manipulation. Developed by training models against real browser rendering (Safari, Chrome, Firefox) for weeks until output matched exactly — a case study in AI-friendly iteration with pixel-perfect ground truth. [Demos](https://chenglou.me/pretext/) `tags: ai-assisted, browser, text-layout, iteration, ground-truth`

---

## Articles & Blog Posts

*Key readings on the state and future of AI-assisted development.*

- [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) — Anthropic engineering post on multi-agent harness patterns: GAN-inspired generator/evaluator architecture, context management, and when complexity pays off. `tags: harness-design, multi-agent, anthropic, architecture`
- [Harness Engineering: Leveraging Codex in an Agent-First World](https://openai.com/index/harness-engineering/) — OpenAI's philosophy of the repo as the agent's knowledge store: push docs, plans, and decisions into version control so agents can operate without external context. `tags: harness-design, openai, codex, architecture, agents-md`
- [Introducing Advanced Tool Use](https://www.anthropic.com/engineering/advanced-tool-use) — Three new API features: Tool Search Tool (on-demand discovery), Programmatic Tool Calling (Python orchestration), and Tool Use Examples. Dramatic token and accuracy improvements. `tags: harness-design, anthropic, tools, mcp, api`
- [The Emerging "Harness Engineering" Playbook](https://www.ignorance.ai/p/the-emerging-harness-engineering) — Charlie Guo's overview of best practices for building structured environments, tools, and documentation that enable AI coding agents to work effectively at scale. `tags: harness-design, best-practices, overview, agents`
- [Claude Code Auto Mode](https://www.anthropic.com/engineering/claude-code-auto-mode) — How Anthropic built classifiers to automate permission decisions: two-layer architecture (input probe + transcript classifier), 93% approval rate problem, what it catches and misses. `tags: harness-design, safety, anthropic, permissions, auto-mode`

---

## Videos & Talks

*Presentations, demos, and tutorials.*

---

## Benchmarks & Evaluation

*How models and harnesses are measured.*

---

## Contributing

To add a resource, submit a PR adding an entry under the appropriate section using this format:

```markdown
- [Resource Name](https://url) — One-line description. `tags: relevant, tags`
```

For ratings and feedback, see the rating system *(coming soon)*.
