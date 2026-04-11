# AI-Assisted Software Development

Companion materials for a survey talk on AI-assisted software development, covering harnesses and frontier models, common approaches, and extraordinary examples of AI-accelerated coding.

[A catalog of resources](resources/README.md), similar to Awesome lists, is available and free to be updated.

## Repository Layout

```
├── presentation/       Slidev-based slide deck (Markdown + Mermaid diagrams)
│   ├── slides.md       Main presentation source
│   ├── images/         Slide images and figures
│   ├── docs/           Reference documents
│   └── pixi.toml       Environment config (run via pixi)
│
└── resources/          Curated link collection
    └── README.md       Awesome-style resource list organized by topic
```

## Running the Presentation

The slide deck uses [Slidev](https://sli.dev) and is managed with [pixi](https://pixi.sh):

```bash
cd presentation
pixi install
pixi run npx slidev slides.md
```

## Talk Abstract

A survey talk discussing the growing use of AI-assisted software development including (1) an overview of harnesses and frontier models like Claude, Codex, and Gemini, (2) some common approaches and issues with their use, and (3) extraordinary examples of how people have used AI-accelerated coding.
