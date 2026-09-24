# Woloshin Club · Mobile-Cinematic Spec (v4)

**File:** `/Users/pro/Documents/Projects/Woloshin_club/v2/index.html`
**Reference audits:** `agents/final-audit.md` (desktop v3), `agents/mobile-cinematic.md` (this doc)
**Target viewport:** iPhone 14 Pro · **390 × 844 CSS px** · 3x DPR · touch
**Method:** Headless Chrome (CDP `Emulation.setDeviceMetricsOverride`) at mobile metrics, GSAP pinned timelines force-cleared so final layout is visible. Per-section screenshots: `/Users/pro/Documents/Projects/Woloshin_club/v2/audit/mobile-before/{s01..s13,scarcity-block}.png`.

---

## TL;DR

Desktop v3 was designed at 1440px and only ships 8 thin media-query overrides (`@media (max-width: 820/880/720px)`) that mostly collapse grids to 1 column. On a 390px viewport the page reads like a *cropped letterhead* — not a designed mobile experience.

**The 5 mobile problems that block launch:**

1. **Persistent horizontal overflow** — page is 432px wide on a 390px viewport (42px overflow). Caused by `.nav__cta` "SOLICITĂ O ÎNTÂLNIRE" pill clipping the right edge on every section, and the S13 submit button ("TRIMIT. APOI, TĂCERE — NOI REVENIM…") overflowing the form column.
2. **S05 horizontal-scroll track ships unchanged on mobile** — five 240px cards on a 390px screen with `overflow-x: auto` means user sees a sliver of card 2 and has to swipe a 1000px-wide track. Looks like a desktop-only pattern accidentally left on.
3. **S06 ritual grid collapsed to 1 column but the 1px gold center-divider still renders** down the entire 1900px section as a vertical hairline — looks like a bug, not design.
4. **S10 rings show counter values (50/3/2) but the gold progress arc is missing** — `data-target="314"` + GSAP scrub never fires on the touch viewport, so user sees three empty circles with numbers below.
5. **Three.js hero canvas and S12 closing canvas** don't initialize on a 390px viewport (likely the `IntersectionObserver` triggers but the WebGL shader has no width, or the canvas is `display:none` until first paint and stays 0×0). No particles, no closing fog — user just sees flat dark + text.

