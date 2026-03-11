<div align="center">

# 📐 Mermaid Design Code

![Mermaid](https://img.shields.io/badge/Mermaid-FF3670?style=for-the-badge&logo=mermaid&logoColor=white)
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

**Design code standard for interactive Mermaid diagrams in HTML**

[Guidelines](mermaid-guidelines.md) · [Example Diagram](project-flow-2026-03-11.html) · [Example Description](project-flow-2026-03-11-description.md)

</div>

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
├── project-flow-2026-03-11.html          # example: project lifecycle pipeline
├── project-flow-2026-03-11-description.md # example: text description
├── README.md
├── LICENSE
└── .gitignore
```

---

## 📐 Guidelines Summary

### Arrows
| Type | Syntax | When |
|------|--------|------|
| Regular | `A --> B` | Main flow |
| Dotted | `A -.- B` | Dependency without flow |
| Dotted with text | `A -. "text" .-> B` | Annotated dependency |
| **Never** | `A ==> B` | ❌ Too thick/heavy |

### Node Colors (classDef)
```mermaid
classDef clrAuth    fill:#eff6ff,stroke:#3b82f6,color:#000
classDef clrDeploy  fill:#eff6ff,stroke:#3b82f6,color:#000
classDef clrService fill:#fff,stroke:#999,color:#000,stroke-dasharray:5 5
classDef clrAPI     fill:#ecfeff,stroke:#06b6d4,color:#000
classDef codeBox    fill:#6366f1,stroke:#818cf8,stroke-width:3px,color:#fff
```

### Outer Subgraphs
```mermaid
style FRONTEND fill:#fffbeb,stroke:#f59e0b,stroke-width:2px,color:#000
```

Full reference: [mermaid-guidelines.md](mermaid-guidelines.md)

---

## 🗺️ Roadmap

- [x] Mermaid guidelines document
- [x] Example diagram (project-flow)
- [x] Example description
- [ ] More example diagrams
- [ ] Diagram template generator

---

## 🤝 Contributing

Fork → `feature/name` → PR

---

## 📄 License

MIT © [Max Osovsky](https://www.linkedin.com/in/osovsky/)
