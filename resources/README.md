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
  - [Claude (Anthropic)](#claude-anthropic)
  - [OpenAI Codex](#openai-codex)
  - [Google Gemini](#google-gemini)
- [Approaches: Providing Large Codebase Context](#approaches-providing-large-codebase-context)
  - [Hierarchical Maps (llms.txt / CLAUDE.md)](#hierarchical-maps-llmstxt--claudemd)
  - [RAG & Knowledge Graphs](#rag--knowledge-graphs)
  - [Context Engineering (General)](#context-engineering-general)
- [Extraordinary Examples](#extraordinary-examples)
- [Articles & Blog Posts](#articles--blog-posts)
- [Videos & Talks](#videos--talks)
- [Benchmarks & Evaluation](#benchmarks--evaluation)

---

## Harnesses & Tools

### IDE-Integrated

*AI assistants that work within your editor.*

- [GitHub Copilot](https://github.com/features/copilot) — AI pair programmer integrated into VS Code, JetBrains, and other editors. <!-- tags: ide, autocomplete, github -->
- [Cursor](https://www.cursor.com/) — AI-native code editor built on VS Code with deep model integration. <!-- tags: ide, editor, agentic -->
- [Windsurf](https://windsurf.com/) — AI-powered IDE (formerly Codeium) with agentic "Cascade" flows. <!-- tags: ide, editor, agentic -->
- [Cline](https://github.com/cline/cline) — Open-source autonomous coding agent as a VS Code extension. <!-- tags: ide, open-source, agentic -->

### Terminal / Agent-Based

*CLI tools where you give the AI a task and it works autonomously.*

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — Anthropic's CLI agent for agentic coding with Claude. File editing, shell access, Git integration. <!-- tags: cli, agentic, anthropic, claude -->
- [Codex CLI](https://github.com/openai/codex) — OpenAI's open-source terminal coding agent built in Rust. <!-- tags: cli, agentic, openai, codex, open-source -->
- [Codex (Cloud)](https://openai.com/codex/) — OpenAI's cloud-based async coding agent with sandboxed environments. <!-- tags: cloud-agents, openai, codex -->
- [Gemini CLI](https://github.com/google-gemini/gemini-cli) — Google's open-source terminal agent with Gemini 2.5 Pro. Free tier: 1K requests/day. <!-- tags: cli, agentic, google, gemini, open-source, free -->
- [Aider](https://aider.chat/) — Open-source AI pair programming in the terminal. Works with multiple models. <!-- tags: cli, open-source, multi-model -->
- [Pi](https://pi.dev/) — Minimal, extensible terminal coding agent by Mario Zechner. Works with 15+ AI providers, customizable via TypeScript extensions and skills. <!-- tags: cli, agentic, open-source, multi-model, extensible -->
- [Amp](https://ampcode.com/) — Coding agent by Sourcegraph. CLI-based, pay-as-you-go with frontier models. <!-- tags: cli, agentic, sourcegraph, multi-model -->

### Skills & Extensions

*Shareable skill libraries and configuration packs that extend agent capabilities.*

- [gstack](https://github.com/garrytan/gstack) — Garry Tan's (YC CEO) open-source skill library: 23 slash-command skills encoding a full sprint process (office hours, CEO/eng/design review, QA, ship, security audits). Built on the SKILL.md standard — works across Codex CLI, Claude Code, Gemini CLI, Cursor, Factory Droid. 62K+ stars. <!-- tags: skills, process, open-source, multi-agent -->
- [GitHub Spec Kit](https://github.com/speckit) — Open-source templates for spec-driven development across Copilot, Claude Code, Gemini CLI, Cursor, Windsurf. <!-- tags: specs, templates, open-source, multi-agent -->
- [Impeccable](https://impeccable.style/) — Open-source design skills package by Paul Bakaus. 21 commands to steer AI-generated UIs toward better design while detecting anti-patterns like purple gradients and nested cards. <!-- tags: skills, design, ui, open-source -->

### Cloud / Autonomous Agents

*Systems designed to work with minimal user interaction beyond specs or task descriptions.*

- [Copilot cloud agent](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent) — GitHub's autonomous cloud coding agent. Spins up ephemeral GitHub Actions environments, researches the codebase with RAG via GitHub code search, writes code, runs tests, and pushes to a branch. Assignable via issues or Copilot Chat. <!-- tags: cloud-agents, github, multi-model -->
- [Devin](https://devin.ai/) — AI software engineering agent by Cognition with web-based IDE for monitoring. Assigns tickets, writes code, opens PRs. <!-- tags: cloud-agents, ide -->
- [OpenHands](https://github.com/All-Hands-AI/OpenHands) — Open-source platform for AI software agents. <!-- tags: agent, open-source -->
- [mini-SWE-agent](https://github.com/SWE-agent/mini-swe-agent) — 100-line Python agent that solves GitHub issues. Successor to SWE-agent, scores >74% on SWE-bench verified. By Princeton/Stanford. <!-- tags: agent, research, open-source, lightweight -->
- [Claude Code /autoplan](https://code.claude.com/docs/en/ultraplan) — Cloud planning agent that clones your local repo to an Anthropic-managed VM and produces an editable plan viewable via web page. 90-minute timeout; plans may need manual recovery if it expires. <!-- tags: cloud-agents, anthropic, claude, planning, claude-code -->
- [Jules](https://jules.google/) — Google Labs cloud coding agent with tight GitHub integration. Assigns tasks, writes code, opens PRs. [GitHub Action](https://github.com/google-labs-code/jules-action) <!-- tags: cloud-agents, google, gemini, github -->

### Spec-Driven Development

*Tools that emphasize specifications as the source of truth for AI-generated code.*

- [GitHub Spec Kit](https://github.com/github/spec-kit) — Open-source toolkit for spec-driven development. Templates for Copilot, Claude Code, Gemini CLI, Cursor, Windsurf. Specs become contracts that agents code against. <!-- tags: spec-driven, open-source, github, workflow -->
- [Kiro](https://kiro.dev/) — Amazon/AWS AI-powered IDE built around spec-driven development. Translates natural language into requirements (EARS notation), generates implementation plans, validates against specs. <!-- tags: spec-driven, ide, aws, amazon -->

### AI-Powered Design & Prototyping

*AI tools for UI design, prototyping, and full-stack app generation.*

- [Google Stitch](https://stitch.withgoogle.com/) — AI-native UI design canvas from Google Labs. Voice-driven "vibe design," generates HTML/CSS/Tailwind, exports to Figma. Free. <!-- tags: design, ui, google, gemini, free -->
- [Antigravity](https://aistudio.google.com/) — Full-stack coding agent in Google AI Studio. Turns text prompts into production-ready web apps with persistent data, auth, and external services. <!-- tags: full-stack, google, gemini, cloud -->
- [Firebase Studio](https://firebase.studio/) — Google's app prototyping agent. Natural language, mockups, or screenshots to working apps using popular framework templates. <!-- tags: prototyping, google, gemini, cloud -->

### Sandboxing & Containment

*Tools for isolating and constraining AI agents to prevent unintended system changes.*

- [jai](https://jai.scs.stanford.edu/) — Lightweight Linux sandbox for AI agents from Stanford SCS. Contains agents to a working directory with copy-on-write overlays — no Docker required. <!-- tags: sandbox, security, open-source, containment, stanford -->

---

## Frontier Models

*The large language models powering AI-assisted development, with model-specific resources.*

### Claude (Anthropic)

*Opus 4.6, Sonnet 4.6, Haiku 4.5. 200K context. Strong code quality and instruction following.* — [claude.ai](https://www.anthropic.com/claude)

#### Articles & Blog Posts

- [Best Practices for Claude Code](https://code.claude.com/docs/en/best-practices) — Comprehensive guide from Anthropic: explore-plan-code-verify workflow, CLAUDE.md best practices, context management, subagents, common failure patterns. <!-- tags: best-practices, anthropic, claude-code, workflow -->
- [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) — Anthropic engineering post on multi-agent harness patterns: GAN-inspired generator/evaluator architecture, context management, and when complexity pays off. <!-- tags: harness-design, multi-agent, anthropic, architecture -->
- [Introducing Advanced Tool Use](https://www.anthropic.com/engineering/advanced-tool-use) — Three new API features: Tool Search Tool (on-demand discovery), Programmatic Tool Calling (Python orchestration), and Tool Use Examples. Dramatic token and accuracy improvements. <!-- tags: harness-design, anthropic, tools, mcp, api -->
- [Claude Code Auto Mode](https://www.anthropic.com/engineering/claude-code-auto-mode) — How Anthropic built classifiers to automate permission decisions: two-layer architecture (input probe + transcript classifier), 93% approval rate problem, what it catches and misses. <!-- tags: harness-design, safety, anthropic, permissions, auto-mode -->

#### Repos & Resources

- [awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) — Curated directory of Claude Skills, tools, and resources. Skills use a progressive disclosure architecture (metadata scan → full instructions → bundled resources) for token efficiency. <!-- tags: skills, claude, curated-list, community -->

### OpenAI Codex

*GPT-5.4. 1M context (Codex). Broad ecosystem.* — [openai.com](https://openai.com/)

#### Articles & Blog Posts

- [How OpenAI Uses Codex](https://cdn.openai.com/pdf/6a2631dc-783e-479b-b1a4-af0cfbd38630/how-openai-uses-codex.pdf) — OpenAI's internal use cases and best practices from their own engineering teams: code understanding, refactoring, performance optimization, testing, staying in flow. <!-- tags: best-practices, openai, codex, use-cases -->
- [Harness Engineering: Leveraging Codex in an Agent-First World](https://openai.com/index/harness-engineering/) — OpenAI's philosophy of the repo as the agent's knowledge store: push docs, plans, and decisions into version control so agents can operate without external context. <!-- tags: harness-design, openai, codex, architecture, agents-md -->

#### Repos & Resources

- [codex-cli-best-practice](https://github.com/shanraisshan/codex-cli-best-practice) — Comprehensive community guide with 47 tips for OpenAI Codex CLI: subagents, skills, workflows, and orchestration patterns. <!-- tags: best-practices, codex, tips, community, open-source -->

### Google Gemini

*Gemini 3.1 Pro. 1M token context window. Free CLI access.* — [ai.google.dev](https://ai.google.dev/)

#### Repos & Resources

- [Gemma](https://ai.google.dev/gemma/docs) — Google's open-weight model family (Gemma 4). Lightweight enough for local fine-tuning, 140+ languages, up to 256K context. Built on Gemini research. <!-- tags: open-weights, local, fine-tuning, google, multimodal -->

---

## Approaches: Providing Large Codebase Context

*How to help AI understand codebases too large for any context window.*

### Hierarchical Maps (llms.txt / CLAUDE.md)

*Human-curated indexes at multiple levels of detail that let agents navigate from summaries to specifics.*

- [llms.txt specification](https://llmstxt.org/) — Jeremy Howard's proposal to standardize an `/llms.txt` markdown file on websites, providing LLM-friendly content with brief background, guidance, and links to detailed markdown pages. Adopted by many documentation sites. <!-- tags: standard, maps, context, llm-friendly, jeremy-howard -->
- [Claude Code docs map](https://code.claude.com/docs/en/claude_code_docs_map.md) — Auto-generated hierarchical index of all Claude Code documentation. Claude Code fetches this map first, then drills into specific pages as needed — a working example of the maps pattern at scale. <!-- tags: maps, context, claude-code, anthropic, example -->
- [Simon Willison on Claude Code's docs map](https://simonwillison.net/2025/Oct/24/claude-code-docs-map/) — Analysis of how Claude Code uses a markdown index to answer questions about itself: fetch the map, identify relevant pages, fetch those pages. Notes the pattern matches llms.txt. <!-- tags: maps, context, claude-code, analysis, simon-willison -->
- [Using CLAUDE.md files](https://claude.com/blog/using-claude-md-files) — Anthropic's guide to the hierarchical CLAUDE.md system: global (`~/.claude/CLAUDE.md`), project root (`./CLAUDE.md`), and per-directory files that give Claude immediate orientation in a codebase. <!-- tags: maps, context, claude-code, anthropic, claude-md -->
- [Designing a CLAUDE.md Context System](https://dev.to/syntora/designing-a-claudemd-context-system-how-i-give-ai-full-project-context-without-re-explaining-3p2p) — Practitioner guide to structuring multi-level CLAUDE.md files for full project context without re-explaining anything each session. <!-- tags: maps, context, claude-md, tutorial, community -->
- [Context Engineering for Claude Code](https://thomaslandgraf.substack.com/p/context-engineering-for-claude-code) — Deep dive on organizing codebase knowledge for Claude Code: reference don't inline, keep the hot cache small, make the full knowledge base navigable. <!-- tags: maps, context, claude-code, best-practices -->

### RAG & Knowledge Graphs

*Automated retrieval approaches that index codebases into searchable representations.*

- [GitHub Copilot repository indexing](https://docs.github.com/copilot/concepts/indexing-repositories-for-copilot-chat) — How Copilot indexes repositories for context retrieval: background indexing, semantic code search with RAG powered by GitHub code search. Local indexing caps at 2,500 files. <!-- tags: rag, context, github, copilot, indexing -->
- [Augment Code](https://www.augmentcode.com/) — AI coding assistant built around a "Context Engine" that constructs a live knowledge graph of code relationships via AST analysis, dataflow analysis, and embeddings. Handles 400K+ files across multiple languages. <!-- tags: rag, knowledge-graph, context, augment, enterprise -->
- [Beyond Code Generation — Augment Code](https://www.augmentcode.com/blog/beyond-code-generation-what-if-your-developer-ai-actually-understood-your-codebase) — How Augment's Context Engine combines static analysis, dependency graphs, and commit history to understand code structure rather than just surface similarity. <!-- tags: rag, knowledge-graph, context, augment, architecture -->
- [GitNexus: Code Knowledge Graphs and Graph RAG](https://blog.pebblous.ai/blog/gitnexus-code-knowledge-graph-2026/en/) — Graph RAG approach that preserves code structure as explicit relationships rather than flat vector embeddings, treating code structure itself as queryable data. <!-- tags: knowledge-graph, graph-rag, context, code-structure -->
- [Is RAG Dead? What AI Coding Agents Actually Use](https://www.mindstudio.ai/blog/is-rag-dead-what-ai-agents-use-instead) — Analysis of what tools like Claude Code, Cursor, and Devin actually use for codebase understanding: grep, file trees, AST parsing with Tree-sitter — not vector databases. <!-- tags: rag, context, agents, analysis, comparison -->

### Context Engineering (General)

*Cross-cutting resources on managing context for AI agents working with large codebases.*

- [Context Engineering for AI Agents (LangChain)](https://blog.langchain.com/context-engineering-for-agents/) — LangChain's framework for treating RAG, long-context models, and hierarchical maps as complementary tools selected based on latency, cost, and accuracy constraints. <!-- tags: context-engineering, rag, maps, framework, langchain -->
- [Context Engineering Part 2 (Philipp Schmid)](https://www.philschmid.de/context-engineering-part-2) — Practical patterns for context engineering in agentic systems: hierarchical action spaces, retrieval strategies, and when each approach pays off. <!-- tags: context-engineering, agents, patterns, best-practices -->
- [Beyond RAG: The Rise of Context Engineering](https://towardsdatascience.com/beyond-rag/) — Overview of how context engineering and semantic layers are emerging alongside (not replacing) RAG for agentic AI, with analysis of tradeoffs between approaches. <!-- tags: context-engineering, rag, semantic-layers, analysis -->

---

## Extraordinary Examples

*Remarkable demonstrations of what's possible with AI-assisted development.*

- [Pretext](https://github.com/chenglou/pretext) — Cheng Lou's JS library for measuring and laying out multiline text without DOM manipulation. Developed by training models against real browser rendering (Safari, Chrome, Firefox) for weeks until output matched exactly — a case study in AI-friendly iteration with pixel-perfect ground truth. [Demos](https://chenglou.me/pretext/) <!-- tags: ai-assisted, browser, text-layout, iteration, ground-truth -->
- [vinext](https://blog.cloudflare.com/vinext/) — Cloudflare rebuilt Next.js with AI in one week. Vite-based alternative that builds up to 4x faster, produces 57% smaller bundles, and deploys to Cloudflare Workers. <!-- tags: ai-assisted, cloudflare, vite, nextjs, framework -->
- [rewrites.bio](https://rewrites.bio/) — Seqera Labs' manifesto for AI-assisted rewrites of bioinformatics tools. Principles for exact output matching, validation, and attribution. Example: RustQC on 10 GB BAM runs 63x faster, saving ~1.5M CPU-hours annually. <!-- tags: ai-assisted, bioinformatics, scientific-software, rewrite, validation -->
- [Project Glasswing](https://www.anthropic.com/glasswing) — Anthropic's Claude Mythos Preview found thousands of previously unknown vulnerabilities in major OSes and browsers. 83.1% on CyberGym benchmark. $100M in credits committed with partners including AWS, Apple, Google, Microsoft. <!-- tags: security, vulnerabilities, anthropic, mythos, defensive-ai -->
- [Building a C Compiler with a Team of Parallel Claudes](https://www.anthropic.com/engineering/building-c-compiler) — Anthropic tasked 16 parallel Claude agents to build a full C compiler in Rust from scratch in 2 weeks wall-clock time (~$20K cost). The 100K-line compiler can compile the Linux kernel with a 99% pass rate on most test suites. <!-- tags: ai-assisted, compiler, multi-agent, anthropic, autonomous -->

---

## Articles & Blog Posts

*Key readings on the state and future of AI-assisted development (model-agnostic).*

- [The Third Era of AI Software Development](https://cursor.com/blog/third-era) — Cursor's Michael Truell on the shift from interactive AI coding to autonomous cloud agents handling larger tasks independently over extended periods. <!-- tags: vision, cursor, autonomous-agents, cloud -->
- [The Emerging "Harness Engineering" Playbook](https://www.ignorance.ai/p/the-emerging-harness-engineering) — Charlie Guo's overview of best practices for building structured environments, tools, and documentation that enable AI coding agents to work effectively at scale. <!-- tags: harness-design, best-practices, overview, agents -->

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
- [Resource Name](https://url) — One-line description. <!-- tags: relevant, tags -->
```

For ratings and feedback, see the rating system *(coming soon)*.
