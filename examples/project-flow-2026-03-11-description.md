# Project Lifecycle Map

> Text description of the diagram [project-flow-2026-03-11.html](project-flow-2026-03-11.html)

---

## Why This Diagram

When you launch any new project (WallPlan, gsclone, merge-video — doesn't matter), it follows the same path. This diagram captures that path so nothing gets forgotten.

## What Each Stage Means

1. **Idea** — a product idea appears in your head

2. **Planning** — before writing code, you create three documents: architecture, visual diagram, and implementation plan. This is your "contract with yourself" — what we're going to build

3. **Terminal** — you run `100star-init.ps1`, which creates the project scaffold. From here, three parallel branches emerge:

4. **Front-end** — everything the user sees: authentication, design (fonts, colors, icons, layout), SEO (so Google can find it)

5. **GitHub Repo** — the project's "storefront": README, license, llms.txt. What a person sees when visiting GitHub

6. **Back-end** — code that works "under the hood": source code → deploy to Vercel/Alibaba → connect services (Cloudflare, Redis) → API (GitHub Actions, GA4, Gemini)

7. **Autoposting Dashboard** — when the project is ready, you publish an article on Dev.to / Product Hunt / Hacker News, and the dashboard automatically distributes across channels: Mastodon, Bluesky, Threads, Reddit, LinkedIn, Telegram

8. **Monitoring** — `morning-report.ps1` checks every morning: is there traffic? Is GA4 working? Is everything alive?

### In One Sentence

This is your **standard pipeline**: from idea to a working product that gets promoted and monitored — and every new project follows the same tracks.

---

## Full Flow

### 1. Start: Idea
Everything begins with the 💡 Idea node — the entry point.

### 2. Planning
Idea leads via arrow to the 📐 Planning block, where three documents sit horizontally:
- **ARCHITECTURE.md** — project architecture
- **mermaid-diagram.html** — visual diagram
- **implementation_plan.md** — implementation plan

### 3. Terminal
From Planning, an arrow goes to 💻 Terminal (`100star-init.ps1`) — the project scaffold script. Terminal is a hub: three arrows branch out to three large yellow containers.

### 4. Site-decor (yellow container)
Before building the front-end, you prepare visual assets:
- favicon.svg / .ico, og-image 1200×630, cover Dev.to 1000×420, cover GitHub repo, logo.png

### 5. Front-end (yellow container)
Vertical structure top to bottom:

**🔑 Authentication → 🎨 Design & UI → 🔍 SEO & Optimization**

- **Authentication**: Google Auth (OAuth 2.0, Rainbow border) and GitHub Auth (OAuth, github-24292f.svg)
- **Design & UI** — combined block with three sub-blocks:
  - *Tokens & Fonts*: site-design/ (Lato/Sora, CSS Variables, dark/light), colors (Accent #6078ff, Text #33334f), animations (0.2s buttons, scale(1.2) icons)
  - *UI Elements*: theme toggle (site-design/icons/ moon/sun SVG), social icons (site-design/icons/, 25 SVG, gray→brand hover), external link arrows, Welcome Modal
  - *Layout*: Header (logo+nav+theme, clamp sizing), Hero (text+image, badge pill), Features (3 cards desktop, stack mobile), Footer (text+social, gray #999)
- **SEO & Optimization**: SEO (title, meta, OG, twitter:card, canonical, JSON-LD, sitemap, robots, Search Console), PWA (manifest, Service Worker, favicon set), Performance (Core Web Vitals, mobile-first @768px, clamp())

Dotted connections inside: `site-design/` links to Header, Footer, and Theme Toggle. Social Icons links to Footer.

### 6. GitHub Repo — Public Face (yellow container)
What's visible on GitHub:

- **📄 Documentation**: README.md + ARCHITECTURE.md (with clickable link to readme-guidelines), ROADMAP.md + CHANGELOG.md, MANUAL.md
- **📎 Metadata**: llms.txt / llms-full.txt, LICENSE MIT + .gitignore + .npmignore, README badges (shields.io, badge-check.ps1)

Dotted connection: Repo ↔ ARCHITECTURE.md in the Planning block (same document).

### 7. Back-end — Code & Infrastructure (yellow container)
Vertical flow top to bottom:

**💻 Source Code → 🔒 Security → 🚀 Deploy → ⚙️ CI/CD → 📦 Release → 🔌 Services → 📡 API**

- **Source Code**: src/lib/api + package.json, bin/cli.js (Commander.js), tests/ (lint, audit)
- **Security**: .env + safe-push + npm audit + .env.example, pin versions + .npmignore
- **Deploy**: Vercel (Hobby free, 100GB bw, 10s timeout), GitHub Pages (500MB, free), Alibaba ECS (Singapore, $1.6/mo stopped), *.osovsky.com (GoDaddy)
- **CI/CD**: GitHub Actions (Auto-deploy), Lint · test · badges, readme-lint.yml
- **Release**: npm publish (npx project-name), GitHub Release (tag · changelog)
- **Services** (dashed border): Cloudflare (DNS+SSL, R2 10GB free), Resend (email 100/day), Upstash Redis (10K cmd/day)
- **API**: GitHub Actions (CI/CD, ∞ min public), GA4 (Analytics, 14 mo retention), Gemini 2.5 Flash (AI API)

Dotted connections: GitHub Actions ↔ Vercel, CI/CD Actions ↔ Vercel, README ↔ SRC. Repo Public arrow leads to Back-end (docs describe code).

### 8. Cross-connections (dotted)
- SEO → Vercel and GitHub Pages (landing deploy)
- SEO → GA4 (analytics)
- Google Auth → Services (OAuth)

### 9. Autoposting Dashboard (yellow container)
Front-end and Back-end both lead via arrows to Autoposting Dashboard. Inside:

- **🚀 Publishing**: Dev.to (article + checklist: no Russian text, no real IPs, raw.githubusercontent images, clickable link to write-article-workflow.md), Product Hunt 🚀, Hacker News 🟠
- **📢 Distribution Channels**: Mastodon, Bluesky, Threads, Reddit, LinkedIn+X, Telegram
- **⚙️ Engine**: Dev.to API (articles.json), sync-articles.ps1 (Redis sync), modal.js (Preview→Publish), render.js (Calendar grid)

Connections: Publishing → Channels, Engine → Channels. Dev.to Article is dotted-linked to Dev.to API (one side writes, other reads).

### 10. Monitoring (yellow container)
From Autoposting Dashboard, an arrow leads to 📊 Monitoring — the endpoint:
- morning-report.ps1, GitHub Traffic, npm downloads, GA4 → TG alerts

---

## Full Pipeline in One Line

**Idea → Planning (arch + mermaid + plan) → Terminal → Site-decor → [Front-end + Back-end + Repo] → Autoposting Dashboard (publishing → channels) → Monitoring**
