# ARCHITECTURE.md — Technical Deep-Dive

For AI agents and engineers who need to understand the system, not just use it.

---

## High-level

Single-file HTML landing page (`index.html`, ~141 KB, ~3,420 lines). Loads 4 Google Fonts via CDN, runs GSAP + Three.js inline, applies 8 SVG backgrounds. No build step. No external assets except fonts.

---

## Page structure

```
<html lang="ru-RU">
  <head>
    <meta charset + viewport + theme-color + description + title>
    <link rel="preconnect" Google Fonts>
    <link Google Fonts URL: Kurale + Plus Jakarta Sans + cyrillic subset>
    <style>
      /* Design tokens (mirror of woloshin.css) */
      /* Section styles (S01-S14) */
      /* Mobile @media (max-width: 720px) */
      /* prefers-reduced-motion override */
    </style>
  </head>
  <body>
    <header> Site nav: logo, menu, lang-toggle RU|RO, CTA </header>
    <main>
      <section#s01> Hero: Three.js canvas + headline + epigraph + CTA </section>
      <section#s02> Manifesto: 4 pinned lines </section>
      <section#s03> The Number: giant "50" + 50-dot scarcity SVG </section>
      <section#s04> The House: editorial paragraph + placeholder frame </section>
      <section#s05> The Spaces: horizontal-scroll 5 cards </section>
      <section#s06> The Ritual: 7-beat timeline </section>
      <section#s07> The Privileges: 8 numbered editorial items </section>
      <section#s08> The Door: 50 000 MDL single numeral + subline </section>
      <section#s09> The Calendar: 3 events/year </section>
      <section#s10> The Numbers: 3 Aston-Martin-style rings </section>
      <section#s11> The Host: abstract silhouette + signature </section>
      <section#s12> The Closing: fog-parting Three.js scene + CTA </section>
      <section#s13> The Form: editorial 2-field form </section>
    </main>
    <footer#s14> Colophon </footer>
    <script>
      /* GSAP + ScrollTrigger master timeline */
      /* Three.js Scene A (Threshold fog + particles) */
      /* Three.js Scene C (Closing fog parting) */
      /* IntersectionObserver pause/resume */
      /* Language toggle (setLang + localStorage) */
      /* Counters (initial render + GSAP scroll-trigger ease) */
      /* prefers-reduced-motion fallback (st.disable) */
    </script>
  </body>
</html>
```

---

## Design tokens (CSS custom properties)

The `:root` block in `<style>` mirrors `woloshin.css` (do NOT diverge without Vlad approval):

```css
:root {
  /* Backgrounds */
  --wol-bg-night:    #06080F;
  --wol-bg-deep:     #0F1B2D;
  --wol-bg-warm:     #1A1410;
  --wol-bg-card:     #10203A;

  /* Text */
  --wol-text-cream:      #F5E9D3;
  --wol-text-white:      #FFFFFF;
  --wol-text-muted:      #A0A8B8;
  --wol-text-muted-warm: #9A8870;
  --wol-text-gold:       #E8C492;

  /* Accents */
  --wol-gold:        #C9A24A;
  --wol-gold-2:      #D4A93B;
  --wol-gold-bright: #F2A900;
  --wol-amber:       #F5A623;
  --wol-amber-deep:  #D68A1F;
  --wol-ember:       #FF8A3D;
  --wol-ice:         #AEC8E6;

  /* Borders */
  --wol-border-subtle: rgba(201, 164, 74, 0.18);
  --wol-border-mid:    rgba(201, 164, 74, 0.30);
  --wol-border-strong: rgba(201, 164, 74, 0.45);
  --wol-line-cream:    rgba(245, 233, 211, 0.14);

  /* Fonts */
  --wol-font-display: 'Kurale', serif;
  --wol-font-serif:   'Kurale', serif;
  --wol-font-body:    'Plus Jakarta Sans', sans-serif;
  --wol-font-script:  'Kurale', serif;
  --wol-font-italic:  'Kurale', serif;  /* used for italic subheads */

  /* Spacing rhythm */
  --wol-section-pad: clamp(48px, 7vh, 80px);
  --wol-section-pad-mobile: clamp(40px, 6vh, 64px);
  --wol-container-pad: 32px;
  --wol-container-max: 1240px;
}
```

---

## Language toggle architecture

### HTML contract

Every translatable text node has BOTH `data-ru` and `data-ro` attributes. The visible `textContent` between tags is the RUSSIAN default (what shows before JS loads).

