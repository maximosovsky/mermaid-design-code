<div align="center">

# 📐 Mermaid Design Code

![Mermaid](https://img.shields.io/badge/Mermaid-FF3670?style=for-the-badge&logo=mermaid&logoColor=white)
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

**Design code standard for interactive Mermaid diagrams in HTML**

[Quick Start](#-quick-start) · [Features](#-features) · [Tech Stack](#️-tech-stack) · [Guidelines](mermaid-guidelines.md) · [Examples](examples/)

</div>

---

> Every Mermaid diagram in the 100star workspace follows one standard: consistent fonts, colors, zoom/pan, dark/light theme, and a paired description file. This repo is that standard.

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

1. Read the [mermaid-guidelines.md](mermaid-guidelines.md)
2. Create a pair of files:
   ```
   <name>-<YYYY-MM-DD>.html          # interactive diagram
   <name>-<YYYY-MM-DD>-description.md # text walkthrough
   ```
3. Follow the pastel `classDef` palette
4. Run the pre-save checklist before committing

<details>
<summary>📋 Pre-save Checklist</summary>

- [ ] All `==>` replaced with `-->`
- [ ] No orphan nodes (every ID used in a subgraph or connection)
- [ ] Emoji via HTML entities, not Unicode
- [ ] `direction` specified in every subgraph
- [ ] classDef assigned to every node
- [ ] Dark/light theme works
- [ ] Zoom/pan works
- [ ] Fit button fits diagram to screen
- [ ] Creation date present

</details>

---

## 🏗️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Diagrams | Mermaid v11 (CDN ESM) |
| Fonts | Google Fonts: Sora, Lato |
| Theme | CSS Variables + `data-theme` attribute |
| Icons | `site-design/icons/` (moon.svg, sun.svg) |
| Zoom | Vanilla JS (wheel + mousedown/mousemove) |

### File Tree

```
mermaid-design-code/
├── mermaid-guidelines.md                  # design code standard
├── examples/
│   ├── project-flow-2026-03-11.html      # example: project lifecycle pipeline
│   └── project-flow-2026-03-11-description.md # example: text description
├── llms.txt                               # LLM short context
├── llms-full.txt                          # LLM full context
├── README.md
├── LICENSE
└── .gitignore
```

---

## 🗺️ Roadmap

- [x] Mermaid guidelines document
- [x] Example diagram (project-flow)
- [x] Example description
- [x] LLM-ready docs (llms.txt + llms-full.txt)
- [ ] More example diagrams
- [ ] Diagram template generator

---

<div align="center">

## 🤝 Contributing

Fork → `feature/name` → PR

---

## 📄 License

MIT — [Max Osovsky](https://www.linkedin.com/in/osovsky/)

</div>
