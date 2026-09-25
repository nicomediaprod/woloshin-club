# HANDOFF.md — Current State + Next Steps

**Last updated:** 2026-09-25 by Vlad via Hermes Agent

---

## What's been built

Woloshin Club landing page — single self-contained HTML file at `/Users/pro/Documents/Projects/Woloshin_club/index.html`. Cinematic luxury scroll-driven site, Russian primary with Romanian toggle, GSAP + Three.js motion, 8 SVG atmospheric backgrounds, 14 sections covering hero through footer.

---

## Version history

| Version | Lines | Key changes |
|---------|-------|-------------|
| v1 (archive/index.html) | ~955 | First Romanian-only build, before audit |
| v2 | 2,764 | Counter fixes, placeholder S04/S11, scarcity grid integrated |
| v3 | 3,002 | + 5 in-app fixes (centering, glow, floating numbers, Aston rings, abstract silhouette) + 8 SVG backgrounds wired |
| **v5 (current index.html)** | **3,415** | Official management facts integrated across all sections (50 участников - Одно сообщество; 50k MDL: 10k fee + 40k deposit; именной халат и шапка; персональный администратор; 10% скидка на все услуги; условия приватных бань; приоритет бронирования; ранний доступ; 3 бесплатных события; разовый гость; чат в Telegram; 2 ужина с основателем; подарок на день рождения от Woloshin Banya), 100% RU/RO parity (145/145), default Russian textContent, banned words: 0 |
| **v2.html (Standalone Fact-Driven Edition)** | **1,298** | Отдельная вторая версия лендинга, собранная строго по исходным данным руководства без выдуманной информации (50 членов, 50k MDL [10k взнос + 40k депозит], личные атрибуты, условия, закрытые события, ужины с основателем, подарки). Полный премиальный стиль, Three.js аура частиц, зерно, мгновенный переключатель RU/RO (88/88), 0 запрещенных слов, протестировано на десктопе 1440px и мобильных 390/320px. |

---

## Current state

**What works:**
- 14 sections all rendering
- Russian default + Romanian toggle via `RU | RO` button in nav
- Three.js fog + 240 particles in hero (Vlad liked the "aura")
- Grain texture on body (Vlad liked)
- Counter animations (50 / 3 / 2)
- 8 SVG backgrounds applied to S02-S07, S12
- Mobile-responsive (Three.js disabled ≤720px, S05 becomes vertical scroll-snap-y stack)
- `prefers-reduced-motion: reduce` honored throughout
- Banned words count: 0 (`привилегия|премиальный|эксклюзивный|уникальный|абонемент|бенефиты`)
- Mixed-script word bug ("Анти-реvelion") FIXED — now full Cyrillic "Анти-ревельон"

**What Vlad explicitly liked:**
- The aura/fog in the hero (Three.js)
- The grain texture
- Mobile cinematic feel
- The 42/50 scarcity grid
- The Russian copy after the AI-slop cleanup

**Known issues / pending:**