**The cinematic brief (Vlad's request):**

> "Сайзинг и спейсинг объектов был максимально кинематографичный"

→ Full-bleed sections, generous vertical rhythm, *very* big typography (H1s at 11–14vw on mobile), slow GSAP durations (luxury = slow), single-column narrative. Mobile is **not** "compact desktop" — it's a *portrait-mode cinema reel*.

**The 5 cinematic moves that fix the broken feel:**

1. **Section padding scales by viewport height, not fixed px** — `clamp(96px, 14vh, 160px)` for sections, `clamp(28px, 4vw, 56px)` for horizontal container. The page breathes with the device.
2. **H1 clamp values specifically tuned for mobile**: `clamp(48px, 14vw, 92px)` — at 390px viewport that's **55px** (vs current 54px which already fits but feels timid). Headlines feel *confident* not *cropped*.
3. **S05 collapses to vertical scroll-snap stack** — each card becomes a 75vh full-bleed panel, snap-y mandatory. The user's thumb scrolls, the page pins each card.
4. **S10 rings become vertical stacked stat-blocks** — number above (gold), label below (tracked uppercase), caption as italic line. Ring SVG becomes a thin gold arc *behind* the number, not a separate circle.
5. **Hero Three.js swapped for a static SVG background + CSS parallax-on-scroll** — no WebGL on mobile. A wide horizontal amber radial at 30% opacity behind the H1 + 8 sparse gold particles drifting via CSS `@keyframes`.

**Plus: font swap.** Drop Cinzel + Cormorant + EB Garamond. Bring in **Kurale** (display, Meta Ads pattern from hotels.banya.md brand) + **Plus Jakarta Sans** (body). Cyrillic + Latin subsets. One pairing, not three.

**Plus: RU/RO language toggle.** Default RU (per Vlad's preference + banya.md audience), RO secondary, auto-detect via `navigator.language`, swap via `data-ru`/`data-ro` attributes, instant — no animation.

---

## 1 · Current mobile audit (390 × 844)

### Critical (block launch)

| # | Section | Issue | Evidence |
|---|---|---|---|
| 1 | **Global nav** | `.nav__cta` ("SOLICITĂ O ÎNTÂLNIRE") pill clips the right edge on every section. The CTA is *visible* in every screenshot, bleeding past 390px. | `mobile-before/*.png` (all 14) |
| 2 | **S05 Spaces** | Horizontal-scroll-snap track ships unchanged on mobile. Five 240px cards in a 1000px row. User sees ~24% of card 2. | `mobile-before/s05.png` |
| 3 | **S06 Ritual** | 1px vertical gold center-rule still rendered down the entire 1900px section after the 2-column grid collapses to 1 column on mobile. Looks like a bug. | `mobile-before/s06.png` |
| 4 | **S08 Price** | The "MDL" currency label at the right of `50 000 MDL` is partially clipped off-screen right on 390px viewport. | `mobile-before/s08.png` |
| 5 | **S10 Rings** | Counter values render (50/3/2) but the gold progress arc inside each ring is invisible — `data-target="314"` scrub never fires on touch viewport. Three empty circles + numbers below. | `mobile-before/s10.png` |
| 6 | **S13 Form** | `.btn--amber` "TRIMIT. APOI, TĂCERE — NOI REVENIM." overflows right edge of form column. `.btn` width is not constrained on mobile. | `mobile-before/s13.png` |

### High (visual quality)

| # | Section | Issue | Evidence |
|---|---|---|---|
| 7 | **S01 Hero** | Three.js canvas appears blank on mobile — no gold particles, no fog. Hero reads as flat dark + text. | `mobile-before/s01.png` |
| 8 | **S02 Manifesto** | Pinned scrub timeline, when forced to final state, shows three lines of italic Cormorant in a 1500px section with ~600px of empty space above the text. | `mobile-before/s02.png` |
| 9 | **S03 Cifra** | Eyebrow "CIFRA · 50" sits at top of section, then the giant "50" numeral is **not visible** (digit reveal animation cleared the start state but final state didn't render). Subline visible. | `mobile-before/s03.png` |
| 10 | **S04 House** | Two-column grid correctly collapses to 1 column, but the photo placeholder is rendering as a **generic user-icon avatar SVG** (head + shoulders silhouette). Brand says "the house photo" — needs to be either the actual photo or a *designed* placeholder frame, not a default avatar. | `mobile-before/s04.png` |
| 11 | **S11 Host** | Same placeholder issue — a generic avatar SVG is rendering as the host portrait. | `mobile-before/s11.png` |
| 12 | **S11 body text** | On warm brown background, white-cream Inter body copy at 15–16px reads borderline-illigible. Contrast ≈ 4.2:1 (WCAG AA min is 4.5:1). | `mobile-before/s11.png` |
| 13 | **Footer (s14)** | After S13 form, footer is single-column (correct for mobile) but the 3-column grid stacks with awkward "Casa · Program · Urmărește" headings and small italic addresses — feels like a SaaS footer pasted into a luxury page. | (visible at scroll end) |

### Medium (rhythm)

| # | Section | Issue |
|---|---|---|
| 14 | **All sections** | `--wol-section-pad: clamp(64px, 9vh, 104px)` resolves to **75–104px on a 844px viewport** — too tight for "cinematic" rhythm. Cinematic = 14vh feels right (118px @ 844). |
| 15 | **All H1s** | `--wol-display-mega: clamp(54px, 6.5vw, 92px)` resolves to **54px** on mobile — small for a hero. Should be 12–14vw on mobile = 47–55px on smallest, 80–90px on tablet portrait. |
| 16 | **Hero CTA stack** | "Programează o conversație" amber + "Cum funcționează, mai exact" ghost stack vertically (correct) but the ghost link has no visible affordance on dark bg — only underlined link. |
| 17 | **Footer copyright** | Tracked uppercase + small print — corporate feel in a handcrafted page. |
| 18 | **S12 closing** | "TRECEȚI" eyebrow + giant H1 + form-like CTA "Solicită" — competes with S13 which has the *real* form. Redundant on mobile. |

---

## 2 · Section-by-section mobile spec

All values below are **mobile-first** (default = ≤720px). Tablet portrait (721–1024px) uses the `md:` override. Desktop (1025px+) inherits the existing v3 styles.

Cinematic rhythm baseline:
```css
--wol-section-pad-y:  clamp(96px, 14vh, 160px);   /* was clamp(64px,9vh,104px) */
--wol-container-pad:  clamp(28px, 6vw, 80px);     /* was clamp(24px,4vw,80px) */
--wol-display-mega:   clamp(54px, 13vw, 96px);    /* H1 hero — was clamp(54px,6.5vw,92px) */
--wol-display-h1:     clamp(40px, 9.5vw, 72px);   /* section H1 — was clamp(38px,5.5vw,72px) */
--wol-display-h2:     clamp(32px, 7.5vw, 56px);   /* card / subhead */
--wol-display-h3:     clamp(26px, 6vw, 42px);     /* card title */
--wol-body:           clamp(17px, 4.2vw, 20px);   /* was 16px */
--wol-eyebrow-size:   clamp(11px, 2.8vw, 14px);   /* tracked uppercase */
--wol-tap-min:        56px;                       /* WCAG AAA tap target */
```

Font stack refresh:
```css
--wol-font-display: 'Kurale', 'Times New Roman', serif;
--wol-font-italic:  'Plus Jakarta Sans', -apple-system, sans-serif;
--wol-font-body:    'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, sans-serif;
--wol-font-meta:    'Kurale', 'Times New Roman', serif;  /* alias */
```
- `Kurale` weight 400 (default), 700 (eyebrow / strong).
- `Plus Jakarta Sans` weight 300 (body), 400 (UI), 500 (button), 600 (eyebrow / strong).
- *No* italic from Plus Jakarta. For italic subheads, use Kurale italic (`font-style: italic`) OR drop italics on mobile (preferred for performance + clarity).

### Global mobile overrides (`@media (max-width: 720px)`)

```css
@media (max-width: 720px) {

  /* ── Nav: hide CTA pill, show hamburger + lang toggle ─────── */
  .nav__cta   { display: none; }                      /* replaces the bleeding CTA */
  .nav__links { display: none; }                      /* already hidden < 820 */
  .nav__lang  { display: inline-flex; }               /* NEW — RU | RO toggle */
  .nav { height: 64px; padding: 0 20px; }

  /* ── Global: kill horizontal overflow at the root ──────────── */
  html, body { overflow-x: hidden; }
  .container { padding-left: 20px; padding-right: 20px; max-width: 100%; }

  /* ── Section rhythm: cinematic ─────────────────────────────── */
  .section { padding: var(--wol-section-pad-y) var(--wol-container-pad); }

  /* ── Buttons: full-width on mobile, generous tap height ────── */
  .btn { min-height: 56px; padding: 18px 28px; }
  .btn--amber, .btn--ghost { width: 100%; justify-content: center; }

  /* ── Type scale ────────────────────────────────────────────── */
  h1, .h1, .hero-headline { font-size: var(--wol-display-mega); }
  h2, .h2 { font-size: var(--wol-display-h1); }
  h3, .h3 { font-size: var(--wol-display-h3); }
  body, p { font-size: var(--wol-body); line-height: 1.7; }

  /* ── Three.js: hide canvas, show static SVG fallback ──────── */
  #s01__canvas, #s12__canvas { display: none !important; }
  .hero__svg-fallback, .closing__svg-fallback { display: block; }

  /* ── Kill the desktop center rule on S06 ───────────────────── */
  .ritual__rule, .ritual > .ritual__divider { display: none; }
}
```

---

### S01 · Hero (Threshold)

**Desktop reference:** amber `Woloshin Club nu se cumpără. Se poartă.` epigraph + 130px H1 + sub + 2 CTAs + meta + scroll cue + Three.js particles.
**Mobile cinematic intent:** *full-bleed portrait cinema poster.* Single column. Big H1. Three.js disabled, replaced by a wide horizontal amber radial at 30% opacity + 8 sparse gold particles drifting via CSS keyframes.

```html
<section id="s01" class="section section--hero" aria-label="Threshold">
  <div class="hero__svg-fallback" aria-hidden="true">
    <!-- horizontal amber horizon at 30% viewport height -->
    <svg viewBox="0 0 390 600" preserveAspectRatio="xMidYMid slice">
      <defs>
        <radialGradient id="horizon" cx="50%" cy="30%" r="60%">
          <stop offset="0%"  stop-color="#E8C492" stop-opacity="0.22"/>
          <stop offset="60%" stop-color="#C9A24A" stop-opacity="0.08"/>
          <stop offset="100%" stop-color="#06080F" stop-opacity="0"/>
        </radialGradient>
      </defs>
      <rect width="100%" height="100%" fill="url(#horizon)"/>
      <!-- 8 gold particles -->
      <circle class="particle" cx="40"  cy="180" r="1.5" fill="#C9A24A"/>
      <circle class="particle" cx="120" cy="320" r="1"   fill="#E8C492"/>
      <circle class="particle" cx="220" cy="140" r="1.2" fill="#C9A24A"/>
      <circle class="particle" cx="320" cy="280" r="1"   fill="#E8C492"/>
      <circle class="particle" cx="60"  cy="420" r="1.5" fill="#C9A24A"/>
      <circle class="particle" cx="280" cy="450" r="1"   fill="#E8C492"/>
      <circle class="particle" cx="180" cy="500" r="1.2" fill="#C9A24A"/>
      <circle class="particle" cx="350" cy="380" r="1"   fill="#E8C492"/>
    </svg>
  </div>

  <div class="container hero__inner">
    <p class="hero-epigraph" data-ru="Woloshin Club не продаётся. Носят."
                              data-ro="Woloshin Club nu se cumpără. Se poartă.">
      Woloshin Club nu se cumpără. Se poartă.
    </p>

    <div class="hero-body">
      <p class="hero-eyebrow" data-ru="WOLOSHIN · CLUB — ИЗДАНИЕ I"
                              data-ro="WOLOSHIN · CLUB — EDIȚIA I">
        WOLOSHIN · CLUB — EDIȚIA I
      </p>

      <h1 class="hero-headline" data-ru="Пятьдесят членов. Ни одного лишнего."
                                data-ro="Cincizeci de membri. Niciunul în plus.">
        Cincizeci de membri. Niciunul în plus.
      </h1>

      <p class="hero-sub" data-ru="Это не абонемент. Это место за столом — у Woloshin Banya, у леса. Кто сейчас решает, кто войдёт следующим."
                         data-ro="Nu este un abonament. Este un loc la masă — la Woloshin Banya, lângă pădure. Cine este acum decide cine mai intră.">
        Nu este un abonament. Este un loc la masă…
      </p>

      <div class="hero-cta-row">
        <a href="#s13" class="btn btn--amber" data-ru="Назначить разговор" data-ro="Programează o conversație">
          Programează o conversație
        </a>
        <a href="#s02" class="btn btn--ghost" data-ru="Как именно это работает" data-ro="Cum funcționează, mai exact">
          Cum funcționează, mai exact
        </a>
      </div>
    </div>

    <p class="hero-meta" data-ru="Издание I · Кишинёв · Woloshin Banya"
                        data-ro="Ediția I · Chișinău · Woloshin Banya">
      Ediția I · Chișinău · Woloshin Banya
    </p>
  </div>
</section>
```

**Mobile CSS:**
```css
@media (max-width: 720px) {
  .section--hero { min-height: 100vh; min-height: 100svh; padding-top: 88px; padding-bottom: 60px; }
  .hero__svg-fallback {
    position: absolute; inset: 0;
    pointer-events: none; z-index: 0;
    opacity: 0.9;
  }
  .hero__svg-fallback .particle {
    animation: drift 18s ease-in-out infinite;
  }
  .hero__svg-fallback .particle:nth-child(odd) { animation-duration: 24s; }
  @keyframes drift {
    0%, 100% { transform: translate(0, 0); }
    50%      { transform: translate(8px, -14px); }
  }
  .hero__inner { position: relative; z-index: 1; }

  .hero-epigraph {
    font-family: var(--wol-font-display);  /* Kurale */
    font-style: italic; font-weight: 400;
    font-size: clamp(18px, 4.5vw, 22px);
    line-height: 1.4; color: var(--wol-text-cream);
    text-align: left;
    margin: 0 0 80px 0;
    max-width: 22ch;
  }
  .hero-eyebrow {
    font-family: var(--wol-font-body);
    font-size: var(--wol-eyebrow-size);
    letter-spacing: 0.32em;
    color: var(--wol-text-muted);
    margin-bottom: 24px;
  }
  .hero-headline {
    font-family: var(--wol-font-display);
    font-weight: 400;            /* Kurale looks best at 400 */
    font-size: var(--wol-display-mega);
    line-height: 0.96;
    letter-spacing: -0.01em;
    color: var(--wol-text-cream);
    text-transform: none;         /* Kurale is already display; don't uppercase */
    margin: 0 0 48px 0;
    text-wrap: balance;
  }
  .hero-sub {
    font-family: var(--wol-font-body);
    font-size: var(--wol-body);
    font-weight: 300;
    line-height: 1.7;
    color: var(--wol-text-muted);
    margin: 0 0 56px 0;
    max-width: 32ch;
  }
  .hero-cta-row { display: flex; flex-direction: column; gap: 14px; margin-bottom: 80px; }
  .hero-meta {
    font-family: var(--wol-font-body);
    font-size: 11px;
    letter-spacing: 0.3em;
    color: var(--wol-text-muted);
    text-transform: uppercase;
  }
}
```

**GSAP mobile:**
```js
// Kill pinned hero scroll on mobile — single full-screen intro only
mm.add('(max-width: 720px)', () => {
  const tl = gsap.timeline({ defaults: { ease: 'expo.out' } });
  tl.from('.hero-epigraph',  { autoAlpha: 0, y: 16, duration: 1.4 }, 0.2);
  tl.from('.hero-eyebrow',   { autoAlpha: 0, y: 8,  duration: 0.8 }, 0.4);
  tl.from('.hero-headline',  { autoAlpha: 0, y: 30, duration: 1.6 }, 0.6);
  tl.from('.hero-sub',       { autoAlpha: 0, y: 16, duration: 1.0 }, 1.4);
  tl.from('.hero-cta-row',   { autoAlpha: 0, y: 12, duration: 1.0 }, 1.6);
  tl.from('.hero-meta',      { autoAlpha: 0, duration: 0.8 },       1.9);
  // NO pin, NO scrub. One intro on load.
});
mm.add('(min-width: 721px)', () => {
  // desktop pinned hero stays as-is
});
```

---

### S02 · Manifesto

**Desktop reference:** pinned scrub timeline reveals 3 italic lines sentence-by-sentence over 180% scroll.
**Mobile cinematic intent:** *full-bleed portrait, deep navy, single italic line per viewport*, slow opacity reveal on scroll-snap. NO pin (pin breaks on mobile touch).

```css
@media (max-width: 720px) {
  .section--manifesto {
    min-height: 100vh;
    display: flex; flex-direction: column;
    justify-content: center;
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
  }
  .manifesto {
    text-align: left;          /* left-align kills the desktop's center-rag */
    max-width: 28ch;
    margin: 0;
  }
  .manifesto__line {
    font-family: var(--wol-font-display);  /* Kurale */
    font-style: italic; font-weight: 400;
    font-size: clamp(28px, 7.5vw, 42px);
    line-height: 1.25;
    color: var(--wol-text-cream);
    margin: 0 0 48px 0;
    opacity: 0; transform: translateY(20px);
  }
  .manifesto__line:last-child { margin-bottom: 0; }
}
```

**GSAP mobile:** keep the per-line reveal but drop the pin & scrub:
```js
mm.add('(max-width: 720px)', () => {
  gsap.utils.toArray('.manifesto__line').forEach((line, i) => {
    gsap.fromTo(line,
      { autoAlpha: 0, y: 30 },
      { autoAlpha: 1, y: 0, duration: 1.4, ease: 'expo.out',
        scrollTrigger: { trigger: line, start: 'top 85%' } });
  });
});
```

---

### S03 · Cifra · 50

**Desktop reference:** eyebrow "CIFRA · 50" + giant Cinzel "50" + tracked "42 LOCURI OCUPATE · 8 RĂMASE" + italic legend.
**Mobile cinematic intent:** the giant "50" *fills* the viewport. No fixed pixel size — `clamp(180px, 48vw, 320px)`. Single column, centered. The 50-dot row lives HERE on mobile too (was misplaced in scarcity-block on desktop — see `final-audit.md`).

```css
@media (max-width: 720px) {
  .section--cifra {
    min-height: 90vh;
    display: flex; flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
  }
  .giant-number {
    font-family: var(--wol-font-display);  /* Kurale */
    font-weight: 400;
    font-size: clamp(220px, 56vw, 360px);
    line-height: 0.86;
    color: var(--wol-text-gold);
    margin: 24px 0;
    letter-spacing: -0.02em;
  }
  .scarcity-grid__sub {
    font-family: var(--wol-font-body);
    font-size: var(--wol-eyebrow-size);
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--wol-text-muted);
    margin: 0 0 56px 0;
  }
  .scarcity-grid__legend {
    font-family: var(--wol-font-display);
    font-style: italic; font-weight: 400;
    font-size: clamp(20px, 5vw, 28px);
    color: var(--wol-text-muted-warm);
    max-width: 26ch;
    margin: 0;
  }

  /* Move the 50-dot row here on mobile (was in scarcity-block) */
  .scarcity-dots-row {
    display: flex; flex-wrap: wrap;
    justify-content: center;
    gap: 6px;
    max-width: 340px;
    margin: 56px auto 0;
  }
  .scarcity-dots-row .dot { width: 12px; height: 12px; }
}
```

**JS move:** clone the `<svg>` from `.scarcity-block` into `#s03` on `matchMedia('(max-width: 720px)')` add, hide original.

---

### S04 · The House

**Desktop reference:** warm brown bg, 2-column (image / text), big Cinzel H1, body copy, city list.
**Mobile cinematic intent:** full-bleed warm brown. Image placeholder at top (60vh tall), text below. NO city list (drop it on mobile — was illegible at 14px even on desktop).

```css
@media (max-width: 720px) {
  .section--warm.section--house { padding: 0; }
  .house {
    display: grid; grid-template-columns: 1fr;
    gap: 0;
  }
  .house__visual {
    min-height: 60vh;
    background:
      linear-gradient(180deg, transparent 60%, var(--wol-bg-warm) 100%),
      radial-gradient(ellipse at 50% 30%, rgba(245, 166, 35, 0.18), transparent 60%),
      var(--wol-bg-card);
    border: 1px solid var(--wol-border-subtle);
    border-radius: 0;
    margin: 0;
  }
  /* When real photo lands, drop the radial gradient above. */
  .house__copy {
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
    text-align: left;
  }
  .house__copy h2 {
    font-size: var(--wol-display-h1);
    margin-bottom: 32px;
  }
  .house__copy .italic-lead {
    font-size: clamp(20px, 5vw, 28px);
    margin-bottom: 24px;
  }
  .house__copy .body { font-size: var(--wol-body); }
  .house__copy .cities { display: none; }   /* hide illegible city list on mobile */
}
```

---

### S05 · The Spaces (THE BIG ONE)

**Desktop reference:** horizontal scroll-snap track of 5 arched cards (240–340px wide each).
**Mobile cinematic intent:** **vertical scroll-snap-y stack** — 5 full-bleed cards, each `min-height: 75vh`, snap-y mandatory. The user's thumb scrolls; each card pins in place. Tap-target = the whole card.

```css
@media (max-width: 720px) {
  .section--spaces {
    /* Remove horizontal padding so cards are truly full-bleed */
    padding-left: 0; padding-right: 0;
  }
  .s05__head {
    padding: var(--wol-section-pad-y) var(--wol-container-pad) 40px;
  }
  .s05__head h2 { font-size: var(--wol-display-h1); margin: 12px 0 0; }

  /* THE FIX: vertical scroll-snap stack */
  .spaces-track {
    display: flex; flex-direction: column;
    overflow-y: auto;
    overflow-x: hidden;
    scroll-snap-type: y mandatory;
    gap: 16px;
    height: 75vh;                  /* each card takes 75vh */
    padding: 0 20px 20px;
  }
  .space-card {
    flex: 0 0 75vh;                /* each card fills the visible area */
    width: 100%;
    aspect-ratio: auto;            /* kill the desktop 3:4 */
    border-radius: 28px;           /* less arch on mobile */
    scroll-snap-align: start;
    display: flex; flex-direction: column;
    justify-content: flex-end;     /* content at bottom */
    padding: 32px;
    background:
      linear-gradient(180deg, transparent 30%, rgba(6, 8, 15, 0.92) 100%),
      radial-gradient(ellipse at 50% 25%, rgba(201, 164, 74, 0.22), transparent 65%),
      var(--wol-bg-deep);
  }
  .space-card__num {
    font-size: clamp(48px, 12vw, 72px);
    line-height: 1;
    margin-bottom: 16px;
  }
  .space-card__title {
    font-family: var(--wol-font-display);  /* Kurale */
    font-weight: 400;
    font-size: clamp(32px, 8vw, 44px);
    color: var(--wol-text-cream);
    margin: 0 0 12px 0;
  }
  .space-card__caption {
    font-size: var(--wol-body);
    color: var(--wol-text-muted);
    max-width: 28ch;
  }

  /* Counter (1 of 5) shown at top-right of each card */
  .space-card__counter {
    position: absolute; top: 20px; right: 24px;
    font-family: var(--wol-font-body);
    font-size: 11px;
    letter-spacing: 0.3em;
    color: var(--wol-text-muted);
    text-transform: uppercase;
  }
}
```

**GSAP mobile:** swap the card stagger for an in-place reveal per card:
```js
mm.add('(max-width: 720px)', () => {
  gsap.utils.toArray('.space-card').forEach((card, i) => {
    gsap.from(card.querySelectorAll('.space-card__num, .space-card__title, .space-card__caption'),
      { autoAlpha: 0, y: 20, duration: 1.0, stagger: 0.1, ease: 'expo.out',
        scrollTrigger: { trigger: card, start: 'top 75%' } });
  });
});
```

---

### S06 · The Ritual

**Desktop reference:** 2-column list of 7 numbered beats with vertical gold center-rule + paragraph epigraph.
**Mobile cinematic intent:** single column, 7 beats stacked. **Kill the center rule.** Number above, title, body. Hairline divider between beats.

```css
@media (max-width: 720px) {
  .section--ritual {
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
  }
  .ritual {
    display: flex; flex-direction: column;
    gap: 0;                          /* divider handles spacing */
    margin: 56px 0 0;
  }
  .ritual__col { display: contents; } /* flatten the desktop columns */
  .ritual__rule, .ritual__divider { display: none !important; }

  .ritual__beat {
    display: grid;
    grid-template-columns: 64px 1fr;
    gap: 20px;
    padding: 32px 0;
    border-bottom: 1px solid var(--wol-border-subtle);
    align-items: start;
  }
  .ritual__beat:first-child { border-top: 1px solid var(--wol-border-subtle); }
  .ritual__num {
    font-family: var(--wol-font-display);
    font-weight: 400;
    font-size: clamp(36px, 9vw, 48px);
    color: var(--wol-gold);
    line-height: 1;
    margin: 0;
  }
  .ritual__title {
    font-family: var(--wol-font-display);
    font-weight: 400;
    font-size: clamp(22px, 5.5vw, 28px);
    color: var(--wol-text-cream);
    margin: 0 0 8px 0;
  }
  .ritual__body {
    font-size: var(--wol-body);
    color: var(--wol-text-muted);
    line-height: 1.65;
  }
}
```

---

### S07 · The Privileges

**Desktop reference:** 2-column list of 8 privilege rows with Cinzel titles + Inter bodies + line-drawn SVG icons.
**Mobile cinematic intent:** single column, full-bleed rows, generous vertical rhythm. Icons left, text right.

```css
@media (max-width: 720px) {
  .privileges {
    display: flex; flex-direction: column;
    gap: 0;
    margin-top: 56px;
  }
  .privilege-row {
    display: grid;
    grid-template-columns: 48px 1fr;
    gap: 20px;
    padding: 28px 0;
    border-bottom: 1px solid var(--wol-border-subtle);
  }
  .privilege-row:first-child { border-top: 1px solid var(--wol-border-subtle); }
  .privilege-row__icon {
    width: 32px; height: 32px;
    align-self: start;
  }
  .privilege-row h3 {
    font-family: var(--wol-font-display);
    font-weight: 400;
    font-size: clamp(22px, 5.5vw, 28px);
    color: var(--wol-text-cream);
    margin: 0 0 8px 0;
  }
  .privilege-row p {
    font-size: var(--wol-body);
    color: var(--wol-text-muted);
    line-height: 1.65;
  }
}
```

---

### Scarcity block (between S07 and S08)

**Desktop reference:** eyebrow + H1 "8 LOCURI RĂMASE" + 50-dot SVG.
**Mobile cinematic intent:** tight, full-bleed, gold glow behind dots, dots larger (16px each, 4px gap), centered.

```css
@media (max-width: 720px) {
  .scarcity-block {
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
    text-align: center;
  }
  .scarcity-block__title {
    font-family: var(--wol-font-display);
    font-weight: 400;
    font-size: clamp(36px, 9vw, 56px);
    color: var(--wol-text-cream);
    margin: 16px 0 12px;
  }
  .scarcity-block__sub {
    font-size: var(--wol-body);
    color: var(--wol-text-muted-warm);
    margin-bottom: 48px;
  }
  .scarcity-block__svg {
    width: 100%; max-width: 340px;
    height: auto;
  }
  /* The desktop SVG has 720 viewBox with 26px steps; scale to viewport */
  .scarcity-block__svg .dot { r: 6; }   /* bump from 5 */
  .scarcity-block__svg .dot--hollow { stroke-width: 1.2; }
}
```

---

### S08 · The Door (Price)

**Desktop reference:** eyebrow + H1 "CEEA CE 50 000 MDL DESCHIDE" + giant "50 000" + tracked subline + amber CTA.
**Mobile cinematic intent:** the "50 000" is the most important number on the page on mobile too. **Move "MDL" to the line below** ("50 000" / "lei moldovenești" on two lines), so it never clips right.

```css
@media (max-width: 720px) {
  .section--door {
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
    text-align: center;
  }
  .price-numeral {
    display: flex; flex-direction: column;
    align-items: center;
    gap: 8px;
    margin: 40px 0 16px;
    font-family: var(--wol-font-display);
    font-weight: 400;
    font-size: clamp(96px, 26vw, 160px);
    line-height: 0.92;
    color: var(--wol-text-cream);
    letter-spacing: -0.02em;
  }
  .price-currency {
    font-family: var(--wol-font-body);
    font-weight: 500;
    font-size: var(--wol-eyebrow-size);
    letter-spacing: 0.4em;
    color: var(--wol-text-gold);
    text-transform: uppercase;
    margin-top: 4px;
  }
  .price-digit-row {
    display: inline-flex;
    gap: 0;
  }
  /* soft amber radial behind price — visible on mobile */
  .section--door::before {
    content: "";
    position: absolute; inset: 30% 0 0 0;
    background: radial-gradient(ellipse at 50% 50%, rgba(245, 166, 35, 0.18), transparent 65%);
    pointer-events: none;
    z-index: 0;
  }
}
```

**JS swap:** on mobile, restructure the `.price-numeral` markup so "MDL" becomes a separate `<span class="price-currency">` below the digits, not an inline sibling.

---

### S09 · The Calendar

**Desktop reference:** 3-column row (date · title+body · pill) for 2 events (NOIEMBRIE 14 / 28).
**Mobile cinematic intent:** single column, big date above, title, body, then pill — stacked vertically per event. 2 events become 2 large cards.

```css
@media (max-width: 720px) {
  .section--calendar {
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
  }
  .event-row {
    display: flex; flex-direction: column;
    gap: 16px;
    padding: 32px 0;
    border-bottom: 1px solid var(--wol-border-subtle);
  }
  .event-row:first-child { border-top: 1px solid var(--wol-border-subtle); }
  .event-row__date {
    font-family: var(--wol-font-display);
    font-weight: 400;
    font-size: clamp(48px, 12vw, 64px);
    color: var(--wol-text-cream);
    line-height: 1;
    letter-spacing: -0.01em;
  }
  .event-row__month {
    font-family: var(--wol-font-body);
    font-size: var(--wol-eyebrow-size);
    letter-spacing: 0.3em;
    color: var(--wol-text-muted);
    text-transform: uppercase;
    display: block; margin-top: 8px;
  }
  .event-row h3 {
    font-family: var(--wol-font-display);
    font-style: italic; font-weight: 400;
    font-size: clamp(24px, 6vw, 32px);
    color: var(--wol-text-cream);
    margin: 16px 0 8px;
  }
  .event-row p {
    font-size: var(--wol-body);
    color: var(--wol-text-muted);
  }
  .event-row__pill {
    align-self: flex-start;
    margin-top: 8px;
    padding: 8px 16px;
    font-size: 11px;
    letter-spacing: 0.2em;
  }
}
```

---

### S10 · The Numbers (Rings)

**Desktop reference:** 3-column grid of 3 rings with Cinzel value inside circle + label + caption.
**Mobile cinematic intent:** **vertical stack**, each stat becomes a *horizontal card*: thin gold arc *behind* the number on the left, label + caption on the right. The "circle" is decorative now, not a progress meter.

```css
@media (max-width: 720px) {
  .section--numbers {
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
  }
  .rings {
    display: flex; flex-direction: column;
    gap: 0;
    max-width: 100%;
    margin: 56px 0 0;
  }
  .ring {
    display: grid;
    grid-template-columns: 96px 1fr;   /* arc left, text right */
    gap: 24px;
    align-items: center;
    padding: 32px 0;
    border-bottom: 1px solid var(--wol-border-subtle);
  }
  .ring:first-child { border-top: 1px solid var(--wol-border-subtle); }
  .ring svg {
    width: 96px; height: 96px;
    overflow: visible;
  }
  .ring svg .ring__progress {
    transform-origin: center;
    transform: rotate(-90deg);
    stroke-dasharray: 314;
    stroke-dashoffset: 0;          /* mobile: show full arc immediately */
    transition: stroke-dashoffset 1.6s var(--wol-ease-out);
  }
  .ring__value {
    font-family: var(--wol-font-display);
    font-weight: 400;
    font-size: clamp(56px, 14vw, 72px);
    line-height: 1;
    color: var(--wol-gold-bright);
    text-align: left;
  }
  .ring__label {
    font-family: var(--wol-font-body);
    font-size: var(--wol-eyebrow-size);
    letter-spacing: 0.3em;
    color: var(--wol-text-muted);
    text-transform: uppercase;
    margin-top: 8px;
    text-align: left;
  }
  .ring__caption {
    font-family: var(--wol-font-display);
    font-style: italic; font-weight: 400;
    font-size: clamp(16px, 4vw, 20px);
    color: var(--wol-text-muted-warm);
    text-align: left;
    margin-top: 8px;
  }
  /* Hide the SVG center value, since the value is in the text column now */
  /* (but keep the SVG as a decorative arc — reposition it) */
  .ring svg {
    grid-row: span 1;
  }
}
```

**JS swap:** on mobile, the value should live in a sibling `<span class="ring__value">` *next* to the SVG (not inside the SVG). Restructure markup in `mm.add('(max-width: 720px)')`.

**GSAP mobile:** kill the stroke-dashoffset scrub — just fade the ring in.
```js
mm.add('(max-width: 720px)', () => {
  gsap.utils.toArray('.ring').forEach((ring, i) => {
    gsap.from(ring, {
      autoAlpha: 0, y: 24, duration: 1.0, ease: 'expo.out',
      scrollTrigger: { trigger: ring, start: 'top 80%' }
    });
  });
});
```

---

### S11 · The Host

**Desktop reference:** warm brown bg, 2-column (portrait / text), italic Cormorant headline + Inter body.
**Mobile cinematic intent:** full-bleed warm brown. Portrait at top (60vh, with the actual portrait OR a *designed* placeholder — NOT the default user-icon avatar). Text below. Body color contrast bumped to WCAG AA.

```css
@media (max-width: 720px) {
  .section--host { padding: 0; }
  .host {
    display: flex; flex-direction: column;
    gap: 0;
  }
  .host__portrait {
    width: 100%;
    min-height: 60vh;
    background:
      radial-gradient(ellipse at 50% 35%, rgba(245, 166, 35, 0.20), transparent 65%),
      var(--wol-bg-card);
    border: 1px solid var(--wol-border-subtle);
    border-radius: 0;
    overflow: hidden;
    display: flex; align-items: flex-end; justify-content: center;
    padding-bottom: 20px;
  }
  /* When real photo: <img src="rares.jpg"> fills container */
  .host__portrait img { width: 100%; height: 100%; object-fit: cover; }

  .host__caption {
    position: relative; top: auto; left: auto;
    font-family: var(--wol-font-display);
    font-style: italic;
    font-size: 14px;
    color: var(--wol-text-muted-warm);
    text-align: center;
    margin-top: 16px;
  }

  .host__copy {
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
    text-align: left;
  }
  .host__copy .italic-lead {
    font-family: var(--wol-font-display);
    font-style: italic; font-weight: 400;
    font-size: clamp(28px, 7vw, 40px);
    line-height: 1.25;
    color: var(--wol-text-cream);
    margin: 16px 0 32px;
  }
  /* Bump body contrast for WCAG AA */
  .host__copy p {
    font-family: var(--wol-font-body);
    font-size: var(--wol-body);
    line-height: 1.7;
    color: var(--wol-text-cream);          /* was muted — too low contrast */
    opacity: 0.85;
  }
}
```

**CRITICAL:** Replace the `<svg>` avatar with the actual photo of Rareș, or with a *designed* placeholder frame (gold border + caption "Rareș · soon" on warm brown) — NOT a default user-icon avatar.

---

### S12 · The Closing

**Desktop reference:** eyebrow + giant italic H1 + small form-like CTA "Solicită". Three.js closing fog canvas behind.
**Mobile cinematic intent:** **drop this section on mobile.** The real form lives in S13, so S12 is redundant. Replace with a thin closing line + amber radial background.

```css
@media (max-width: 720px) {
  .section--closing {
    min-height: 60vh;
    display: flex; flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
    position: relative;
  }
  .section--closing::before {
    content: "";
    position: absolute; inset: 30% 0 0 0;
    background: radial-gradient(ellipse at 50% 50%, rgba(245, 166, 35, 0.20), transparent 60%);
    pointer-events: none;
  }
  .section--closing .eyebrow { font-size: var(--wol-eyebrow-size); }
  .section--closing h2 {
    font-family: var(--wol-font-display);
    font-style: italic; font-weight: 400;
    font-size: clamp(28px, 7vw, 40px);
    color: var(--wol-text-cream);
    margin: 16px 0 24px;
    max-width: 22ch;
  }
  .section--closing p { display: none; }   /* hide "Scroll pentru a continua" */
  .section--closing .btn { width: 100%; }
}
```

---

### S13 · The Form (Apply)

**Desktop reference:** single column form (email / phone / message) + amber CTA + privacy + footer below.
**Mobile cinematic intent:** full-width inputs, generous tap height (56px), stacked, single button. Footer below collapses cleanly.

```css
@media (max-width: 720px) {
  .section--form {
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
  }
  .form-wrap h2 {
    font-family: var(--wol-font-display);
    font-weight: 400;
    font-size: var(--wol-display-h1);
    color: var(--wol-text-cream);
    margin: 16px 0;
  }
  .form { gap: 28px; }
  .field { display: flex; flex-direction: column; gap: 10px; }
  .field__label {
    font-family: var(--wol-font-body);
    font-size: 11px;
    letter-spacing: 0.3em;
    color: var(--wol-text-muted);
    text-transform: uppercase;
  }
  .field input, .field textarea {
    width: 100%;
    min-height: 56px;
    padding: 18px 20px;
    background: transparent;
    border: 0;
    border-bottom: 1px solid var(--wol-border-mid);
    font-family: var(--wol-font-body);
    font-size: var(--wol-body);
    color: var(--wol-text-cream);
    border-radius: 0;
  }
  .field input::placeholder, .field textarea::placeholder {
    color: var(--wol-text-muted);
    font-family: var(--wol-font-display);
    font-style: italic;
  }
  .field input:focus, .field textarea:focus {
    outline: none;
    border-bottom-color: var(--wol-gold);
  }
  .field textarea { min-height: 120px; resize: vertical; }

  /* The big fix: full-width CTA */
  .btn--amber { width: 100%; justify-content: center; min-height: 56px; }

  .form__privacy {
    font-family: var(--wol-font-body);
    font-size: 12px;
    color: var(--wol-text-muted);
    text-align: center;
    margin-top: 16px;
  }
}
```

**Footer (s14) on mobile:**
```css
@media (max-width: 720px) {
  .footer {
    padding: var(--wol-section-pad-y) var(--wol-container-pad);
    text-align: left;
  }
  .footer-sigil {
    font-family: var(--wol-font-display);
    font-weight: 400;
    font-size: clamp(28px, 7vw, 36px);
    color: var(--wol-gold);
    letter-spacing: 0.02em;
    margin: 0 0 8px;
  }
  .footer-grid {
    display: flex; flex-direction: column;
    gap: 32px;
    margin: 48px 0 32px;
  }
  .footer-col h3 {
    font-family: var(--wol-font-body);
    font-size: 11px;
    letter-spacing: 0.3em;
    color: var(--wol-text-gold);
    text-transform: uppercase;
    margin-bottom: 12px;
  }
  .footer-col p, .footer-col a {
    font-family: var(--wol-font-display);
    font-style: italic; font-weight: 400;
    font-size: 17px;
    color: var(--wol-text-cream);
    line-height: 1.6;
    text-decoration: none;
    display: block;
    margin: 4px 0;
  }
  .footer-meta {
    font-family: var(--wol-font-body);
    font-size: 12px;
    color: var(--wol-text-muted);
    line-height: 1.6;
    text-transform: none;          /* sentence case, not tracked uppercase */
    letter-spacing: 0;
  }
  .footer-meta small { display: block; margin-top: 8px; }
}
```

---

## 3 · Cinema principles applied

Seven rules the mobile v4 follows:

1. **Vertical-first rhythm.** Every section is a *scene* with its own full-height breath. Section padding scales with `vh` not `px`. Result: scrolling feels like turning pages of a coffee-table book, not a Twitter feed.

2. **Headlines are the loudest thing.** H1 = `clamp(54px, 13vw, 96px)` — at 390px viewport that's 54px minimum, scaling to 92px+ on small tablets. Headlines should *fill the column width*. Body text is `clamp(17px, 4.2vw, 20px)` — smaller relative to H1 than the desktop (where body is 16px and H1 is 72px, ratio 1:4.5; mobile ratio 1:3.2 with 17/54). Mobile reads as a *poster*.

3. **One voice per text register.**
   - Display (H1, H2, zone titles, numbers, prices): **Kurale** 400 — serif, calm, ornamental without shouting.
   - UI (body, buttons, eyebrows, form labels): **Plus Jakarta Sans** 300–600 — sans, geometric, modern.
   - Italic (sub-headlines, captions, legends): **Kurale italic** — pairs naturally with its upright sibling.
   - No more Cinzel/Cormorant/EB Garamond/Inter mix. One pairing, fewer weight shifts, faster visual scan.

4. **Slow motion.** GSAP intro durations extended (`expo.out` ease, 1.4–1.6s on H1 reveal). Pinned scroll-scrub timelines are *killed* on mobile (they break touch); replaced with `start: 'top 75%'` one-shot reveals. The page still animates, but the *camera moves slowly* — luxury = slow.

5. **Generous whitespace around focal points.** Hero CTA stack has 80px between subtitle and button. Form CTA has 32px between field and button. Section transitions have 96–160px of breathing space. Whitespace is not "wasted" — it's the silence between sentences.

6. **Single-column narrative.** Every 2-column desktop layout (house, ritual, privileges, calendar, rings) collapses to 1 column on mobile. Hairline gold dividers between rows replace the desktop's center rule. The page reads *top to bottom*, no scanning back-and-forth.

7. **Full-bleed scenes, not cropped cards.** No max-widths on mobile. The deep navy of S02 fills 100vw. The warm brown of S04 fills 100vw. The amber glow behind S08 fills 100vw. The page is a *sequence of full-screen paintings*, not a deck of slides on a card table.

---

## 4 · Language toggle architecture

**Default: RU** (Vlad's preference + banya.md audience). Toggle to RO via nav button.

### Markup pattern

Every translatable string is wrapped in **both** `data-ru` and `data-ro` attributes. The visible text comes from whichever attribute matches the active language. JS swaps `innerText` on toggle.

```html
<!-- Pattern 1: text on element -->
<h1 data-ru="Пятьдесят членов. Ни одного лишнего."
    data-ro="Cincizeci de membri. Niciunul în plus.">
  Cincizeci de membri. Niciunul în plus.
</h1>

<!-- Pattern 2: nested element -->
<a href="#s13" class="btn btn--amber"
   data-ru="Назначить разговор"
   data-ro="Programează o conversație">
  Programează o conversație
</a>

<!-- Pattern 3: dynamic value (placeholder, aria-label) -->
<input type="email" placeholder="name@domain.md"
       data-ru-placeholder="имя@домен.md"
       data-ro-placeholder="nume@domeniu.md">
```

### Nav toggle UI

```html
<div class="nav__lang" role="group" aria-label="Limba / Язык">
  <button class="nav__lang-btn is-active" data-lang="ru" aria-pressed="true">RU</button>
  <span class="nav__lang-sep" aria-hidden="true">|</span>
  <button class="nav__lang-btn" data-lang="ro" aria-pressed="false">RO</button>
</div>
```

```css
.nav__lang {
  display: none;               /* shown only ≤ 720px */
  align-items: center;
  gap: 8px;
  margin-left: auto;
}
.nav__lang-btn {
  background: transparent; border: 0;
  font-family: var(--wol-font-body);
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.2em;
  color: var(--wol-text-muted);
  padding: 8px 4px;
  cursor: pointer;
  text-transform: uppercase;
}
.nav__lang-btn.is-active {
  color: var(--wol-text-gold);
  border-bottom: 1px solid var(--wol-gold);
}
.nav__lang-sep {
  color: var(--wol-text-muted);
  font-size: 12px;
  opacity: 0.4;
}

@media (max-width: 720px) {
  .nav__lang { display: inline-flex; }
}
```

### JS — `initLangToggle()`

```js
function initLangToggle() {
  const STORAGE_KEY = 'woloshin-lang';
  const supported = ['ru', 'ro'];

  function detect() {
    const saved = localStorage.getItem(STORAGE_KEY);
    if (saved && supported.includes(saved)) return saved;
    const nav = (navigator.language || 'ru').slice(0, 2).toLowerCase();
    return supported.includes(nav) ? nav : 'ru';   // default RU
  }

  let current = detect();

  function apply(lang) {
    current = lang;
    document.documentElement.lang = lang === 'ro' ? 'ro' : 'ru';
    localStorage.setItem(STORAGE_KEY, lang);

    // Swap element text
    document.querySelectorAll('[data-ru][data-ro]').forEach(el => {
      const next = el.getAttribute(`data-${lang}`);
      if (next != null) el.textContent = next;
    });

    // Swap placeholders
    document.querySelectorAll(`[data-${lang}-placeholder]`).forEach(el => {
      el.placeholder = el.getAttribute(`data-${lang}-placeholder`);
    });

    // Update toggle buttons
    document.querySelectorAll('.nav__lang-btn').forEach(btn => {
      const active = btn.dataset.lang === lang;
      btn.classList.toggle('is-active', active);
      btn.setAttribute('aria-pressed', String(active));
    });
  }

  document.querySelectorAll('.nav__lang-btn').forEach(btn => {
    btn.addEventListener('click', () => apply(btn.dataset.lang));
  });

  apply(current);   // initial render (in case nav button needs to highlight)
}
```

**Initial render on page load** should run *before* paint to avoid FOUC of the wrong language. Either:
- Use `<html lang="ru">` + inline `<script>` at top of body that calls `apply(detect())` synchronously, OR
- Server-side render the chosen language as the default text (best for SEO + no flash).

**No animation on swap** — instant text replacement is more luxurious than a crossfade (which can feel "web app-y").

---

## 5 · Font swap — full CSS snippet

### HTML — replace existing Google Fonts link

**Old:**
```html
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;500;600;700&family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,400;1,500;1,600&family=Inter:wght@300;400;500;600&family=EB+Garamond:ital,wght@0,400;1,400&display=swap" rel="stylesheet">
```

**New:**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Kurale&family=Plus+Jakarta+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&display=swap&subset=latin,latin-ext,cyrillic" rel="stylesheet">
```

### CSS — `:root` variable overrides

**Add to existing `:root` block:**
```css
:root {
  /* ── Шрифты (refresh v4: Kurale + Plus Jakarta Sans) ─── */
  --wol-font-display: 'Kurale', 'Times New Roman', serif;
  --wol-font-italic:  'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, sans-serif;
  --wol-font-body:    'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, sans-serif;
  --wol-font-meta:    'Kurale', 'Times New Roman', serif;

  /* Cinzel → Kurale (display) */
  /* Cormorant Garamond → Plus Jakarta Sans (no italics on body) */
  /* EB Garamond → Kurale italic (for subheads only) */
  /* Inter → Plus Jakarta Sans (body/UI) */
}
```

### CSS — global font rules

```css
html, body {
  font-family: var(--wol-font-body);
  font-weight: 400;
  font-size: 16px;
  line-height: 1.6;
  color: var(--wol-text-cream);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
}

h1, h2, h3, h4, .hero-headline, .giant-number, .price-numeral {
  font-family: var(--wol-font-display);  /* Kurale */
  font-weight: 400;                       /* Kurale's natural weight */
  letter-spacing: 0;
  text-wrap: balance;
}

.italic-lead, blockquote em, .host__copy .italic-lead {
  font-family: var(--wol-font-display);   /* Kurale italic */
  font-style: italic;
  font-weight: 400;
}

/* Override Cormorant Italic classes if any JS-driven code references them */
.cormorant, .font-italic {
  font-family: var(--wol-font-display);
  font-style: italic;
}
```

### Why this pairing works

- **Kurale** is a single-weight serif (Latin + Cyrillic) designed for headlines — it's the brand font on banya.md Meta Ads. Distinctly humanist, slightly geometric, calm. 400 weight reads as elegant, 700 weight reads as confident.
- **Plus Jakarta Sans** is a geometric sans (Latin + Latin Ext + Cyrillic on Google Fonts) with 8 weights (200–800, italic 400). Geometric enough to feel modern, friendly enough to feel handcrafted. The `wght@300..700` range gives plenty of UI hierarchy without loading 8 webfont files.
- **Together:** Kurale for "the rooms", Plus Jakarta Sans for "the doors". One serif, one sans. No third voice.

### What gets dropped

- ❌ **Cinzel** — ornamental Roman caps, too "Roman colonnade" for a banya. Replaced by Kurale's calmer serif.
- ❌ **Cormorant Garamond** — beautiful but heavy on Cyrillic subsets, slow to load. Replaced by Kurale italic.
- ❌ **EB Garamond** — only used for italic subheads; Kurale italic does the same job with one less font family.
- ❌ **Inter** — reads SaaS, not Aman. Replaced by Plus Jakarta Sans.

---

## 6 · Implementation order (priority fixes for v4)

### Phase 1 — Ship blockers (1–2 hours)

1. **Fix horizontal overflow at root** — add `html, body { overflow-x: hidden; }` + `.nav__cta { display: none; }` on mobile + `.btn--amber { width: 100%; }` on mobile. Solves 3 of the 6 critical issues in one CSS pass.
2. **Add the language toggle scaffold** — empty nav__lang div + JS module + `[data-ru][data-ro]` attribute contract for *only* the nav, hero headline, hero sub, hero CTAs, and S08 / S13 copy. Seed with RO text already in the page; add RU translations. Pages still default to RO; user can flip to RU via the toggle.
3. **Kill the S06 center divider** on mobile — one line: `.ritual__divider { display: none; }`.

### Phase 2 — Visual quality (3–4 hours)

4. **S05 → vertical scroll-snap stack** — biggest single visual win. 30 lines of CSS + 10 lines of GSAP.
5. **S10 → stat-block stack** — kill the progress arcs on mobile, restructure as 2-column rows.
6. **S08 → MDL on separate line** — restructure the price-numeral markup so "MDL" never clips right.
7. **S09 calendar → stacked rows** — same single-column treatment as S06/S07.

### Phase 3 — Typography refresh (2–3 hours)

8. **Font swap** — replace Google Fonts link + update `:root` variables. Run through all sections adjusting `font-family` overrides if anything breaks.
9. **Tune clamp values** for H1/H2/H3/body on mobile (the values in section 2 above).
10. **Replace S04 + S11 placeholder SVGs** with either real photos or designed "coming soon" frames (NOT default user-icon avatars).

### Phase 4 — Polish (2–3 hours)

11. **Disable Three.js on mobile** + ship the SVG fallback for hero + closing.
12. **Move 50-dot row from scarcity-block to S03** on mobile (or duplicate).
13. **Section padding scale-by-vh** — replace `--wol-section-pad` with `clamp(96px, 14vh, 160px)`.
14. **Footer sentence-case** — drop tracked uppercase on copyright.
15. **Drop S12 "Solicită" button** on mobile — the form is in S13, redundant.
16. **S11 body contrast** — bump from `--wol-text-muted` to `--wol-text-cream @ 85%` for WCAG AA.

### Phase 5 — RU translations (concurrent)

17. **Russian copy** for all sections, all eyebrows, all CTAs, all form labels. This is the bulk of the content work. Hire a Russian native copywriter who knows luxury hospitality tone (Aman / Soho House voice).
18. **Update form placeholders** — `data-ru-placeholder` / `data-ro-placeholder` on email, phone, message fields.

### Phase 6 — Validation (1 hour)

19. Re-run mobile audit at 390 × 844 with this spec applied — verify all 6 critical issues resolved.
20. Test at 360 × 780 (Galaxy S8) and 430 × 932 (iPhone 15 Pro Max) for edge cases.
21. Lighthouse mobile perf — should be ≥ 90 with fonts preloaded + Three.js disabled.

**Total estimate:** 8–12 hours of focused implementation work + 4–6 hours of Russian translation.

---

## 7 · Verification checklist

Before declaring v4 shipped, confirm:

- [ ] **No horizontal scroll** at 360 / 390 / 430 / 480 widths (`document.documentElement.scrollWidth === document.documentElement.clientWidth`).
- [ ] **Nav CTA hidden on mobile**, replaced by `RU | RO` toggle in top-right.
- [ ] **S05 is a vertical scroll-snap-y stack** — swipe up to move between cards.
- [ ] **S06 has no vertical center line** on mobile.
- [ ] **S08 "50 000" + "MDL" never clip** — "MDL" sits on its own line below the digits.
- [ ] **S10 rings render the arc OR are restyled as stat blocks** (the desktop arcs may stay if they fire reliably on touch — test before deciding).
- [ ] **S11 / S04 placeholders are NOT default user-icon avatars** — either real photos or designed frames.
- [ ] **All form inputs have `min-height: 56px`** on mobile.
- [ ] **All CTAs are full-width on mobile** (`.btn { width: 100%; }`).
- [ ] **Font swap loads** — `getComputedStyle(document.body).fontFamily` includes `'Plus Jakarta Sans'`; H1 includes `'Kurale'`.
- [ ] **Language toggle works** — click `RO` button, all text swaps to Romanian; click `RU`, all text swaps back. No FOUC on load.
- [ ] **No Three.js canvas visible** on mobile (or it gracefully degrades).
- [ ] **Russian translations present** on all sections — copy reads naturally, not machine-translated.

---

## 8 · Files referenced

- `/Users/pro/Documents/Projects/Woloshin_club/v2/index.html` — the v3 source (3002 lines)
- `/Users/pro/Documents/Projects/Woloshin_club/v2/agents/final-audit.md` — desktop audit (v3 review)
- `/Users/pro/Documents/Projects/Woloshin_club/v2/audit/mobile-before/*.png` — 14 section screenshots at 390 × 844 (this audit)
- `/Users/pro/HERMES_AGENT/projects/woloshin_banya/design-system/woloshin.css` — brand tokens (canonical Kurale/Plus Jakarta Sans pairing reference)

---

**Spec written by:** Mobile-Cinematic Designer (delegated subagent)
**For:** Vlad · Woloshin Club · Ediția I — 2026
**Default language on launch:** RU (with RO toggle)
