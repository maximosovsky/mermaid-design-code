# Mermaid Diagram Guidelines

> Standard for creating Mermaid diagrams in HTML.

## File Structure

Every diagram is a **pair of files**: an interactive HTML and a text description in Markdown.

**Naming convention:** filename must include the creation date in `YYYY-MM-DD` format.

```
mermaid-design-code/
├── mermaid-guidelines.md                  # design code standard (this file)
├── examples/
│   ├── project-flow-2026-03-11.html      # example diagram
│   └── project-flow-2026-03-11-description.md
```

- **`<name>-<YYYY-MM-DD>.html`** — the interactive Mermaid diagram with zoom/pan, theme toggle, legend
- **`<name>-<YYYY-MM-DD>-description.md`** — plain-text walkthrough explaining what each block means, the full flow, and a one-line pipeline summary

## Required Elements

### 1. HTML Wrapper
- **Creation date** — always include in `<title>` or toolbar, format: `YYYY-MM-DD`
- Fonts: `Sora 700` (headings) + `Lato 400/700` (body) — via Google Fonts
- CSS Variables for dark/light theme (`:root` and `[data-theme="light"]`)
- `<pre class="mermaid">` — diagram container
- Mermaid v11 via CDN ESM: `https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs`

### 2. Theme (dark/light)
- Default: light mode
- Icons: `moon.svg` / `sun.svg` from `../site-design/icons/`
- CSS filters for icon visibility:
  ```css
  .icon-moon { filter: brightness(0) saturate(100%) invert(84%) sepia(60%) saturate(600%) hue-rotate(5deg) brightness(105%); }
  .icon-sun  { filter: brightness(0) saturate(100%) invert(75%) sepia(90%) saturate(500%) hue-rotate(360deg) brightness(105%); }
  ```
- Persist selection in `localStorage`

### 3. Legend (color dots)
Every diagram **must** have a legend in the toolbar. Dot colors match `classDef` strokes.

```html
<div class="legend">
    <span><i class="dot auth"></i> Auth</span>
    <span><i class="dot deploy"></i> Deploy</span>
    ...
</div>
```

```css
.legend { display: flex; gap: 10px; font-size: 11px; flex-wrap: wrap; }
.legend span { display: flex; align-items: center; gap: 4px; }
.legend .dot { width: 10px; height: 10px; border-radius: 50%; }
.dot.auth    { background: #3b82f6; }     /* classDef clrAuth    stroke */
.dot.deploy  { background: #22c55e; }     /* classDef clrDeploy  stroke */
.dot.service { background: #999; }        /* classDef clrService stroke */
.dot.api     { background: #06b6d4; }     /* classDef clrAPI     stroke */
.dot.repo    { background: #94a3b8; }     /* classDef clrRepo    stroke */
.dot.distrib { background: #ec4899; }     /* classDef clrDistrib stroke */
```

**Rule:** dot color = `stroke` value from the corresponding `classDef`.

### 4. Zoom + Pan + Scale
- Scroll = zoom (wheel event with `preventDefault`)
- Drag = pan (mousedown/mousemove/mouseup)
- Buttons: `−`, `%`, `+`, `⊡` (fit)

**Default scale:**
- Set via `baseScale` — the `scale` value at which the label shows **100%**
- Example: if `baseScale = 5.1`, then `scale = 5.1` displays "100%", `scale = 10.2` displays "200%"
- Display formula: `Math.round((scale / baseScale) * 100) + '%'`

```javascript
var baseScale = 5.1;  // tune per diagram

function initZoom() {
    scale = baseScale;  // starting scale = 100%
    panX = 20;
    panY = 20;
    applyTransform();
}

setTimeout(initZoom, 500);   // after first render
setTimeout(initZoom, 1500);  // after full draw
```

**Scale selection rule:**
> Default scale should make **one subgraph block fill ~30% of screen width** with readable node text. This is typically 300–500% of the "fit" scale. `fitToView` is too small — the entire graph is visible but text is unreadable. Start zoomed in — user can zoom out.

**How to find `baseScale`:**
1. Open the diagram, scroll-zoom until one block ≈ 30% of screen width
2. Read the current `%` — divide by 100, that's your `baseScale`
3. The `⊡` (fit) button always fits to screen, regardless of `baseScale`

## Diagram Style

### Graph Type
```mermaid
graph TB    %% Top-to-Bottom — primary
graph LR    %% Left-to-Right — for compact diagrams
```

### Arrows
| Type | Syntax | When |
|------|--------|------|
| Regular | `A --> B` | Main flow |
| Dotted | `A -.- B` | Dependency without flow |
| Dotted with text | `A -. "text" .-> B` | Annotated dependency |
| **Never** | `A ==> B` | ❌ Too thick/heavy |