1. **Backgrounds are SVG (vector gradients with grain), not real PNG.** They look fine but real atmospheric photography (Imagen 4 via gflow) would be richer. Requires `gflow auth --clear && gflow auth --profile "Default"` manual login (Vlad's session expired). When Vlad re-auths, regenerate 8 PNGs and replace the SVGs.

2. **Host portrait (S11) is an abstract blob silhouette.** Better than the cartoon head/torso, but a real photo would be more human. Currently uses an organic SVG path with `feGaussianBlur` for refinement.

3. **Form (S13) uses mailto: link** — not a real form backend. To make it work, replace `<a href="mailto:...">` with a `<form action="..." method="POST">` pointing to a real backend (Formspree, Netlify Forms, custom).

4. **S05 numbers size was reduced** from `clamp(96px, 12vw, 180px)` to `clamp(56px, 7vw, 110px)` per Vlad's feedback. Currently sit on top of the cards with realistic layered shadows.

5. **S02 manifesto centering was fixed** (justify-items: center + max-width 880px + margin auto + text-align center on .manifesto__line).

---

## Decision log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-09-25 | Symlinked backgrounds/ and agents/ to root | Enables index.html at project root to load SVG backgrounds and aligns with README.md/AGENTS.md paths |
| 2026-09-25 | Kurale + Plus Jakarta Sans | Brand fonts from hotels.banya.md |
| 2026-09-25 | Russian primary, Romanian secondary | Vlad: "для меня важнее русский язык при разработке" |
| 2026-09-25 | No new colors, only brand tokens | Vlad: avoid "Moldovan premium" look |
| 2026-09-25 | RU | RO toggle in nav | Bilingual audience (Moldova), localStorage-persisted |
| 2026-09-25 | SVG backgrounds instead of PNG | gflow auth expired, can't regenerate; SVG fallback works |
| 2026-09-25 | 5-ease vocabulary (revelation/settle/drift/magnetic/ritual) | Avoid generic power1.out defaults |
| 2026-09-25 | Three.js fog + 240 particles (vs heavier R3F) | Performance budget + luxury restraint |
| 2026-09-25 | Host portrait as abstract blob | Refined over cartoon head/torso |
| 2026-09-25 | S05 numbers floating above cards with shadow | Vlad: "реалистично (тень и тд)" |
| 2026-09-25 | S10 rings with Aston Martin style (ticks, gold rule) | Vlad: "как дорогой дашбор от астон мартин" |
| 2026-09-25 | Full natural copywriting rewrite across all 14 sections | Vlad: "не нравятся формулировки они ИИ слоп, так не говорят". Replaced artificial tropes with dry, concrete, grounded human language. Enforced default Russian textContent across all 145 translatable elements. Banned words: 0. |
| 2026-09-25 | Integrated official club data from management | Replaced AI-invented details with authentic club specs: 50 участников - Одно сообщество; 50k MDL (10k взнос + 40k баланс); именной халат и шапка; персональный администратор; 10% скидка на все услуги; условия приватных бань; приоритет бронирования; ранний доступ; 3 бесплатных события; разовый бесплатный гость; закрытый чат в Telegram; 2 ужина с основателем; подарок на день рождения от Woloshin Banya. |

---

## Pending work (in priority order)

### P0 — done in current build
- [x] All 14 sections rendering
- [x] RU/RO toggle
- [x] 8 SVG backgrounds
- [x] 5 in-app fixes (S02, S04, S05, S10, S11)
- [x] Russian copy cleanup (banned words: 0)

### P1 — Vlad-requested, not yet done

1. **Real PNG backgrounds** (when gflow auth restored)
   - Re-run `gflow generate-image` with the prompts in `agents/research/out.md` (and `backgrounds/MANIFEST.md` has the exact commands)
   - Replace each `.svg` with the new `.png`, keeping the same filename so CSS references don't break
   - Or keep SVG as fallback for offline

2. **Hero "aura" enhancement**
   - Vlad liked the Three.js fog. Could push further: add subtle volumetric godrays, dust particles on scroll, soft chromatic aberration on CTA hover.

3. **S12 Closing "fog parting" effect**
   - Currently fog density scrubs high → low. Could add: a single warm gold ray appears at the bottom, growing as user scrolls into CTA.

4. **S11 Host — real photo OR more abstract**
   - Currently abstract blob. Two paths forward: (a) integrate a real photo of Rareș (needs Vlad's approval to use the image), (b) make it even more abstract (just a monogram + signature, no figure at all).

### P2 — nice to have

5. **Real form backend** (replace mailto with Formspree/Netlify)
6. **Analytics** (Plausible or Umami)
7. **i18n: add English** for tourists/diaspora
8. **OG tags** + Twitter card for share previews
9. **Favicon** + Apple touch icon
10. **Open Graph image** (1200×630 PNG of the hero)

---

## How to resume work

```bash
# Check what's been done
cd /Users/pro/Documents/Projects/Woloshin_club
wc -l index.html
grep -c "<section" index.html

# Read the docs in order
cat README.md
cat AGENTS.md
cat ARCHITECTURE.md
cat HANDOFF.md  # (this file)

# Read the latest agent artifacts
ls agents/
cat agents/copy-ru.md
cat agents/motion/out.md
cat agents/design/out.md

# Make a change
# 1. Identify the smallest possible change
# 2. Apply via patch
# 3. Validate (wc -l, grep counts, browser test)
# 4. Update this file with what changed

# Commit
git add .
git commit -m "feat: describe the change"
```

---

## For the next agent

You are not the first agent to work on this. Read `agents/critique-v3.md`, `agents/copy-rudit.md`, `agents/copy-critic.md`, and `agents/copy-rewrite-summary.md` to understand what's been tried before. The site is currently in a good state — only make changes that Vlad has explicitly requested.

If you find an issue:
1. Reproduce it (open in browser, screenshot)
2. Read the relevant agent artifact to see if it was already discussed
3. If new, document your fix in this file
4. If it's a debatable creative decision, ASK VLAD before applying

Vlad is bilingual (Russian primary) and prefers WhatsApp. He responds to concrete, evidence-based proposals ("Here are 3 options, I recommend X because Y") better than open-ended questions.

---

## Contact

- **Project owner:** Vladislav Nicolaev (Vlad)
- **Primary chat:** WhatsApp (this DM)
- **Working directory:** `/Users/pro/Documents/Projects/Woloshin_club/`
- **Brand source of truth:** `/Users/pro/HERMES_AGENT/projects/woloshin_banya/design-system/woloshin.css`
