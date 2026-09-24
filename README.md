# Woloshin Club — Landing Page

Premium membership landing page for **Woloshin Club** (Moldova) — 50 members only, 50 000 MDL entry. Self-contained single-file HTML, GSAP + Three.js motion, SVG atmospheric backgrounds, Russian primary with Romanian toggle.

**Live preview:** open `index.html` directly in a modern browser (Chrome/Safari/Firefox/Edge, last 2 versions).

---

## What this is

A scroll-driven, cinematic luxury landing page built as a **single self-contained HTML file** (`index.html`, ~141 KB, ~3,420 lines). No build step, no server required, no external assets except Google Fonts CDN.

Designed for:
- Russian-speaking primary audience (default)
- Romanian as secondary (`RU | RO` toggle in nav, localStorage-persisted)
- Desktop (1440×900+) and mobile (390×844 iPhone-class), both luxury-tuned

---

## Quick start

```bash
# Just open the file
open index.html       # macOS
xdg-open index.html   # Linux
start index.html      # Windows

# Or serve it (recommended for proper font loading)
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## What's inside

| Section | Name | Purpose |
|---------|------|---------|
| S01 | Hero / Threshold | Big headline, Three.js fog aura, nav, RU/RO toggle, CTA |
| S02 | Manifesto | Pinned 4-line poetic declaration |
| S03 | The Number | Giant "50" + 50-dot scarcity grid (42 filled) |
| S04 | The House | Woloshin Banya context, editorial paragraph |
| S05 | The Spaces | Horizontal-scroll 5 banya world cards |
| S06 | The Ritual | 7-beat timeline of arrival sequence |
| S07 | The Privileges | 8 numbered editorial privilege list |
| S08 | The Door | Single `50 000 MDL` price numeral + subline |
| S09 | The Calendar | 3 events per year with editorial descriptions |
| S10 | The Numbers | 50 / 3 / 2 rings (Aston Martin dashboard style) |
| S11 | The Host | Personal administrator — abstract silhouette + signature |
| S12 | The Closing | CTA moment with fog-parting Three.js scene |
| S13 | The Form | Editorial 2-field contact form (Email + optional phone + message) |
| S14 | Colophon | Footer with logo, contact, legal |

---

## Tech stack

- **HTML5** — single file, semantic `<section>` / `<article>` / `<nav>` / `<footer>`
- **CSS** — inline `<style>` block, design tokens from `woloshin.css` (deep navy `#0F1B2D`, gold `#C9A24A`, amber CTA `#F5A623`)
- **JS** — inline `<script>` blocks at end of body
  - **GSAP 3.12.5** + **ScrollTrigger** (cdnjs) — master timeline, scrubbed section reveals, counters, text reveals
  - **Three.js r163** (ESM importmap, unpkg) — fog + 240 particles hero, fog-parting closing scene
  - Vanilla **IntersectionObserver** — pause Three.js off-screen, swap renderer scenes
- **Fonts** (Google Fonts CDN) — Kurale (display + serif italic) + Plus Jakarta Sans (body + UI), Cyrillic + Latin
- **Backgrounds** — 8 inline SVG atmospheric gradients in `backgrounds/` (vector, ~2-4 KB each)

---

## Project structure

```
Woloshin_club/
├── index.html                 # THE LANDING PAGE (single self-contained file)
├── backgrounds/               # 8 SVG atmospheric backgrounds
│   ├── S01-hero-bg.svg        #   Hero fog + warm radial
│   ├── S02-manifesto-bg.svg   #   Soft amber glow upper-left
│   ├── S03-number-bg.svg      #   Near-black + ember lower-right
│   ├── S04-house-bg.svg       #   Stone-wood ritual texture
│   ├── S05-spaces-bg.svg      #   21:9 midnight + bottom firelight
│   ├── S06-ritual-bg.svg      #   9:16 thin gold center line
│   ├── S07-privileges-bg.svg  #   Velvet + gold fade top
│   └── S12-closing-bg.svg     #   Dark portal with gold slit
├── agents/                    # Process artifacts (read-only, not loaded by site)
│   ├── copy/                  # Romanian master copy
│   ├── copy-ru.md             # Russian primary copy (used in HTML)
│   ├── translate-map.md       # Per-element RU/RO mapping
│   ├── design/out.md          # Design specification
│   ├── motion/out.md          # GSAP + Three.js specification
│   ├── research/out.md        # Luxury reference research
│   ├── mobile-cinematic.md    # Mobile design spec
│   ├── final-audit.md         # v2 visual audit
│   ├── critique-v3.md         # v3 review (KEEP/FIX/DROP)
│   ├── copy-rudit.md          # Russian copy audit (AI slop)
│   ├── copy-critic.md         # Russian copy tone critique
│   └── copy-rewrite-summary.md # What the rewriter changed
├── archive/                   # Earlier iterations
│   ├── index.html             # v2 (3002 lines)
│   ├── IDEA.md
│   ├── preview-*.png
│   └── 02 — Брендбук — Сказочная система v3.html
├── V3-SUMMARY.md              # What changed v2 → v3
├── V4-SUMMARY.md              # What changed v3 → v4 (RU/RO + new fonts + mobile)
├── AGENTS.md                  # Conventions for AI agents working on this project
├── ARCHITECTURE.md            # Technical deep-dive
└── HANDOFF.md                 # Current state + next steps for the next agent
```

---

## For AI agents working on this

**Read these in order before touching anything:**

1. **AGENTS.md** — conventions, banned words, what NOT to change
2. **HANDOFF.md** — current state of work, what was decided, what's next
3. **ARCHITECTURE.md** — technical deep-dive (fonts, motion system, language toggle, accessibility)

---

## Conventions

- **Russian is primary** — default text shown is Russian (`data-ru`). Romanian is secondary (`data-ro`).
- **No external assets except Google Fonts CDN** — all SVGs are inline or in `backgrounds/`, all JS is inline.
- **Strict palette** — only brand tokens from `woloshin.css` (deep navy, gold, amber, cream). No new colors without explicit approval.
- **Typography** — Kurale (display, serif italic) + Plus Jakarta Sans (body). Do NOT introduce new font families.
- **Banned Russian words** — `привилегия`, `премиальный`, `эксклюзивный`, `уникальный`, `абонемент`, `бенефиты`, `почувствуйте`, `откройте для себя`. Use concrete language instead.
- **Banned patterns** — `Это не X — это Y` used more than once per section, `Здесь [verb]` poetic openers, empty intensifiers (`абсолютно`, `действительно`, `поистине`).
- **Accessibility** — `prefers-reduced-motion: reduce` honored throughout. Semantic HTML. ARIA labels on rings, form fields, navigation.

---

## License

Internal project. © Woloshin Club 2026. All rights reserved.
