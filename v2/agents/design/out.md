# WOLOSHIN CLUB — LANDING PAGE
## UX & Visual Architecture Specification

**Project:** Premium membership club. Moldova. 50 members. Entry 50,000 MDL.
**Language:** Romanian (ro-RO).
**Tone references:** Aman · Aesop · Soho House · 1970s editorial · Søren Carlée
**Brand tokens source:** `/Users/pro/HERMES_AGENT/projects/woloshin_banya/design-system/woloshin.css` (canonical — DO NOT fork)
**Stack assumption:** Next.js / Vue SSR + GSAP ScrollTrigger + Three.js (vanilla) for 3D scenes. Locomotive Scroll for smooth-scroll feel.

---

## 0 · READING ORDER

This document is read top-to-bottom. Each chapter builds on the prior. Skim the *Page Map* (§1) for the scroll skeleton, then go chapter-by-chapter for mood + content, then jump to §7 (3D), §8 (Microinteractions), §9 (Navigation), §11 (Tokens) when building.

---

## 1 · PAGE MAP

14 sections, divided into 4 scroll chapters. The page is one long scroll. No tabs, no modals except the application form (right-side sliding panel, not a full page takeover).

```
┌─ CHAPTER I — THRESHOLD ──────────────────────────────────────┐
│  S01  Pre-loader (grain + sigil + 1..50 counter)            │
│  S02  Hero                (full-viewport 3D fog + manifest)  │
│  S03  Manifesto           (single paragraph, 100vh pinned)  │
├─ CHAPTER II — BELONGING ─────────────────────────────────────┤
│  S04  The House           (split: portrait + quote)          │
│  S05  The Spaces          (horizontally-pinned arch cards)   │
│  S06  The Ritual          (numbered timeline vertical)       │
├─ CHAPTER III — PRIVILEGES ───────────────────────────────────┤
│  S07  The Privileges      (editorial list, 8 items)         │
│  S08  Membership          (typographic pricing composition)  │
│  S09  The Calendar        (vertical event timeline)          │
│  S10  The Numbers         (3 ring counters, single beat)     │
├─ CHAPTER IV — CLOSING ───────────────────────────────────────┤
│  S11  The Host            (portrait + mouse-reactive layer)  │
│  S12  The Door            (final 3D moment: fog parting)     │
│  S13  Apply / Inquire     (minimal 3-field form)            │
│  S14  Colophon / Sigil    (footer)                          │
└──────────────────────────────────────────────────────────────┘
```

---

## 2 · SCROLL CHAPTERS

