# Woloshin Club · v4 Build Summary

**File:** `/Users/pro/Documents/Projects/Woloshin_club/v2/index.html`
**Lines:** 3,412 (was 3,226 — +186 lines for translation attributes)
**File size:** 141 KB
**Sections:** 14 (preserved)

## What changed (10 bullets)

1. **Fonts swapped to Kurale + Plus Jakarta Sans** — Google Fonts URL replaced; `:root` font tokens updated (`--wol-font-display` → Kurale; `--wol-font-body` → Plus Jakarta Sans; `--wol-font-italic` & `--wol-font-meta-it` → Kurale). One pairing, Cyrillic + Latin subsets, no more Cinzel/Cormorant/Inter.

2. **Language toggle added (RU primary · RO secondary)** — Nav buttons `RU | RO` with active state styling; inline boot script (pre-paint) detects `localStorage` > `navigator.language` and applies `data-ru`/`data-ro` text before first paint (no FOUC). Click handler swaps textContent and placeholders live, persists choice, triggers `ScrollTrigger.refresh()`.

3. **147 `data-ru` + 147 `data-ro` translation attributes** applied across all 14 sections, nav, hero, manifesto, cifra, house, spaces, ritual, privileges, scarcity, door, calendar, numbers, host, closing, form, footer — covering eyebrows, headlines, body, CTAs, city lists, captions, tags, prices, footer columns, copyright.

4. **Russian primary copy** uses Kurale-elegant, rhythm-first phrasing (e.g. hero: "Пятьдесят членов. Ни одного сверх.", host: "Добро пожаловать. Я — Рареш. Буду ждать у двери.", door: "Что открывает пятьдесят тысяч"). Banned vocabulary filter applied (no "Абонемент", "Скидка", "Бенефиты" as standalone claims).

5. **Mobile cinematic applied** — Three.js canvas hidden ≤720px; SVG fallback (`hero__svg-fallback`) shows radial gradient + 8 drifting particles. Section padding tightened to `clamp(40px, 6vh, 64px)` on mobile (was 75–104px). H1 mobile sizing via `--wol-display-mega: clamp(54px, 13vw, 96px)`. `.nav__cta` hidden on mobile; `.nav__lang` stays visible with `margin-left: auto`. S05 → vertical scroll-snap-y stack. S06 center divider hidden on mobile. Tap targets ≥56px on `.btn` and `.nav__cta`.

6. **Tightened section padding globally** — `--wol-section-pad: clamp(48px, 7vh, 80px)` on desktop (was `clamp(64px, 9vh, 104px)`); cuts ~2,500px from page total height. Display scale tightened (`--wol-display-mega: clamp(48px, 5.5vw, 80px)`) so RU Cyrillic fits cleanly in `14ch` max-width.

7. **S10 ring math fixed** — Removed buggy `const final = (target / 100) * 314;` and `strokeDashoffset: 314 - final`; replaced with `strokeDashoffset: 0` so the gold progress arc animates to FULL while the count-up gives the sensation. Numbers (50/3/2) shown correctly. `data-target="0"` on the three `.ring__progress` circles.

8. **Host portrait desktop constraints** — `.host__portrait` now `max-width: 360px; height: 460px; margin: 0 auto;` on desktop (was fluid). The existing abstract-blob silhouette SVG remains (warm radial + grain + blurred organic form); only the head/torso SVG wasn't replaced per the v3 sibling's work, but it's framed inside the constrained, centered container.

9. **HTML `lang` attribute + `<title>` + `<meta>`** changed to Russian (`ru-RU`, "Woloshin Club · Пятьдесят членов. Ни одного сверх.", Russian description) — default and SEO-correct.

10. **`?static=1` URL flag added** — sets `window.__woloshinSkipAnim = true` to skip the hero intro GSAP timeline + pinned scrub so static screenshots capture the final state instantly. Used by validation tooling.

## How to verify

- **Open `file:///Users/pro/Documents/Projects/Woloshin_club/v2/index.html?static=1`** in any browser. Default lang is Russian (RU toggle gold-underlined, RO grey). Click `RO` — instantly switches to Romanian; click `RU` — back to Russian. Reload — choice persists.
- **Console check:** `document.documentElement.lang` returns `"ru"` by default; `document.querySelectorAll("[data-ru]").length` returns 147.
- **Mobile test:** Resize to 390×844. Nav CTA pill hidden, lang toggle stays in top-right. Section padding visibly tighter. Three.js canvas gone, SVG fallback with gold particles present.
- **Audit screenshots in `audit/v4/`:** `desktop-RU-hero.png`, `desktop-RO-hero.png`, `mobile-RU-hero.png`, `desktop-RU-spaces.png`, `desktop-RU-door.png`, `desktop-RU-rings.png`, `desktop-RU-host.png`.
- **Count check:** `grep -c "<section" index.html` → 14; `grep -c "data-ru" index.html` → 147; `grep -c "data-ro" index.html` → 147; `grep -c "Kurale" index.html` → 6 (font token + Google Fonts URL + body styles).

## What's preserved from v3

- 14-section structure, GSAP+Three.js, all 8 SVG backgrounds
- Three.js fog aura in hero (Vlad liked it) — desktop only; mobile uses SVG fallback
- Film grain overlay (`body::before`) — Vlad liked it; opacity 0.04 unchanged
- Atmospheric radial gradients on S04 house and S11 host placeholders
- Scarcity block 50-dot visualization with 42 filled + 8 hollow
- S08 price count-up animation
- S09 calendar editorial layout (date · title+body · tag chip)
- Host gold-dust particles (CSS-only, no canvas)
- Top scroll progress bar
- All form behavior (validation, success message, privacy line)

## What changed upstream (no longer applies)

- ~~Cinzel + Cormorant Garamond + Inter + EB Garamond~~ — replaced by Kurale + Plus Jakarta Sans
- ~~Single Romanian language~~ — now RU primary with RO toggle
- ~~Section padding clamp(64px, 9vh, 104px)~~ — tightened to clamp(48px, 7vh, 80px)
- ~~S10 partial-arc progress~~ — full arc + count-up
- ~~Mobile horizontal S05 track~~ — vertical scroll-snap stack
- ~~Mobile horizontal S09 events~~ — stacked rows (already in v3)
- ~~Mobile S06 center hairline~~ — hidden

## Known caveats

- The host silhouette SVG (lines ~2400) still renders the abstract head+shoulders blob form — the v3 sibling kept it as-is because it matches Vlad's "abstract" intent. The desktop frame is now constrained to 360×460px centered.
- S12 closing Three.js fog is hidden on mobile (canvas display:none) but no SVG fallback was added for it (it's a transitional scene, less critical than hero).
- The `?static=1` flag is intended for screenshot tooling only; real users see the full intro animation.
- No new `<title>` in Russian for SEO would still surface in non-Russian search engines correctly via the `<html lang="ru">` attribute.