```html
<h1 data-ru="Пятьдесят членов. Ни одного сверх." data-ro="Cincizeci de membri. Niciunul în plus.">
  Пятьдесят членов. Ни одного сверх.
</h1>
```

For input placeholders:
```html
<input data-ru-placeholder="Ваше имя" data-ro-placeholder="Numele dumneavoastră" placeholder="Ваше имя">
```

### JS implementation

```js
const setLang = (lang) => {
  localStorage.setItem('wol-lang', lang);
  document.documentElement.lang = lang === 'ru' ? 'ru-RU' : 'ro-RO';

  // Swap text nodes
  document.querySelectorAll('[data-ru][data-ro]').forEach(el => {
    el.textContent = el.getAttribute(`data-${lang}`);
  });

  // Swap placeholders
  document.querySelectorAll(`[data-${lang}-placeholder]`).forEach(el => {
    el.placeholder = el.getAttribute(`data-${lang}-placeholder`);
  });

  // Update toggle visual state
  document.querySelectorAll('.lang-toggle__btn').forEach(btn => {
    btn.classList.toggle('active', btn.dataset.lang === lang);
  });

  // Refresh ScrollTrigger so animations re-trigger on the now-Russian text
  if (window.ScrollTrigger) window.ScrollTrigger.refresh();
};

// Init: localStorage > navigator.language > RU default
const initLang = () => {
  const stored = localStorage.getItem('wol-lang');
  const detected = navigator.language?.startsWith('ru') ? 'ru' : 'ro';
  setLang(stored || detected);
};
```

### Pre-paint FOUC prevention

To avoid the flash of unstyled Russian when the user's preference is Romanian, run `initLang()` in a `<script>` block at the END of `<body>`, BEFORE the closing tag, with no `defer` or `async`.

---

## Motion system

### Easing vocabulary (5 eases)

| Name | Use case | Easing string | Duration range |
|------|----------|---------------|----------------|
| `revelation` | Dramatic entrance (hero headline, big reveals) | `expo.out` or `power3.out` | 0.6–1.2 s |
| `settle` | Soft landing (text in, lists) | `sine.out` | 0.4–0.8 s |
| `drift` | Parallax / scroll-linked movement | `none` (linear) | continuous |
| `magnetic` | Hover micro-interactions | `power3.out` | 0.2–0.4 s |
| `ritual` | Slow ceremonial (closing scene, fog parting) | `expo.inOut` | 1.2–2.5 s |

### GSAP architecture

