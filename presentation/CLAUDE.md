# Slidev Presentation

## Setup

This is a Slidev project. The owner prefers **pixi** for environment management.

### First-time setup:
```bash
pixi init
pixi add nodejs
pixi run npm install
```

### If node_modules already exist but slidev fails with rollup errors:
```bash
rm -rf node_modules package-lock.json
pixi run npm install
# or just: npm install
```

### Run dev server:
```bash
pixi run npx slidev
# or just: npx slidev
```

### Export:
```bash
pixi run npx slidev export          # PDF
pixi run npx slidev export --format pptx  # PowerPoint
```

## Slide Authoring

- All slides are in `slides.md`
- Slides are separated by `---`
- Front matter at the top configures theme, transitions, etc.
- Mermaid diagrams: use ` ```mermaid ` fenced code blocks
- Videos: use `<video src="./assets/filename.mp4" controls></video>`
- Images: use standard markdown `![alt](./assets/filename.png)` or HTML `<img>` tags
- Assets go in `presentation/assets/` (create if needed)

## Slidev Markdown Conventions

```markdown
---
layout: section
---
# Section Title       <!-- section divider slide -->

---
layout: center
---
# Centered Content    <!-- centered layout -->

---
# Normal Slide        <!-- default layout with title + content -->

Content with **markdown**, lists, code blocks, etc.
```
