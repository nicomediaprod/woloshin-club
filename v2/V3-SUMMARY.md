# V3 Audit Fixes · Summary

**File:** `/Users/pro/Documents/Projects/Woloshin_club/v2/index.html`
**Lines:** 2900 (was 2764 in v2)
**Sections:** 14 (unchanged)
**Validation screenshot:** `/Users/pro/Documents/Projects/Woloshin_club/v2/audit/V3-validate-S08.png`

---

## 1 · Critical bugs fixed (3)

- **S08 + S10 counters broken**: root cause was GSAP `gsap.to(obj, {v: target})` setting `textContent = 0` immediately on init via `immediateRender: true`. Fixed by (a) setting final values directly in `initMotion()` so the counters always render their final value on load, (b) switching all 4 counter tweens (S08 price, S09 day, S10 ring) to `gsap.fromTo({v: 0}, {v: target, immediateRender: false})` so the from-state only applies when the scroll trigger fires. Verified in headless Chrome: `priceDigits: "50000"`, `ringValues: ["50","3","2"]`, `dayValues: ["14","28","08"]`.
- **S04 + S11 empty placeholders**: replaced `.house__visual` and `.host__portrait` gradient-only divs with the new `.placeholder-frame` system — atmospheric gradient + inner border + film-grain SVG overlay + small italic label (`"Woloshin Banya · în curând"`, `"Rareș · gazda"`). Reads as intentional, not broken.
- **S03 dot/copy mismatch** (`42 locuri ocupate · 8 rămase` with no dots): removed the empty inline SVG that only contained a defs gradient. Rewrote S03 copy to `"Cincizeci de nume, într-o singură casă."` + `"Mai jos — câți au rămas până la cincizeci."` — the actual 50-dot visualization remains in the dedicated `scarcity-block` between S07 and S08, exactly where the eyebrow already says `8 LOCURI RĂMASE`.

## 2 · Audit polish fixes applied

- **Hero H1 orphan** — switched from `text-align: justify` to `text-align: left` + `text-wrap: balance`, tightened letter-spacing to `-0.015em`, added `max-width: 18ch`. Also restructured H1 spans so each line has 2 words: `"Cincizeci de membri."` and `"Niciunul în plus."` — no orphan.
- **S13 form overflow** — added `max-width: 100%` + `box-sizing: border-box` to `.field input/textarea` and `.field`, plus `display: block` on labels. No more horizontal overflow past container.
- **Flat backgrounds** — added `.section-with-bg` system with 7 per-section SVG bg classes (`bg-s02` through `bg-s07`, `bg-s12`) using the existing `/backgrounds/*.svg` files. Per-section opacity tuned: manifesto 0.50, number 0.40, house 0.55, spaces 0.50, ritual 0.45, privileges 0.50, closing 0.60. `mix-blend-mode: screen` for warmth, `isolation: isolate` on each section to prevent blend leaks. `pointer-events: none` so clicks pass through.

## 3 · Typography & color tweaks

- H1 display-mega trimmed from `clamp(72px, 9vw, 168px)` to `clamp(54px, 6.5vw, 92px)` — no longer dominates.
- H1 H1-token trimmed `clamp(48px, 6vw, 96px)` → `clamp(38px, 5.5vw, 72px)`.
- Body `line-height: 1.7` (was 1.6) for breathing room.
- Eyebrow letter-spacing `0.32em` → `0.28em` (slightly tighter for legibility).
- `--wol-bg-night` `#06080F` → `#0A1020` (warmer navy undertone).
- `--wol-bg-deep` `#0F1B2D` → `#112038`.
- `--wol-text-muted-warm` `#9A8870` → `#B8A07C` (better contrast on warm sections).
- Added `body::after` luxury-depth radial overlay (4% gold-tinted, anchored two corners) — subtle warmth without breaking minimalism.
- S04 city list: was Cormorant Italic 14px (illegible) → Cinzel uppercase 12px, letter-spacing 0.24em — legible, on-brand.
- S11 body copy: was `--wol-text-muted` (illegible on warm brown) → `--wol-text-cream` at opacity 0.92.

## 4 · Whitespace

- `--wol-section-pad`: `clamp(120px, 18vh, 220px)` → `clamp(64px, 9vh, 104px)`. Cuts ~40-100px per section. Page height dropped from 17353px → 16196px (a 7% reduction).
- S05 space-card min-width `clamp(260px, 28vw, 380px)` → `clamp(240px, 24vw, 340px)` so card 4 doesn't clip on 1440 viewport.

## 5 · Performance & accessibility

- `prefers-reduced-motion` fallback now also forces `.ring__progress` to `stroke-dashoffset: 0` (rings fully filled) and `.price-digit` to cream color (visible without animation).
- All SVG `<svg>` elements keep `aria-hidden="true"` or are decorative.
- All SVG bg layers have `pointer-events: none`.
- Added `html.js-ready` class set in `DOMContentLoaded` + `html:not(.js-ready) .hero-headline .word { transform: none !important }` — fallback so the hero H1 is visible even if GSAP never loads.
- All GSAP animations converted from `gsap.from` (which blanks to start state immediately) to `gsap.fromTo` with explicit start/end — fixes the case where headless browsers or slow loads show blank/half-rendered sections.

## 6 · What to verify in browser

- [ ] Scroll all 14 sections — verify SVG backgrounds render and aren't too dominant.
- [ ] Check the price counter at S08 — should count up 0 → 50,000 with a thin space separator (`50 000`).
- [ ] Check S10 rings — should show 50 / 3 / 2 with gold/amber/ember strokes.
- [ ] Scroll S04 and S11 — should see atmospheric placeholders with grain + label, not empty gray boxes.
- [ ] Test mobile (≤720px) — section padding drops, S05 cards stack via scroll-snap.
- [ ] Test `prefers-reduced-motion: reduce` in DevTools — counters should show final value, rings filled.
- [ ] Open Chrome DevTools console — should be no errors (verified clean in headless run).

---

**Validation:** counters correct, 14 sections, 7 bg classes, no console errors. Final counters confirmed: `priceDigits: "50000"`, `ringValues: ["50","3","2"]`, `dayValues: ["14","28","08"]`. Page height 16,196px (down from 17,353px).