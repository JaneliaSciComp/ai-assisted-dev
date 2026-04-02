# AI-Assisted Software Development — Janelia Talk & Resources

## Project Overview

This repo contains two things for a talk at Janelia Research Campus (Scientific Software group):

1. `presentation/` — A **Slidev** markdown-based slide deck
2. `resources/` — An **Awesome-style** curated resource list (single README.md)

## Presentation (Slidev)

- The slides live in `presentation/slides.md` — this is the single source of truth
- Slidev renders markdown into a web-based presentation with hot reload
- Supports Mermaid diagrams in fenced code blocks, `<video>` tags for MP4/GIF, and Vue components
- Run with: `npx slidev` (from the `presentation/` directory)
- Export: `npx slidev export` for PDF, `npx slidev export --format pptx` for PowerPoint

### Environment Setup

The owner prefers **pixi** for contained environments rather than global npm. To set up:

```bash
cd presentation/
pixi init
pixi add nodejs
pixi run npm install
pixi run npx slidev
```

If there are npm/rollup platform errors (e.g., missing `@rollup/rollup-darwin-arm64`), the fix is:
```bash
rm -rf node_modules package-lock.json
npm install   # or: pixi run npm install
```

This happens when node_modules were created on a different platform (e.g., Linux sandbox vs macOS arm64).

## Resources

- `resources/README.md` is an Awesome-style single markdown file with categorized links
- Sections mirror the talk structure: Harnesses & Tools, Frontier Models, Approaches, Examples, Articles, Videos, Benchmarks
- Format for entries: `- [Name](url) — Description. \`tags: tag1, tag2\``

## Web Research

WebFetch is blocked for many domains (medium.com, venturebeat.com, openai.com, etc.) by the sandbox proxy. When WebFetch fails and the **Claude in Chrome extension** is installed and connected, use Chrome as a fallback — navigate to the URL in a Chrome tab and use `get_page_text` or `read_page` to read the content. If Chrome tools are not available, ask the user to install the extension or read the content manually.

## Talk Abstract

A survey talk discussing the growing use of AI-assisted software development including:
1. An overview of harnesses and frontier models like Claude, Codex, and Gemini
2. Some common approaches to their use
3. Extraordinary examples of how people have used AI-accelerated coding

Target audience: Software engineers from the Scientific Software group, plus researchers from across Janelia.
~25-35 slides.