### CHAPTER I · "Threshold" — mood: cinematic, sparse, hovering
**Visual language:** Deepest blacks (#06080F), heavy vignette, kinetic type, one 3D scene (volumetric fog). No rules, no grids, no lists. Read like a film opening.
**Motion language:** Slow reveals. Words drift in. No bounces. Easing `cubic-bezier(0.16, 1, 0.3, 1)` (expo-out). Average section dwell: 4–8 seconds.
**Density:** 0–1 blocks per section. Mostly whitespace.

### CHAPTER II · "Belonging" — mood: editorial, denser, slightly warmer
**Visual language:** Warm undertones emerge (zinc→burnt umber tinting). Cormorant Garamond italic returns for captions. The arch-radius returns in physical form (room cards). Begins to feel inhabited.
**Motion language:** Scroll-pinned horizontal card parade in S05. Vertical timeline in S06 reveals as you scroll. Pinned parallax portraits. Easing slightly faster: `cubic-bezier(0.65, 0, 0.35, 1)`.
**Density:** 2–3 blocks per section. Real content begins.

### CHAPTER III · "Privileges" — mood: architectural, typographic
**Visual language:** This is where the editorial-infographic system lives. 01/02/03 numerals in Cinzel Display 600, italic Cormorant labels. Generous vertical rhythm (140px+ between items). This is the page's *informational* breath — still elegant, never crowded.
**Motion language:** In-place reveals, no parallax. Words stagger in from below at 12px translateY. A single marquee strip runs once across the chapter break (ritual text).
**Density:** 4–6 blocks per section. Heaviest informational beat of the page, but still airy.

### CHAPTER IV · "Closing" — mood: ceremonial, quiet, decisive
**Visual language:** Vignette returns, world narrows. The host portrait breaks the typographic system with a single warm photo. The door 3D is the page's final dynamic gesture. The form is plain — no decoration. The colophon reads like a book's last page.
**Motion language:** Slower than chapter III. CTA hovers gently. Door fog is the slowest, most deliberate motion on the page. Final keystroke reveal of email is sharp and instant.
**Density:** S01, S04, S13 — each have 1 block. S14 has the most info (contact, hours, address, IG, etc) but it's set in small print.

---

## 3 · SECTION-BY-SECTION SPEC

> **Reading convention:** each section is `120vh` unless pinned. Content max-width `1440px` centered inside a 12-col grid (8.33% gutters). All measurements in REM (1rem = 16px). Type sizes scale linearly between `1280px` and `1920px` viewports (`clamp()`).

---

### S01 · Pre-loader (Chapter I)
**Layout:** Full viewport, centered. No grid. Background = grain texture (5% opacity, blend-overlay) over `--wol-bg-night`.
**Typography:**
- 1px gold hairline at 12% viewport height — `letter-spacing: 0.4em` small caps "WOLOSHIN · CHIȘINĂU · 2026"
- Cinzel Display 600, 14px → counter ticks `01 → 50` over 1.8s (count-up script, easing expo-out)
- Last value `50` holds; fades; logo sigil fades in (200ms)
**Content:** Nothing else. Whitespace carries the weight.
**Motion:** Counter ticks, no other motion. Logo fades in 200ms after counter completes. Then unloads (fade out 600ms) and reveals hero.
**3D:** None.
**Density:** Zero blocks — pure ceremonial moment.

---

### S02 · Hero (Chapter I)
**Layout:** Full viewport. 12-col grid for content layer only; 3D canvas fills viewport.
**Grid:**
- Top: eyebrow (cap 12, tracked 0.4em) at row 1, col 1–4
- Vertical center: H1 mega display occupies cols 3–10, vertically anchored to center
- Bottom row: italic Cormorant line, cols 1–6
- Below that: small CTA + scroll cue, cols 1–4
**Typography:**
- Eyebrow: `Inter` 13px, `letter-spacing: 0.32em`, `--wol-text-muted`, "O INVITAȚIE · 50 DE LOCURI"
- H1 (mega): `Cinzel` 600, `clamp(80px, 9vw, 168px)`, line-height 0.96, `--wol-text-white`, uppercase. Two words per line, forced line break.
  - Example copy: *"Nu este un club. / Este o casă."*
- Subtitle: `Cormorant Garamond` italic 500, `clamp(24px, 2.2vw, 36px)`, `--wol-text-muted-warm`, max 12 words.
- Scroll cue: tiny gold dot at viewport bottom, pulsing `2.6s` ease-in-out infinite, 8px → 12px size, 30% → 60% opacity
**Content blocks:** 3 — eyebrow, H1, subtitle
**Motion:**
- On load: H1 word 1 fades+drifts up (translateY 40px → 0, opacity 0 → 1, 800ms expo-out, delay 200ms). Word 2 follows at 400ms offset. Subtitle last at 1200ms.
- On scroll: H1 stays pinned while 3D fog rotates slowly (auto 0.04 rad/s). Subtitle parallax -8% Y.
- Eyebrow drifts left → out at 60% scroll progress.
**3D:** ⭐ **HERO 3D — Scene A: Volumetric Fog Chamber**
- Three.js (vanilla, no R3F — keeps bundle light)
- Scene: orthographic camera → plane geometry → custom GLSL fragment shader
- Shader: layered FBM noise, scrolls very slowly, mixed with gold-amber volumetric tint
- Background-color = deep night (#06080F); fog sampled with `--wol-gold` at 8% intensity, `--wol-ember` at 4%
- A single thin light-shaft ray (1px-wide) drifts left → right over 24s, alpha 12%
- Performance: pixel-ratio capped at 1.5, fullscreen `requestAnimationFrame` only when in viewport (IntersectionObserver pauses when offscreen)
- Mobile fallback: static high-quality JPEG poster frame + CSS conic gradient animation (cheap)
**Density:** Maximum 1 block visible at once. World is empty. Hero.

---

### S03 · Manifesto (Chapter I → II transition)
**Layout:** Centered, pinned for 200vh. Background = `--wol-bg-deep`. Vignette + grain.
**Grid:** Single block, centered, max-width 880px, cols 3–10.
**Typography:**
- Lead: `Cormorant Garamond` italic, weight 500, `clamp(28px, 3.4vw, 56px)`, line-height 1.35, `--wol-text-cream`
- 4 sentences, ~60 words total. They reveal line by line as you scroll the 200vh pin.
- Last line lands with `letter-spacing: 0.04em` weight bump (italic → still italic, but `--wol-gold` color)
**Content:** One paragraph. The club's point of view.
**Motion:**
- Sticky scroll: 200vh pin. As you scroll through it, sentence 1 reveals at 0%, S2 at 25%, S3 at 50%, S4 at 75%, S4 holds.
- Last sentence stays pinned after scroll-out and dissolves to next section.
- A thin vertical gold rule grows upward on left edge from 0 → 100% over the scroll, tracking progress.
**3D:** None.
**Density:** One block. A single thought.

---

### S04 · The House (Chapter II)
**Layout:** Split (60/40 image left, text right). Then a single horizontal rule, then a chapter-break marquee.
**Grid:**
- Image: cols 1–6, full section height, slight parallax (CSS only, translate -8% Y on scroll progress through section)
- Text panel: cols 7–12, padded, vertically centered
- Below split: full-width 1-line marquee strip, 240px tall, gold-on-deep
**Typography:**
- Eyebrow: "CAPITOLUL I" Inter 12px tracked gold
- H2: `Cinzel` 600, `clamp(36px, 4vw, 64px)`, `--wol-text-gold`, uppercase, 1-line
- Italic subtitle: `Cormorant Garamond` italic, 28px, `--wol-text-cream`, single sentence
- Body: `Inter` 17px, `--wol-text-muted`, 3 lines max, max 35 words
**Content blocks:** 3 (eyebrow / H2 / subtitle + body)
**Motion:**
- Portrait parallax -8% Y
- H2 splits in word-by-word (`SplitText` GSAP), 600ms each, 80ms stagger, expo-out
- After section ends: marquee scolls once right→left over 18s (CSS `@keyframes` translateX), text fades in at 30% scroll past
**3D:** None.
**Density:** Two blocks + one decorative marquee.

---

### S05 · The Spaces (Chapter II)
**Layout:** HORIZONTALLY SCROLL-PINNED. Section is 400vh tall. Content area is 100vh wide, scrolls horizontally for 300vh.
**Grid (inside the horizontal scroll):**
- Container: `display: flex; gap: 6vw; padding: 0 12vw`
- 5 arch cards, each `min-width: 28vw` (so 5 cards + 4 gaps + 2 endpads span ~232vw). At any time you see ~3.5 cards.
- Each card: full-height arch (`--wol-radius-arch`), photo bg + dark gradient overlay + zone name in Cormorant italic at bottom + tiny number 01–05 in Cinzel at top-right
- Background: deep + faint grain
**Typography (per card):**
- Number: `Cinzel` 600, 80px, `--wol-gold`, opacity 0.4
- Title: `Cormorant Garamond` italic 600, 72px, `--wol-text-white`, drop-shadow 0 4px 24px #000
- Caption: `Inter` 14px tracked uppercase, `--wol-text-muted-warm`
**Content blocks (per card):** Number + title + caption
**Motion:**
- Section pins at top on entry. As user scrolls vertically, content scrolls horizontally (GSAP `pin` + `x: -(totalWidth - viewportWidth)`)
- Each card fades up 80px and un-blurs (filter blur 8→0) as it crosses viewport center
- Number ticks once when card hits 50% of viewport
**3D:** Subtle. As each card crosses center, a `transform: perspective(1200px) rotateY(±2deg)` settles, parallax-coupled to scroll velocity. Pure CSS — no canvas.
**Density:** Five visible blocks across scroll, but at any instant only ~3 visible. Cinematic.

---

### S06 · The Ritual (Chapter II → III bridge)
**Layout:** Vertical timeline, 12-col grid with a single vertical gold rule at col 6 spanning the entire section. 7 numbered ritual beats, each spanning rows. Section is `min-height: 320vh` for breathing room.
**Grid:**
- Vertical gold line: col 6, opacity 0.4, dot markers (12px circles) at each beat, alternating cream and gold
- Beat items alternate: odd = text in cols 1–5 (left of line), even = text in cols 7–11 (right)
- Each beat: number 01–07 in `Cinzel` 600 48px gold, italic Cormorant 26px cream title, 2 lines of Inter body 16px muted
**Typography:**
- Section eyebrow: "CAPITOLUL II · RITUALUL" gold
- Section H2: "Șapte gesturi, înainte de miezul nopții." (or similar 7-word thesis)
- Each beat:
  - Number: 48px Cinzel 600 `--wol-gold`
  - Title: 28px Cormorant italic, `--wol-text-cream`
  - Body: 16px Inter, `--wol-text-muted`
**Content:** Numbered ritual beats (e.g. "01 — The arrival. Coat taken by hand.", "02 — The first pour.", "03 — Steam, oak, silence." …)
**Motion:**
- Vertical gold rule grows from top as scroll advances (SVG path stroke-dashoffset)
- Each beat's number ticks in (scale 0.85→1 + opacity 0→1, expo-out) when its dot crosses the 60% viewport line
- Italic title slides up 20px on beat entry
**3D:** None. This section is purest typography — the calm before the data.
**Density:** 7 beats across 320vh. Each beat has 3 micro-blocks (number/title/body). Generous spacing.

---

### S07 · The Privileges (Chapter III)
**Layout:** Two-column asymmetric. Left (cols 1–4): sticky chapter intro that pins as the right column scrolls. Right (cols 6–12): editorial list of 8 privileges.
**Grid:**
- Left sticky panel: H2 "Ceea ce aparții, prin simpla prezență." Cinzel 56px gold, max 8 lines, locked while right column animates
- Right column: list of 8 items, each item is a full row (~150px tall)
- Each item row: thin gold rule top + bottom + 4-column inner grid:
  - col A (number): Cinzel 32px gold "01".."08"
  - col B (icon): 32x32px thin-line SVG, cream stroke
  - col C (label): Cormorant Garamond italic 30px cream, privilege title
  - col D (descriptor): Inter 16px muted, 1 line, max 12 words
**Content:** 8 privileges. E.g.
1. *"The Door"* — Access via personal key, no queue, no announcement.
2. *"The Cellar"* — A 480-bottle library curated by sommelier.
3. *"The Library"* — Rare first editions and the right to be alone with them.
4. *"The Calendar"* — Twelve closed events each year. You are on the list.
5. *"The Steam"* — Unlimited access. Two rooms. Whatever the hour.
6. *"The Studio"* — A private workspace reserved under your name.
7. *"The Salon"* — For the conversations that take longer than dinner.
8. *"The Off-Season"* — Two weeks a year, the house travels. You may follow.
**Motion:**
- Sticky left panel = pin to section
- Right column rows: each row's title slides up 12px + un-blurs (filter blur 8→0) at its row entry
- Hover on row: gold rule brightens (`--wol-gold` → `--wol-amber`), icon shifts +4px right
**3D:** None.
**Density:** 8 blocks across right column, ~1200vh total scroll. Each row is its own beat.

---

### S08 · Membership (Chapter III)
**Layout:** Centered typographic composition. NOT A TABLE. A single editorial column, max-width 720px, centered in 12-col (cols 4–10).
**Grid:**
- Section eyebrow: "MEMBERSHIP" gold
- H2: "O singură invitație. O singură sumă. Fără excepții." Cinzel 56px cream, italic Cormorant 36px subtitle below
- Typographic pricing: numeral on its own line, descriptor below, total cadence like a magazine pull-quote
- Single tier, no comparison, no "from", no FAQ inline
**Typography:**
- Numerals: `Cinzel` 200 weight, `clamp(140px, 18vw, 280px)`, line-height 0.95, `--wol-text-cream`
- The "50 000" sets, then below in 36px italic Cormorant: "lei moldovenești"
- Below that: `Inter` 17px muted, single sentence clarifying one-time entry, lifetime access, no monthly dues
- Below that: stamp-style small frame "INCLUD · ACCES PE VIAȚĂ" (like a passport stamp, `--wol-stamp` reuse but smaller)
**Content blocks:** 4 (eyebrow / H2 / price / stamp)
**Motion:**
- Numerals count up from 0 → 50 000 over 1.4s on enter (ease-out-expo)
- "lei" italic subtitle fades in 200ms after numerals stop
- Single "Solicită invitația" gold-line button fades up 400ms later (NOT amber CTA here — gold because this is not final purchase)
**3D:** None. This is the page's most-quietly-numerous moment. No glow.
**Density:** Highest in typography, not in elements. One price, one stamp, one button.

---

### S09 · The Calendar (Chapter III)
**Layout:** Vertical timeline, similar to S06 but with date-pinned events instead of ritual beats. Section is 280vh tall.
**Grid:**
- Horizontal Cinzel eyebrow at top: "ANUL I · 12 EVENIMENTE"
- Vertical rule at col 6 gold-dotted
- Each event row alternates left/right of the rule, same beat-structure as S06
- Event rows: month (gold 14px tracked) + day (Cinzel 36px cream) + title (Cormorant italic 28px) + italic descriptor 2 lines
**Typography:**
- H2: Cinzel 56px gold "Douăsprezece seri. O singură listă."
- Event row inner:
  - Month eyebrow: Inter 12px tracked gold "NOIEMBRIE"
  - Day number: Cinzel 600 36px cream
  - Title: Cormorant italic 28px cream
  - Descriptor: Inter 16px muted
**Content:** 5–6 events shown (rest marked "Further dates by invitation only"), e.g.:
- *14 Noiembrie — "Cina cea mai lungă"* — wine-paired, eight seats, communal table
- *28 Noiembrie — "Vinul lui Rareș"* — vertical tasting of seven vintages
- *12 Decembrie — "Camera de lectură"* — silent evening, three rooms
- *20 Decembrie — "Abur și vorbă"* — winter steam + a fire
- *8 Ianuarie — "Anul Nou, devreme"* — anti-revelry, midnight reading
**Motion:** Same vertical-rule-grow + per-row reveal pattern as S06, but with day numerals count-ticking from "00" → "14" etc.
**3D:** None.
**Density:** 6 visible event blocks + 1 closure note.

---

### S10 · The Numbers (Chapter III)
**Layout:** Single 100vh section. Three gold ring counters centered as a row, evenly spaced (cols 3 / 6 / 9). Below them, one italic line of context.
**Grid:**
- Eyebrow: "CIFRE" Cinzel 14px tracked gold
- 3 `.wol-ring` instances side-by-side. Each: label + ring SVG + numeric value (gold bright) + tiny italic caption
- H2 (above rings, centered): "Cincizeci. Doisprezece. Unu."
- Below rings: italic Cormorant line 22px cream — single sentence tying them together
**Typography:**
- Ring value: Cinzel 60px gold-bright
- Ring inner label: Inter 12px tracked gold
- Caption below ring: Inter 16px muted, 1 line
**Content:**
- 50 — members
- 12 — closed events a year
- 1 — door (single key, never a queue)
**Motion:**
- H2 reveals word-by-word (SplitText)
- Rings stroke-dasharray from 0 → final value as scroll enters (800ms ease-out)
- Inner number count-up simultaneously
**3D:** None. Pure CSS/SVG.
**Density:** Minimal — three rings is the entire content.

---

### S11 · The Host (Chapter IV)
**Layout:** Split 50/50. Left: full-height portrait photo, warm tone. Right: single column of text, vertically centered.
**Grid:**
- Left: portrait, cols 1–6, full section height, 16:21 aspect ratio centered
- Right: cols 7–12
  - Eyebrow: "GAZDA"
  - Italic Cormorant 56px cream — personal greeting
  - 2–3 lines of Inter 17px muted
  - Signature mark at bottom (small handwritten-style SVG path, 180×60px)
**Typography:**
- Italic line: `Cormorant Garamond` italic 500, 36–56px, `--wol-text-cream`
- The greeting is in first person, in Romanian, signed by name
**Content:** A real human. A real greeting. (e.g. "Bun venit. Sunt Rareș. Vă aștept la ușă.")
**Motion:**
- Photo fades up 40px on enter
- Italic Cormorant lines reveal line-by-line (40px translateY + opacity)
- Signature path draws itself via `stroke-dasharray` over 1.6s ease-out, starting 600ms after last line lands
**3D:** ⭐ **HERO 3D — Scene B: Mouse-reactive Portrait Aura**
- Pure CSS + GSAP — no canvas needed for this one
- A radial-gradient (gold 6% → transparent 60%) mask layer pinned to portrait, follows mouse position with 250ms lerp
- A subtle dust-particle SVG layer (precomputed seeded positions, no canvas) — 40 particles max, drift upward very slowly (CSS `translateY` keyframes 60s loop, randomized start phase)
- Performance: pointer-events disabled on layer, will-change: transform
**Density:** 3 blocks (eyebrow, italic greeting, signature).

---

### S12 · The Door (Chapter IV)
**Layout:** Full-viewport 3D scene with overlaid minimal text. Section is 200vh for cinematic dwell.
**Grid:**
- Canvas fills viewport
- Overlaid content (centered, single block):
  - Eyebrow: "TRECEȚI"
  - H2 italic Cormorant 56px cream: *"Ușa se deschide o singură dată pe seară."*
  - Small Inter 16px muted: "Scroll pentru a continua"
**Typography:**
- H2 italic Cormorant 56px cream
- Single CTA-below-text amber "Solicită" button (this is the only amber CTA on the page)
**Content blocks:** 1 (the H2)
**Motion:**
- Static H2 (no scroll animation — it's literally facing you)
- 3D fog parts smoothly as user scrolls through the 200vh pin
- At 100% scroll: fog fully parted, a thin gold rule appears centered vertically (the door's frame)
**3D:** ⭐ **HERO 3D — Scene C: Fog Parting Reveal**
- Three.js vanilla, GLSL fragment shader
- Geometry: fullscreen plane, ortho camera
- Shader: FBM noise fog displaced by mouse X + scroll progress
- At scroll=0: fog density 1.0 (fully opaque, only the H2 reads through)
- At scroll=1: fog density 0.25, central gold vertical "light slit" emerges
- Behind the fog: a single static warm gradient plane (radial gold → deep), always visible at 8% intensity
- Particle layer: 200 dust motes drifting upward at random speeds, sampler-gold tinted
- This is the page's slowest, most deliberate motion — 60fps target, falls back to static JPEG on mobile
**Density:** One block on top of one 3D scene.

---

### S13 · Apply / Inquire (Chapter IV)
**Layout:** Centered. A single column, max-width 540px, set in glass card. Background = `--wol-bg-night` with a subtle gold radial glow behind the card (1500px diameter, 8% opacity).
**Grid:**
- Eyebrow: "APLICĂ"
- H2: "Spune-ne câteva lucruri." Cinzel 44px gold
- Italic Cormorant 22px muted: "Răspundem în 48 de ore."
- Form (3 fields):
  1. **Nume** (single text input)
  2. **Email** (email input)
  3. **Mesaj scurt** (textarea, 4 rows)
- Submit row: amber CTA "Trimite" + ghost "Închide" + privacy line below
**Typography:**
- Field labels: Inter 12px tracked uppercase, `--wol-text-muted`
- Field input: Cormorant Garamond 22px cream, no border except bottom-rule (`var(--wol-line-cream)` → on focus `--wol-gold`)
- Field placeholder: Inter 16px `--wol-text-muted`
- Submit: amber pill button (reuse `.wol-btn--cta`)
- Privacy line: Inter 13px `--wol-text-muted-warm`
**Content blocks:** Form only. No extra marketing copy. The page has already sold the room.
**Motion:**
- Card fades up 40px on viewport entry
- Field underlines animate width 0 → 100% on focus (200ms)
- Submit hover: arrow slides right (reused from buttons.css)
- After submit: card content morphs into confirmation "Am primit. Revin cu un răspuns." in italic Cormorant
**3D:** None.
**Density:** Form-heavy, no marketing excess.

---

### S14 · Colophon / Sigil (Chapter IV)
**Layout:** Centered, 100vh, minimal.
**Grid:**
- Top half: sigil/logo in `--wol-gold-bright`, centered, 96px tall
- Mid: address line (Cormorant italic 18px cream) — "Strada 31 August 1989, nr. 78, Chișinău"
- Hours line (Inter 14px tracked cream) — "Mar–Sâm · 16:00 — 02:00"
- Two columns below (cols 4–6, 8–10):
  - Left: "PROGRAM" — phone, email
  - Right: "URMĂREȘTE" — Instagram handle, only one
- Bottom: 1px gold hairline, tiny tracked uppercase colophon "WOLOSHIN · CHIȘINĂU · MMXXVI"
**Typography:**
- Sigil: SVG, recolored to `--wol-gold-bright`, no shadow
- All text small print — `Inter` 14px, `--wol-text-muted`
- Address: italic Cormorant 18px cream (only the slightly larger moment)
**Content blocks:** Sigil + 4 micro-blocks (address, hours, program, follow) + colophon
**Motion:** Final reveal only — words fade in stagger, 60ms each, on first scroll into viewport. No other motion.
**3D:** None. Pure ink.
**Density:** High in micro-info, low in motion.

---

## 4 · INFORMATION DENSITY STRATEGY

**The Single Rule:** Each section is one *idea*. The idea may be expressed in 1 block or 8 blocks, but never in two ideas.

| Section | Blocks | Words (target) | Motion density |
|---|---|---|---|
| S01 Pre-loader | 0 | 8 chars (counter) | Tick only |
| S02 Hero | 3 | 16 | Slow drift |
| S03 Manifesto | 1 | 60 | Pinned reveal |
| S04 The House | 3 | 50 | Parallax + marquee |
| S05 The Spaces | 5 cards | ~80 total | Pinned horizontal |
| S06 The Ritual | 7 beats | ~140 total | Vertical scroll-reveal |
| S07 The Privileges | 8 rows | ~120 total | In-place stagger |
| S08 Membership | 4 (1 huge price) | 35 | Count-up |
| S09 The Calendar | 6 events + 1 closer | ~120 total | Tick days |
| S10 The Numbers | 3 rings | 12 | Count-up |
| S11 The Host | 3 | 35 | Mouse reactive |
| S12 The Door | 1 H2 | 12 | Slowest 3D |
| S13 Apply | Form (3 fields + submit) | 25 | In-place |
| S14 Colophon | 6 micro-blocks | ~60 words total | Stagger fade only |

**Rules of density:**
- **Hero sections** (S01, S02, S12, S14): 0–3 blocks visible at once. Airiness is the brand.
- **Lists** (S06, S07, S09): each row gets at least 100px vertical space. Never 2 lines of body text per row.
- **Numeric moments** (S08, S10): numerals become the type — display weight, minimal context.
- **The pricing composition** (S08): no table, no "from/to", no FAQ inline. The number, the unit, one clarifying line, the CTA. That's it. Drawing inspiration from Aesop's product pages (one numeral + one descriptor + one button) — not from SaaS pricing tables.

---

## 5 · INFOGRAPHIC SYSTEM

**Style chosen: "Editorial Numbered Chapters" — applied consistently across S06 (Ritual), S07 (Privileges), S09 (Calendar).**

### Visual grammar
- **Numbers:** Cinzel Display 600, 32–48px depending on context. Always gold. Always two-digit formatted (01, 02… 12).
- **Labels:** Cormorant Garamond italic 500, 26–30px, cream. Title-case or sentence-case italic (Romanian typography prefers sentence-case for italic emphasis).
- **Body:** Inter 16px, muted. Max 2 lines per item. Max 14 words per line.
- **Icons:** Thin-line monochrome SVG icons, 32×32px viewBox, `stroke="currentColor"`, `stroke-width="1.5"`, `fill="none"`. Color = cream except where gold dot accent punctuates. Set: door, bottle, book, calendar, steam/leaf, monitor, champagne-glass, plane. **Custom-drawn, not stock icons.** No emoji.
- **Rules:** 1px gold or cream lines, generous `--wol-line-cream` opacity for separators. Vertical gold rule at col 6 in S06 and S09 serves as the timeline spine.

### Why this style (over alternatives)
- A "vertical timeline with editorial labels" is Aesop-meets-Aman: each beat is a chapter, not a stat.
- A "card grid with generous whitespace" was considered and rejected — too SaaS-conventional for the brand.
- An "iconographic system" alone (without numbers) was considered and rejected — would feel like a feature-list, not a membership.

### What stays consistent across S06, S07, S09
1. Cinzel numerals always.
2. Cormorant italic for *the thing itself* (ritual beat / privilege / event).
3. Inter 16px muted for the descriptor.
4. Thin-line SVG icons (only S07 uses them — they're the "object" of each privilege).
5. Vertical gold rule as timeline spine (only S06 and S09).
6. Hover affordance: rule brightens, item shifts -2px X (subtle).

---

## 6 · MICROINTERACTIONS

### Cursor
- **Default:** 4px gold dot, `--wol-gold-bright`, no border, no shadow. Always visible.
- **Hover interactive element (button / link / card):** dot expands to 36px ring (border 1.5px gold, transparent inner), interpolates via FLIP over 200ms ease-out.
- **Magnetic snap:** on `pointerdown` over a CTA, dot center pulls 6px toward the CTA's center (lerp 0.18 per frame).
- **Hidden when over text-input.**
- **Mobile:** disabled entirely below 720px width. Native cursor returns.

### Buttons
- **Primary CTA (amber `.wol-btn--cta`)**: hover lifts -3px Y + shadow bloom (reused from buttons.css). Arrow inside: translateX 0 → +6px on hover, 160ms ease.
- **Secondary gold line (`.wol-btn--gold`)**: hover border brightens (subtle → strong), 200ms ease-out glow ring (var(--wol-glow-gold)).
- **Persistent "Solicită" CTA in nav**: when page scrolls past S12 (the door), the nav CTA flips from gold-ghost to amber-fill, signifying "entry is open". Single micro-moment of conversion signaling.

### Scroll progress indicators
- **Top bar:** 1px gold hairline across the top, scaleX 0 → 1 tracking scroll progress, transform-origin left. Uses CSS `position: fixed; transform: scaleX(var(--progress))`.
- **Side dots:** 8 dots vertically aligned right edge, one per chapter. Active dot → 12px cream-filled; inactive → 6px transparent-with-1px-cream-border. Scroll-spy via IntersectionObserver sections.

### Section transitions
- **No crossfade.** The page uses clean cuts. The CSS `scroll-snap` is NOT used (jarring on luxury feel). The 3D scenes overlap via `position: fixed` canvas + `opacity` blend for the *direct* cuts to feel like film.
- **Between chapters:** a 1-line full-width marquee strip (one line of italic Cormorant, e.g. "—intra în casă—"). It runs once, slowly (18s pass), on the chapter break. Acts as a cinematic chapter card.

### Number counters
- **Privilege count (S08):** 0 → 50 000 over 1.4s, ease-expo-out. No thousand-separators while counting; final value gets the space `50 000`.
- **Day numbers (S09):** 00 → day, 600ms each, expo-out. Run when the row's timeline dot crosses 60% viewport.
- **Chapter nav dots:** no counter; presence-only.

### Kinetic text / marquee
- **S04 chapter break** (between S04 and S05): a single full-width track, 240px tall, gold italic Cormorant text, runs right→left once, over 18s. Text fades in at 30%, fades out at 100%. Loop = once per page visit, not infinite (infinite feels desperate).
- **No other kinetic text.** Restraint.

### Loading state / preloader
- **S01** IS the loading state. Counter ticks 01→50 (membership size) over 1.8s. Final state holds 600ms, then unloads. Total dwell ~2.4–3.0s.
- **Body content has `opacity: 0` until preloader unloads** — `pointer-events: none` on body during preloader. Cleaner than a spinner.

---

## 7 · 3D / WEBGL PLACEMENT

**Principle:** 3D is reserved for 2–3 *moments*, never decoration. The page is 90% typography + 10% atmosphere.

| Scene | Section | Trigger | Library | Render Strategy |
|---|---|---|---|---|
| **A · Volumetric Fog Chamber** | S02 Hero | On load, runs always | Three.js vanilla + custom GLSL | Orthographic full-screen plane, FBM noise, gold-ember volumetric tint, single light-shaft drifts over 24s |
| **B · Mouse-reactive Portrait Aura** | S11 The Host | Mouse-move over section | CSS-only (no canvas) | Radial-gradient mask follows pointer with 250ms lerp; 40 precomputed dust-particles drift upward via CSS keyframes |
| **C · Fog-Parting Door** | S12 The Door | Pinned scroll 0→1, 200vh | Three.js vanilla + custom GLSL + dust particles (Points geometry) | FBM density modulated by scroll progress; behind-fog warm radial plane revealed; gold vertical slit emerges at scroll=1 |

**Why Three.js vanilla (not R3F):** 14 sections, 3 of which are 3D. R3F bundle overhead doesn't earn its complexity at this scale. Plain Three.js + custom shader gives full control of the orthographic-camera-on-fullscreen-quad pattern, which is all we need. Bundle stays under 80kb gzipped for all 3D.

**Why no Lottie/Rive particles in scenes B/C:** particles in scene B are pure CSS keyframes — no canvas, no JS, no perf cost. Particles in scene C are 200 `Points` rendered from a `BufferGeometry` with precomputed velocities, sampled once on init. Negligible cost.

**Performance budget:**
- Each 3D canvas auto-pauses `requestAnimationFrame` when off-screen (IntersectionObserver). On pause, frame count = 0.
- Drei-equivalent helper: `useFBO` is unnecessary here. Single quad, single shader pass.
- Mobile (<720px): 3D canvases become static high-resolution JPEG poster frames with a CSS `conic-gradient` substitution for scene A and a static radial-gradient for scene C. Mouse-reactive scene B is fully disabled (no mouse).
- Reduced-motion (`prefers-reduced-motion: reduce`): all 3D scenes render their final state immediately and skip the dust/fog motion. Scroll-pinning (S05) still works (it's positional, not autonomous motion). Particle counts drop to 0.

**Stack concretely:**
- `three@^0.160` (vanilla)
- `gsap@^3.12` + ScrollTrigger (animation + pinning)
- No physics library. No Rapier. No Cannon.
- Shader source lives in `/shaders/fog-{a,b,c}.frag.glsl` — kept as separate `.glsl` files, bundled with `?raw` import in Vite, or inlined via `vite-plugin-glsl`.

---

## 8 · NAVIGATION

**Approach:** Fixed minimal top nav. Scroll-spy side dots on the right (secondary).

### Top nav (always visible)
- Height: 88px desktop, 64px mobile. Background: `transparent` → `rgba(6,8,15,0.78) backdrop-blur(20px)` after 80px scroll.
- Logo: SVG wordmark in `--wol-gold`, 32px tall. Position: left, 40px from edge.
- Center: nothing (luxury = negative space).
- Right cluster (40px from edge):
  - Text links: "Calendar" · "Spații" · "Privilegii" · "Contact" — `Inter` 14px tracked uppercase, cream, hover gold. Each is anchor `#s09`, `#s05`, `#s07`, `#s14`.
  - Persistent CTA: gold-ghost button "Solicită" → links to `#s13`. Pill, 14px text, 14px padding. On scroll past the door (S12), it swaps to amber-fill (the page's only other amber instance).
- Mobile: text links collapse into a hamburger; tapping opens a full-viewport menu (background `--wol-bg-night`, links stacked centered in Cinzel 36px gold, fade-in stagger).

### Side dots (right edge)
- Vertically centered, 18px from right.
- One dot per major scroll breakpoint: Hero · Casă · Spații · Ritual · Privilegii · Calendar · Gazdă · Ușa.
- Each dot: 6px transparent circle with 1px cream border (opacity 0.4). Active state: 10px cream-fill + label that fades in to the LEFT of dot, Cormorant italic 16px cream (e.g. "Ritualul"). Inactive labels are hidden; only the active label shows.
- On click: smooth scroll to that section.
- Hidden below 1280px width (top nav handles mobile).

### Scroll behavior of nav
- 0–80px scroll: nav fully transparent, no shadow, gold wordmark at full opacity.
- 80–800px: bg fades in to `rgba(6,8,15,0.78)`, hairline gold appears at bottom, wordmark drops to 75% size.
- 800px+: nav stays as-is, scroll-progress bar at very top becomes 1px gold filled to % scroll progress.
- Nav never disappears. Always present. Always available. The door stays lit.

---

## 9 · RESPONSIVE STRATEGY

**Philosophy:** This is a desktop-led luxury page. Mobile is not a degraded desktop; it's a *collapsed* one — fewer sections merge, type drops one step, 3D falls back to static.

| Element | Desktop (≥1280px) | Tablet (720–1279px) | Mobile (<720px) |
|---|---|---|---|
| Hero 3D | Live Three.js | Three.js with `pixelRatio: 1` | Static JPEG poster + CSS conic gradient |
| Manifesto pin | 200vh pin | 180vh pin | Removed pin, lines reveal via scroll-trigger only |
| House split | 60/40 split + parallax portrait | 60/40 split, no parallax | Stacked: image full-bleed → text below |
| The Spaces (S05) | Horizontal pin 400vh | Horizontal pin 300vh | **Vertical stack** of 5 arch cards, full-bleed |
| The Ritual timeline | Vertical timeline, cols 1–5 / 7–11 | Same, narrower padding | Single column, numbers + lines left-aligned, no spine |
| Privileges list | 4-col inner grid (num/icon/label/desc) | 2-col inner grid (num+label / icon+desc) | Stacked rows, num+label top, desc below |
| Membership composition | Numeral `clamp(140–280px)` | Numeral drops to 160px max | Numeral 120px, descriptor wraps below |
| Numbers ring counters | 3 rings horizontally | 3 rings, smaller (120px each) | Single ring stacked vertically |
| The Host | 50/50 split | 50/50 split | Stacked: portrait top, text below |
| The Door | 200vh pin, Three.js | 180vh pin, JS fog density scroll | Pinned (no 3D), static radial gradient + slow CSS scale animation |
| Apply form | Glass card 540px wide | Glass card 480px wide | Glass card full-width minus 24px |
| Top nav | Logo + 4 links + CTA | Logo + 2 links + CTA | Logo + hamburger |
| Side dots | Visible | Visible | Hidden |
| Cursor | Custom magnetic cursor | Custom magnetic cursor | **Disabled — native cursor returns** |
| Type scale | Full clamp scale | -10% on all Cinzel sizes | Mobile scale from typography.css `@media (max-width: 720px)` |
| Spacing | `padding: 8vh 6vw` per section | `padding: 6vh 5vw` | `padding: 5vh 6vw` |

**Critical mobile rules:**
- 3D never plays. Static fallback always renders cleanly.
- Hover states become tap-toggle states (CSS `:hover` is removed, `:active` or tap-state classes drive microinteractions).
- Cursor is fully removed, microinteractions triggered by tap-reveal.
- Vertical stacking of horizontal-pinned sections (S05 specifically) — never attempt horizontal scroll on mobile for content like this.

---

## 10 · TOKEN EXTENSIONS

Append the following block to `/Users/pro/HERMES_AGENT/projects/woloshin_banya/design-system/components/tokens.css` (or import as `tokens-extensions.css`):

```css
/* ─── LUXURY MOTION TOKENS (extensions) ────────────────────── */
:root {
  /* Easing */
  --wol-ease-expo-out:   cubic-bezier(0.16, 1, 0.3, 1);
  --wol-ease-expo-in:    cubic-bezier(0.7, 0, 0.84, 0);
  --wol-ease-luxury:     cubic-bezier(0.65, 0, 0.35, 1);   /* default for everything */
  --wol-ease-soft:       cubic-bezier(0.4, 0, 0.2, 1);     /* micro-interactions */

  /* Durations */
  --wol-dur-instant:   120ms;
  --wol-dur-fast:      220ms;
  --wol-dur-base:      480ms;
  --wol-dur-slow:      900ms;
  --wol-dur-epic:      1800ms;

  /* Layout grid */
  --wol-container-max:  1440px;
  --wol-container-pad:  clamp(24px, 4vw, 80px);
  --wol-col-gap:        clamp(16px, 1.6vw, 28px);

  /* Section rhythm */
  --wol-section-h:      100vh;
  --wol-section-pin:    200vh;
  --wol-section-grid-rows: 12;

  /* Display scale (extended for web beyond 1080 canvas) */
  --wol-display-mega:   clamp(80px, 9vw, 168px);
  --wol-display-h1:     clamp(56px, 6vw, 96px);
  --wol-display-h2:     clamp(40px, 4vw, 64px);
  --wol-display-h3:     clamp(28px, 2.6vw, 44px);
  --wol-italic-h:       clamp(26px, 2.6vw, 40px);

  /* Grain texture (base64 SVG) — for cinematic overlay */
  --wol-grain-svg: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='160' height='160'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.92' numOctaves='2' stitchTiles='stitch'/></filter><rect width='100%' height='100%' filter='url(%23n)' opacity='0.5'/></svg>");

  /* 3D scene tuning */
  --wol-fog-color-a:    rgba(201, 164, 74, 0.08);
  --wol-fog-color-b:    rgba(245, 166, 35, 0.04);
  --wol-fog-density:    1;
  --wol-particle-count: 200;

  /* Premium secondary accents (kept sparse) */
  --wol-velvet:         #2A1A38;   /* deep velvet, for any chromatic break */
  --wol-sand:           #C9B68C;   /* secondary gold, pale, for less important accents */
}

/* ─── REDUCED-MOTION OVERRIDE ──────────────────────────────── */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 11 · ASSEMBLY NOTES FOR BUILDERS

1. **Page wrapper**: `<div class="page">` with `background: var(--wol-bg-night)`. Sections inside, each `class="section"` with `min-height: 100vh` and `position: relative`.
2. **3D canvases**: each scene is a `<canvas class="scene-canvas scene-a|b|c">` positioned `fixed; inset: 0; pointer-events: none; z-index: var(--wol-z-bg)`. Visible only when its parent section's IntersectionObserver is intersecting.
3. **Section content**: `<div class="section__inner" style="grid-template-columns: repeat(12, 1fr); max-width: var(--wol-container-max); margin: 0 auto;">` — 12-col CSS grid. Always.
4. **Type from typography.css**: bind to CSS variables (`--wol-display-mega`, `--wol-italic-h`, etc).
5. **Romanian copy**: every word must be Romanian (with proper diacritics ă/â/î/ș/ț). All link text, headings, body, form labels. English language is reserved for visitor-facing system messages only ("Cookie preferences" etc).
6. **Custom cursor**: requires `<div class="cursor">` + `<div class="cursor-ring">` siblings appended to body, driven by `mouse` Web API (no library). Hides on `pointer-events: none` over form fields.
7. **Horizontal pin (S05)**: GSAP ScrollTrigger `pin: true; scrub: 1; snap: { snapTo: 1/4, inertia: false }`. Or use Locomotive Scroll's horizontal mode with the same scrub setting.
8. **Pre-loader (S01)**: count-up script completes when `load` event fires, then `setTimeout(unload, 600ms)`. Body class `is-loaded` toggled to fade in page content.

---

## 12 · SIGNATURE DESIGN MOVES

These five moves define Woloshin Club's visual identity. Don't negotiate on any of them:

1. **The 3D fog at the door** (S12) — the only time the user sees the world move deliberately. Everything else is restraint before this; the page *opens* with this single gesture.

2. **Editorial numbered chapters** — S06 and S07 read like a Søren Carlée or Apartamento spread. Numbers in Cinzel, italic Cormorant titles. This is how information density earns elegance.

3. **Numerals as type** — S08 (`50 000`) and S10 (50 / 12 / 1) make the number the *hero*. Aesop-product-page discipline. No "from", no comparison table, no asterisk.

4. **One persistent CTA that swaps color once** — the gold "Solicită" in the nav becomes amber after the user sees S12. This is the page's *only* insistence. Everything else is editorial.

5. **50 → 50,000** — the pre-loader counts to 50 (membership size). The membership price is 50,000. The visual rhyme carries the brand's exclusivity argument without saying it.

---

## 13 · DELIVERABLES CHECKLIST

When this design is implemented, the following must exist and be verified visually:

- [ ] Pre-loader counts 01 → 50 then unloads
- [ ] Hero 3D fog visible at low intensity, drifts over 24s
- [ ] Manifesto pin reveals line-by-line over 200vh scroll
- [ ] The Spaces horizontal pin on desktop, vertical stack on mobile
- [ ] The Ritual 7-beat vertical timeline
- [ ] The Privileges 8 rows with thin-line SVG icons
- [ ] Membership `50 000` numeral counts up, single CTA only
- [ ] Calendar events, day numbers count up
- [ ] Three ring counters stroke-dash + count-up
- [ ] Host portrait with mouse-reactive aura (CSS only)
- [ ] Door 3D fog parts over 200vh scroll, vertical gold slit emerges
- [ ] Apply form submits, confirmation text replaces
- [ ] Colophon with sigil + address + hours + IG
- [ ] Custom cursor on desktop (4px dot, ring on interactive)
- [ ] Side dots scroll-spy on right edge
- [ ] Top nav shrinks after 80px scroll
- [ ] Nav CTA flips gold→amber after S12
- [ ] Mobile fallback for all 3D scenes (static)
- [ ] Reduced-motion respected
- [ ] All copy is Romanian with proper diacritics

---

*End of specification. Hand this to engineering. Build it. Don't negotiate the restraint.*