### Subgraphs
```mermaid
subgraph ID["&#x1F3A8; Title"]
    direction TB   %% or LR
    NODE_A["Text<br/>details"]
end
```
- Emoji via HTML entities: `&#x1F3A8;` (🎨), `&#x1F511;` (🔑), `&#x2699;` (⚙️)
- `direction LR` for horizontal subblocks
- `direction TB` for vertical subblocks
- Max subgraph nesting: 3 levels

### Subgraph Color Hierarchy (outer vs inner)

> **Rule:** outer (root) subgraphs get a warm yellow fill. Inner subgraphs use the standard gray from `clusterBkg`.

```mermaid
%% Outer subgraph styling — warm yellow containers
style FRONTEND fill:#fffbeb,stroke:#f59e0b,stroke-width:2px,color:#000
style BACKEND  fill:#fffbeb,stroke:#f59e0b,stroke-width:2px,color:#000
```

| Level | Fill | Stroke | When |
|-------|------|--------|------|
| Outer subgraph | `#fffbeb` (warm yellow) | `#f59e0b` (amber) | Major sections: Front-end, Back-end, Autoposting |
| Inner subgraph | `clusterBkg` from themeVariables | `clusterBorder` | Auth, UI, Layout, Deploy, etc. |
| Node | pastel `fill` from classDef | colored `stroke` from classDef | Individual elements |

This creates a visual hierarchy: **yellow container → gray subblock → pastel node**.

### Node Styles (classDef) — Pastel Palette

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

**Rule:** light pastel `fill` + colored `stroke` + `color:#000`.
Services use dashed border (`stroke-dasharray:5 5`).

### Mermaid themeVariables

> **IMPORTANT:** always specify themeVariables for BOTH modes. Omitting light mode variables will leave dark subgraph backgrounds.

```javascript
mermaid.initialize({
    theme: isDark ? 'dark' : 'default',
    themeVariables: isDark ? {
        // === DARK MODE ===
        primaryColor: '#1a1a2e', primaryTextColor: '#e0e0e0',
        primaryBorderColor: '#6078ff', lineColor: '#888',
        secondaryColor: '#2a2a40', tertiaryColor: '#0f0f1a',
        clusterBkg: '#1a1a2e', clusterBorder: '#2a2a40',
        edgeLabelBackground: '#1a1a2e'
    } : {
        // === LIGHT MODE ===
        primaryColor: '#ffffff', primaryTextColor: '#000',
        primaryBorderColor: '#d1d5db', lineColor: '#aaa',
        secondaryColor: '#f9fafb', tertiaryColor: '#f3f4f6',
        clusterBkg: '#fafafa', clusterBorder: '#e2e4ef',
        edgeLabelBackground: '#fff',
        nodeBorder: '#d1d5db', mainBkg: '#ffffff',
        nodeTextColor: '#000', clusterTextColor: '#000'
    },
    flowchart: {
        curve: 'basis',    // smooth curves
        padding: 14,
        nodeSpacing: 30,
        rankSpacing: 55
    },
    fontSize: 11,
    fontFamily: 'Lato, sans-serif'
});
```

**Key light mode variables:**
| Variable | Value | Purpose |
|----------|-------|---------|
| `clusterBkg` | `#fafafa` | Subgraph background — light gray |
| `clusterBorder` | `#e2e4ef` | Subgraph border — pastel |
| `primaryTextColor` | `#000` | Black text |
| `nodeTextColor` | `#000` | Black text inside nodes |
| `mainBkg` | `#ffffff` | White node background |
| `lineColor` | `#aaa` | Soft gray arrows |

### Links Inside Nodes
```mermaid
NODE["Text<br/><a href='https://url'>label</a>"]
NODE["Text<br/><a href='file:///C:/path'>local file</a>"]
```

## Pre-save Checklist

- [ ] All `==>` replaced with `-->`
- [ ] No orphan nodes (every ID used in a subgraph or connection)
- [ ] Emoji via HTML entities, not Unicode
- [ ] `direction` specified in every subgraph
- [ ] classDef assigned to every node
- [ ] Dark/light theme works
- [ ] Zoom/pan works
- [ ] Fit button fits diagram to screen
- [ ] Creation date present

## Example Files

- [project-flow-2026-03-11.html](file:///C:/100star/mermaid-design-code/examples/project-flow-2026-03-11.html) — full pipeline diagram
- [project-flow-2026-03-11-description.md](file:///C:/100star/mermaid-design-code/examples/project-flow-2026-03-11-description.md) — text description of the flow