- **One master timeline** for the whole page, OR **per-section timelines** triggered by ScrollTrigger
- **Hero intro**: separate `intro` timeline (plays once on load, NOT scrub-bound)
- **Scroll-bound sections**: ScrollTrigger with `scrub: 0.4` for smooth follow
- **Counters**: initial textContent set in HTML (so they're visible without JS), GSAP animates from 0→N on scroll with `fromTo` for ease-on-scroll

### Three.js scenes

#### Scene A — Threshold (Hero)

```js
// Renderer: shared across scenes
const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
renderer.setPixelRatio(Math.min(1.5, devicePixelRatio)); // DPR cap

// Scene
const scene = new THREE.Scene();
scene.fog = new THREE.FogExp2(0x0F1B2D, 0.04);

// Camera
const camera = new THREE.PerspectiveCamera(60, w/h, 0.1, 100);
camera.position.z = 5;

// 240 particles, additive blending, gold tint
const particles = new THREE.Points(geometry, material);

// Mouse parallax
let mouseX = 0, mouseY = 0;
container.addEventListener('mousemove', (e) => {
  mouseX = (e.clientX / window.innerWidth - 0.5) * 0.5;
  mouseY = (e.clientY / window.innerHeight - 0.5) * 0.5;
});
// On animate(): camera.position.x += (mouseX - camera.position.x) * 0.05;

// Animation loop (PAUSED off-screen via IntersectionObserver)
const animate = () => {
  requestAnimationFrame(animate);
  // update particles
  // lerp camera to mouse
  renderer.render(scene, camera);
};
```

#### Scene C — Closing (Fog Parting)

- Single plane with custom depth-shader (`uDensity` uniform)
- Fog density scrubs from high → low as user scrolls into the section
- Underneath: closing CTA text reveals

#### Performance & lifecycle

- Single renderer instance, scene swap via `renderer.render(scene, camera)`
- All scenes paused off-screen via IntersectionObserver
- Dispose geometries/materials when removing a scene
- `prefers-reduced-motion`: skip Three.js entirely, show static SVG fallback

---

## Background SVG system

8 inline SVG files in `backgrounds/`. Each is a vector atmospheric gradient with grain (`<feTurbulence>`). Applied to sections via `.section-with-bg::before` pseudo-element:

```css
.section-with-bg { position: relative; isolation: isolate; }
.section-with-bg::before {
  content: "";
  position: absolute;
  inset: 0;
  background-image: url("backgrounds/S02-manifesto-bg.svg");
  background-size: cover;
  background-position: center;
  opacity: 0.55;  /* tuned per section */
  z-index: -1;
  pointer-events: none;
}
```

Per-section opacity (current values, tunable):
| Section | SVG | Opacity |
|---------|-----|---------|
| S02 | S02-manifesto-bg.svg | 0.50 |
| S03 | S03-number-bg.svg | 0.40 |
| S04 | S04-house-bg.svg | 0.55 |
| S05 | S05-spaces-bg.svg | 0.50 |
| S06 | S06-ritual-bg.svg | 0.45 |
| S07 | S07-privileges-bg.svg | 0.50 |
| S12 | S12-closing-bg.svg | 0.60 |

S01 has Three.js fog instead of SVG. S08-S11, S13, S14 are content-dense so no bg.

---

## Accessibility

- **Semantic HTML**: `<section>`, `<article>`, `<nav>`, `<main>`, `<header>`, `<footer>`
- **ARIA**: `aria-label` on rings (e.g. `aria-label="50 de membri"`), `aria-hidden="true"` on decorative SVGs, `aria-live="polite"` on form success states
- **Focus states**: `:focus-visible` outlines using `var(--wol-gold)`
- **Reduced motion**: full `@media (prefers-reduced-motion: reduce)` block — disables GSAP scrub, kills Three.js, shows counters in final state immediately, no fog-parting animation
- **Keyboard navigation**: all CTAs and form fields are real `<button>`/`<input>` elements (not `<div>` styled to look interactive)

---

## Mobile strategy

- **Breakpoint**: `@media (max-width: 720px)`
- **Three.js**: disabled, replaced by static SVG bg with CSS-drifting particles (keyframe animation on `::after` pseudo)
- **S05 horizontal-scroll → vertical scroll-snap-y stack**
- **H1 size**: `clamp(54px, 13vw, 96px)`
- **Section padding**: `clamp(40px, 6vh, 64px)`
- **Tap targets**: min 56px height on all interactive elements
- **Host portrait**: 220×280px (vs desktop 360×460px)
- **S05 numbers**: smaller (clamp(56px, 7vw, 110px)) — Vlad's feedback

---

## Performance budget

- Total HTML weight: ~141 KB (gzip ~30 KB)
- Three.js: ~50 MB GPU memory cap (with 240 particles + 1 simple scene)
- DPR cap: 1.5 (renderer.setPixelRatio)
- GSAP timelines: paused off-screen, killed when section leaves view
- Lazy Three.js init: only after first user interaction OR after 2s timeout
- Single CDN: Google Fonts (with `display=swap` for FOUT prevention)

---

## Browser support

Last 2 versions of Chrome, Safari, Firefox, Edge. No IE11. No legacy Edge. Tested at:
- Desktop: 1440×900, 1920×1080, 2560×1440
- Tablet: 1024×768 (falls back to desktop layout)
- Mobile: 390×844 (iPhone 14 Pro), 414×896 (iPhone 11), 360×640 (Android mid)

---

## Future improvements (not in current scope)

1. Replace SVG backgrounds with real PNG/AVIF from Imagen 4 (requires gflow auth — see HANDOFF.md)
2. Add WebP/AVIF hero video instead of Three.js particles
3. i18n: add English and Ukrainian (current: RU + RO only)
4. Form backend: currently mailto, replace with proper form handler
5. Analytics: Plausible or Umami for traffic
6. A/B test hero headline variants (3 alternatives in copy-ru.md)
7. SSR/SSG for SEO (currently single HTML, Google sees full content but no meta OG tags)

---

## Files of note

- `/Users/pro/HERMES_AGENT/projects/woloshin_banya/design-system/woloshin.css` — brand tokens (canonical source)
- `agents/copy-ru.md` — Russian copy register (the source of truth for Russian voice)
- `agents/copy/out.md` — Romanian copy register
- `agents/motion/out.md` — full motion specification
- `agents/design/out.md` — section-by-section design spec
