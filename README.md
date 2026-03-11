# 📐 Mermaid Design Code

[![Live Example](https://img.shields.io/badge/example-GitHub_Pages-81D8D0?style=for-the-badge)](https://maximosovsky.github.io/mermaid-design-code/examples/project-flow-2026-03-11.html)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

**Create beautiful, consistent Mermaid diagrams in HTML**

> A design code is not a library or a tool. It's a set of rules, tokens, and examples that ensure every Mermaid diagram looks and behaves the same way.

[Quick Start](#-quick-start) · [Features](#-features) · [Tech Stack](#%EF%B8%8F-tech-stack) · [Examples](#-examples) · [Guidelines](mermaid-guidelines.md)

---

## 💡 Concept

Mermaid Design Code defines a single standard for interactive Mermaid diagrams: pastel color palette with classDef tokens, dark/light theme with localStorage persistence, zoom/pan controls, and paired description files. Every diagram is a pair — an `.html` with interactive controls and a `-description.md` with a text walkthrough.

---

## ✨ Features

| Feature | Details |
|---------|---------|
| 🎨 **Pastel Palette** | Light fill + colored stroke + `color:#000` for all nodes |
| 🌙 **Dark/Light Theme** | Toggle with `localStorage` persistence, moon/sun SVG icons |
| 🔍 **Zoom & Pan** | Mouse wheel zoom, drag pan, fit-to-view button |
| 📐 **Visual Hierarchy** | Yellow containers → gray subblocks → pastel nodes |
| 📝 **Paired Files** | Every `.html` diagram has a `-description.md` walkthrough |
| 🔤 **Typography** | Sora 700 (headings) + Lato 400/700 (body) via Google Fonts |
| ✅ **Pre-save Checklist** | No orphan nodes, no `==>`, emoji as HTML entities |

---

## 🚀 Quick Start

1. Read [mermaid-guidelines.md](mermaid-guidelines.md)
2. Create a pair of files:
   ```
   <name>-<YYYY-MM-DD>.html          # interactive diagram
   <name>-<YYYY-MM-DD>-description.md # text walkthrough
   ```
3. Use the pastel `classDef` palette from the guidelines
4. Run the pre-save checklist before committing

<details>
<summary>📋 Pre-save Checklist</summary>

- [ ] All `==>` replaced with `-->`
- [ ] No orphan nodes (every ID in a subgraph or connection)
- [ ] Emoji via HTML entities, not Unicode
- [ ] `direction` specified in every subgraph
- [ ] classDef assigned to every node
- [ ] Dark/light theme works
- [ ] Zoom/pan works
- [ ] Fit button fits diagram to screen
- [ ] Creation date present

</details>

<details>
<summary>🎨 Color Palette</summary>

```mermaid
classDef clrAuth    fill:#eff6ff,stroke:#3b82f6,color:#000
classDef clrUI      fill:#f5f3ff,stroke:#8b5cf6,color:#000
classDef clrLayout  fill:#f0fdfa,stroke:#14b8a6,color:#000
classDef clrDeploy  fill:#eff6ff,stroke:#3b82f6,color:#000
classDef clrService fill:#fff,stroke:#999,color:#000,stroke-dasharray:5 5
classDef clrAPI     fill:#ecfeff,stroke:#06b6d4,color:#000
classDef clrRepo    fill:#f8fafc,stroke:#94a3b8,color:#000
classDef clrDistrib fill:#fdf2f8,stroke:#ec4899,color:#000
classDef codeBox    fill:#6366f1,stroke:#818cf8,stroke-width:3px,color:#fff
```

**Outer subgraphs** (yellow containers):
```css
fill:#fffbeb, stroke:#f59e0b, stroke-width:2px, color:#000
```

</details>

---

## 🏗️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Diagrams | [Mermaid v11](https://mermaid.js.org/) (CDN ESM) |
| Fonts | [Google Fonts](https://fonts.google.com/): Sora, Lato |
| Theme | CSS Variables + `data-theme` attribute |
| Icons | [site-design/icons/](https://github.com/maximosovsky/site-design/tree/master/icons) (moon.svg, sun.svg) |
| Zoom | Vanilla JS (wheel + drag) |

<details>
<summary>📁 Project Structure</summary>

```
mermaid-design-code/
├── mermaid-guidelines.md              # design code standard
├── examples/
│   ├── project-flow-2026-03-11.html   # example diagram
│   └── project-flow-2026-03-11-description.md
├── llms.txt
├── llms-full.txt
├── README.md
├── LICENSE
└── .gitignore
```

</details>

---

## 🗺️ Roadmap

- [x] Mermaid guidelines document
- [x] Example diagram (project lifecycle pipeline)
- [x] Example description
- [x] LLM-ready docs
- [x] GitHub Pages for live example
- [ ] More example diagrams
- [ ] Diagram template generator

---

## 📂 Examples

| Diagram | Description |
|---------|-------------|
| [project-flow-2026-03-11.html](examples/project-flow-2026-03-11.html) | Project lifecycle pipeline ([live](https://maximosovsky.github.io/mermaid-design-code/examples/project-flow-2026-03-11.html)) |
| [project-flow-2026-03-11-description.md](examples/project-flow-2026-03-11-description.md) | Text walkthrough |

---

## 🤝 Contributing

Fork → `feature/name` → PR

---

## 📄 License

[Maxim Osovsky](https://www.linkedin.com/in/osovsky/). Licensed under [MIT](LICENSE).
