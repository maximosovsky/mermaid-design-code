---
title: "From Chaos to Consistency: I Built a Design Code for Mermaid Diagrams"
published: false
description: "Mermaid defaults are ugly, dark mode breaks everything, and every diagram looks different. Here's the design system I built to fix all three."
tags: mermaid, javascript, design, opensource
cover_image: https://raw.githubusercontent.com/maximosovsky/mermaid-design-code/main/cover.jpg
---

Every developer loves Mermaid. Write some text, get a diagram. No Figma, no drag-and-drop, no exporting PNGs.

Until you look at the result.

The default theme has poor contrast. Dark mode inverts your carefully chosen colors into unreadable chaos. Every diagram in your docs looks different because there's no shared palette, no naming convention, no standard.

I manage 50+ repositories. Every project has at least one architecture diagram. After the fifteenth time I copy-pasted theme variables and forgot which shade of blue meant "authentication" vs "deployment," I snapped.

I built a design code for Mermaid diagrams.

## The 5 Problems Nobody Solves

Search "Mermaid styling" on StackOverflow and you'll find hundreds of frustrated developers hitting the same walls:

| Problem | What Happens |
|---------|-------------|
| 🎨 **Ugly defaults** | The default theme uses harsh colors with poor contrast. Diagrams look like 2005 PowerPoint slides |
| 🌙 **Dark mode breaks everything** | Hardcoded `themeVariables` look fine in light mode but become unreadable on dark backgrounds |
| 🔀 **No consistency** | Every diagram uses different colors. Blue means "API" in one diagram and "database" in another |
| 📐 **Subgraph styling is painful** | Applying `classDef` to subgraphs doesn't work the same way as nodes. Users hack around it with `style` directives |
| 🔍 **Complex diagrams are unusable** | 50+ nodes? Good luck reading anything without zoom and pan |

These aren't edge cases. These are the everyday experience of using [Mermaid](https://mermaid.js.org/) for real documentation.

## What a "Design Code" Actually Is

A design code is not a library. It's not an npm package. You don't install it.

It's a set of rules:
- **9 pastel `classDef` tokens** — each color means one thing across all diagrams
- **Dark/light theme** with `themeVariables` for both modes
- **Typography** — Sora 700 for headings, Lato 400/700 for body
- **Zoom & pan** — vanilla JS, no dependencies
- **File naming** — `<name>-<YYYY-MM-DD>.html` + paired `-description.md`
- **Pre-save checklist** — 9 points to verify before committing

Think of it as what a brand guide does for logos and fonts, but for Mermaid diagrams.

## The Pastel Palette

The default Mermaid colors are either too saturated or too similar. I settled on a pastel palette where every category gets a unique `fill` + `stroke` combination:

```
classDef clrAuth    fill:#eff6ff, stroke:#3b82f6   → blue
classDef clrUI      fill:#f5f3ff, stroke:#8b5cf6   → purple
classDef clrLayout  fill:#f0fdfa, stroke:#14b8a6   → teal
classDef clrDeploy  fill:#eff6ff, stroke:#3b82f6   → blue (bold)
classDef clrService fill:#fff,    stroke:#999       → gray dashed
classDef clrAPI     fill:#ecfeff, stroke:#06b6d4   → cyan
classDef clrRepo    fill:#f8fafc, stroke:#94a3b8   → slate
classDef clrDistrib fill:#fdf2f8, stroke:#ec4899   → pink
classDef codeBox    fill:#6366f1, stroke:#818cf8   → indigo (inverted)
```

**Rule:** light pastel fill + colored stroke + `color:#000`. Always. Every node.

Outer subgraphs use warm yellow (`fill:#fffbeb, stroke:#f59e0b`) to create visual hierarchy: yellow containers → gray subblocks → pastel nodes.

## Dark Mode That Actually Works

The biggest pain point I found on StackOverflow: "My diagram looks fine in light mode but is unreadable in dark mode."

The fix is simple but nobody does it: **specify `themeVariables` for BOTH modes.**

```javascript
mermaid.initialize({
    theme: isDark ? 'dark' : 'default',
    themeVariables: isDark ? {
        primaryColor: '#1a1a2e',
        clusterBkg: '#1a1a2e',
        clusterBorder: '#2a2a40',
        lineColor: '#888'
    } : {
        primaryColor: '#ffffff',
        clusterBkg: '#fafafa',
        clusterBorder: '#e2e4ef',
        lineColor: '#aaa',
        nodeTextColor: '#000'
    }
});
```

Theme toggle uses [moon.svg / sun.svg](https://github.com/maximosovsky/site-design/tree/master/icons) icons with `localStorage` persistence. Click once — it remembers.

## Zoom & Pan (Zero Dependencies)

A 50-node diagram is useless if you can't zoom in. Mermaid doesn't include zoom. Most solutions pull in D3.js or panzoom libraries.

My approach: ~40 lines of vanilla JS.

- **Scroll** = zoom (wheel event with `preventDefault`)
- **Drag** = pan (mousedown/mousemove/mouseup)
- **Buttons:** `−`, `%`, `+`, `⊡` (fit to screen)
- **Scale formula:** `Math.round((scale / baseScale) * 100) + '%'`

No dependencies. No build step. Just works.

## The Paired File Convention

Every diagram is actually two files:

```
project-flow-2026-03-11.html          ← interactive diagram
project-flow-2026-03-11-description.md ← text walkthrough
```

Why? Because a diagram shows structure, but it doesn't explain decisions. The description file answers: *Why is Auth connected to Services? What does the dotted line from SEO to GA4 mean?*

The date in the filename creates a natural timeline. You can see how a project's architecture evolved over months.

## The Pre-Save Checklist

Before committing a diagram, I run through 9 checks:

1. All `==>` replaced with `-->` (thick arrows are banned — too heavy)
2. No orphan nodes (every ID in a subgraph or connection)
3. Emoji via HTML entities (`&#x1F680;`), not Unicode
4. `direction` specified in every subgraph
5. `classDef` assigned to every node
6. Dark/light theme works
7. Zoom/pan works
8. Fit button fits diagram to screen
9. Creation date present

These sound obvious. They're not, until you forget one and spend 20 minutes debugging why a node is invisible in dark mode.

## How My Design Code Solves Each Problem

| Problem | Design Code Solution |
|---------|---------------------|
| Ugly defaults | 9 pastel `classDef` tokens with deliberate contrast |
| Dark mode breaks | Dual `themeVariables` — light AND dark specified |
| No consistency | Shared palette + naming convention + checklist |
| Subgraph styling | Yellow outer → gray inner hierarchy via `style` directive |
| Complex diagrams | Built-in zoom/pan in vanilla JS |

## Try It

**Live example:** [Project Lifecycle Pipeline](https://maximosovsky.github.io/mermaid-design-code/examples/project-flow-2026-03-11.html) — a real 50+ node diagram with zoom/pan, dark/light theme, legend, and pastel palette.

**Repository:** [github.com/maximosovsky/mermaid-design-code](https://github.com/maximosovsky/mermaid-design-code)

The repo includes the full [mermaid-guidelines.md](https://github.com/maximosovsky/mermaid-design-code/blob/main/mermaid-guidelines.md) with every rule, token, and code snippet you need to replicate this in your own projects.

---

*Do your Mermaid diagrams all look the same — or does each one have its own personality? What's your approach to diagram consistency? Drop a comment.*

---

*Building in public, one repo at a time. Follow the journey: [LinkedIn](https://www.linkedin.com/in/osovsky/) · [GitHub](https://github.com/maximosovsky)*
