# Woloshin Club — Motion System Spec

> **Brand premise.** Premium membership club in Moldova. 50 members. 50,000 MDL entry. Romanian. Feel: Aman / Soho House — quiet, expensive, not loud. The motion language is **slow, deliberate, ceremonial**. Every ease should feel like a butler opening a door, not a banner ad.
>
> **Palette reference.** `--wol-bg-night #06080F`, `--wol-bg-deep #0F1B2D`, `--wol-text-cream #F5E9D3`, `--wol-text-gold #E8C492`, `--wol-gold #C9A24A`, `--wol-amber #F5A623`. (See `/Users/pro/HERMES_AGENT/projects/woloshin_banya/design-system/components/tokens.css`.)
>
> **GSAP contract.** All timelines register on `window.__timelines` keyed by `data-composition-id` on the composition root. Timelines start **paused**; the engine seeks them. camelCase only (`xPercent`, `autoAlpha`, `scaleX`). `data-composition-id` is the single key the engine expects; if you build sub-animations outside a composition, register them under a different id and let the page orchestrate.

---

## 1. Architecture overview

**Decision: per-section ScrollTrigger timelines, NOT one master timeline.**

We use **`gsap.matchMedia()` + independent section timelines**, each driven by its own `ScrollTrigger`. Rationale:

1. **Independent scrub control.** Different sections need different scrub durations — the hero "Threshold" needs `scrub: 1.2` for buttery drag, the CTA "Closing" needs `scrub: false` with a hard `toggleActions`. A master timeline forces one scrub rate.
2. **Lazy init & disposal.** Each section's timeline is created inside a `ScrollTrigger.create({ onEnter })` closure and killed on `onLeave` (reverse direction). A master timeline cannot be partially killed without losing every sibling.
3. **No re-entrancy bugs.** ScrollTrigger's `pin` + `scrub` interacts badly with one master TL that crosses multiple pinned sections; the official GSAP guidance is "one ScrollTrigger per pinned scene."
4. **HyperFrames composability.** Each section is a stand-alone unit that can be opened in the HyperFrames preview individually (one composition root, one timeline key). This matches the registry contract.

```js
// motion/registry.js
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

export const sections = {
  threshold:  { id: "section-threshold",  trigger: "#hero",      factory: buildThreshold  },
  membership: { id: "section-membership", trigger: "#stats",     factory: buildMembership },
  ritual:     { id: "section-ritual",     trigger: "#ritual",    factory: buildRitual     },
  personal:   { id: "section-personal",   trigger: "#personal",  factory: buildPersonal   },
  closing:    { id: "section-closing",    trigger: "#cta",       factory: buildClosing    },
};

export function initMotion() {
  const mm = gsap.matchMedia();
  Object.values(sections).forEach((s) => {
    mm.add(s.trigger, (ctx) => {
      const tl = gsap.timeline({ paused: true, defaults: { ease: "expo.out" } });
      s.factory(tl, ctx);
      const st = ScrollTrigger.create({
        trigger: s.trigger,
        start: "top 80%",
        end: "bottom 20%",
        scrub: 1.2,
        anticipatePin: 1,
        animation: tl,
      });
      ctx.add(() => st.kill()); // auto-cleanup when matchMedia reverts
      return s.trigger;
    });
  });
  return mm;
}
```

**ScrollTrigger defaults used site-wide.**

| Option | Value | Why |
| --- | --- | --- |
| `scrub` | `1.2` (or `false` for CTA) | Smooth drag-follow without lag or jitter. |
| `pin` | `true` on Hero, Ritual, Closing | Each pinned section needs `pinSpacing: true` and a section taller than the viewport. |
| `pinSpacing` | `true` | Avoid layout shift on the page flow. |
| `anticipatePin` | `1` | One frame of lookahead — eliminates pin flicker on fast scroll. |
| `snap` | `{ snapTo: 1/4, duration: 0.4, ease: "power2.inOut" }` on Ritual only | Cinematic but discrete "pages" of scroll. |
| `markers` | `false` in prod | Never leave markers on. |
| `toggleActions` | `"play none none reverse"` on CTA | Hard in/out, no scrub. |

**Three.js renderer is shared across scenes.** One canvas, one `WebGLRenderer`, three scene roots mounted/unmounted by an `IntersectionObserver`. See §7 / §8.

---

## 2. Easing vocabulary

Five named eases. Every tween on the page should pick one and stick to it — easiness is the most-read luxury signal. **No `power1.out` defaults.** Durations are deliberately long (1.0s+); instant is cheap.

| Token | GSAP ease | Duration | When to use |
| --- | --- | --- | --- |
| `revelation` | `expo.out` (custom `1.2` overshoot via `back.inOut(1.05)`) | 1.2 – 1.8 s | Entrance of a headline, a number, a hero object — the moment something is *revealed*. |
| `settle` | `sine.out` | 0.9 – 1.2 s | A block lands into place — paragraph copy settling under a title, a card finishing its scale. |
| `drift` | `none` (linear) | varies | Parallax. Scrubbed timelines only. Linear reads as parallax; any ease reads as "tweening." |
| `magnetic` | `power3.out` with `back.out(1.2)` overshoot on the final 5 % | 0.5 – 0.7 s | Hover states on CTA, nav links, cards. Has a touch of life without being cartoony. |
| `ritual` | `expo.inOut` | 1.5 – 2.4 s | Section-to-section transitions, fog parting, slow color washes. Ceremonial. |

```js
// motion/eases.js
import { gsap } from "gsap";

// Register custom eases so authors can write ease: "revelation" etc.
const custom = {
  revelation: "expo.out",
  settle:     "sine.out",
  drift:      "none",
  magnetic:   "power3.out",
  ritual:     "expo.inOut",
};

export function ease(name) {
  return custom[name] ?? name;
}

// Backstop helper — keeps durations in the luxury band.
export function LUX_DUR(token) {
  return {
    revelation: 1.4,
    settle:     1.0,
    magnetic:   0.55,
    ritual:     1.8,
  }[token] ?? 1.0;
}
```

**Anti-patterns.** No `bounce`, no `elastic`, no `power1.in` on entrances, no `circ.out`. These read as playful/cartoony and break the Aman mood.

---

## 3. Text-reveal patterns

Three patterns are wired up. Pick per section by feel — never mix two within the same heading.

### 3.1 Split words (default for everything ≥ 12 words)

Each `<span class="word">` is wrapped in a `<span class="word-wrap">` with `overflow:hidden`; the word itself starts at `yPercent: 110` and eases in with `revelation`. Stagger 0.06s reads as a quiet wave, not a typewriter.

```js
function splitWords(el) {
  const text = el.textContent;
  const words = text.split(/\s+/);
  el.innerHTML = words
    .map((w) => `<span class="word-wrap"><span class="word">${w}</span></span>`)
    .join(" ");
  return el.querySelectorAll(".word-wrap > .word");
}

// Usage inside a section timeline:
const words = splitWords(headlineEl);
tl.from(words, {
  yPercent: 110,
  autoAlpha: 0,
  duration: LUX_DUR("revelation"),
  ease: ease("revelation"),
  stagger: { each: 0.06, from: "start" },
}, 0);
```

### 3.2 Mask reveal (for short display titles — "Woloshin Club")

A single `.clip` element with `clipPath: inset(0 100% 0 0)` is animated to `inset(0 0% 0 0)`. One motion. Quiet.

```js
tl.from(".clip", {
  clipPath: "inset(0 100% 0 0)",
  duration: 1.6,
  ease: ease("ritual"),
}, 0);
```

### 3.3 Blur up (for paragraph body copy)

`filter: blur(12px)` + `opacity: 0` to `blur(0)` + `opacity: 1`. Reads as "coming into focus." Reserved for paragraphs, never headlines.

```js
tl.from(".lead p", {
  filter: "blur(12px)",
  autoAlpha: 0,
  y: 18,
  duration: 1.1,
  ease: ease("settle"),
  stagger: 0.12,
}, 0.4);
```

### Out of scope (explicit non-picks)
- **Scramble.** Too Matrix. Wrong era for an Aman reference.
- **Kinetic headline (chars from random).** Reads as agency reel, not luxury.

---

## 4. Number counter system

The three hero stats: **50** (members), **3** (ritualuri / an), **10%** (discount parteneri). All animate `0 → N` over 1.2 s on `ScrollTrigger` enter, with `snap: 1` for integers.

```js
// motion/counter.js
import { gsap } from "gsap";

export function animateCounter(selector, endValue, opts = {}) {
  const {
    duration = 1.2,
    ease = "expo.out",
    format = (n) => Math.round(n).toString(),
    suffix = "",
  } = opts;

  const el = document.querySelector(selector);
  if (!el) return;
  const obj = { v: 0 };

  gsap.to(obj, {
    v: endValue,
    duration,
    ease,
    snap: { v: 1 },
    onUpdate: () => { el.textContent = format(obj.v) + suffix; },
    scrollTrigger: {
      trigger: el,
      start: "top 85%",
      toggleActions: "play none none none",
    },
  });
}

// init
animateCounter("#stat-members", 50);
animateCounter("#stat-events",  3);
animateCounter("#stat-discount", 10, { suffix: "%" });
```

**Why per-element ScrollTrigger and not a section timeline.** Counters should fire the moment the stat enters the viewport — they are micro-events, not section beats. A scrubbed parent timeline makes them drag with scroll instead of resolving in 1.2 s.

**Accessibility.** Wrap each counter in `<span aria-label="50 de membri">…</span>` so screen readers read the final value, not "0, 1, 2, …". Hydrate the `aria-label` from the data attribute.

---

## 5. Scroll indicator

**Pick: top progress bar only.** Side dots and a custom cursor compete with the WebGL canvas for attention and break the Aman hush. A 1-pixel gold line at the very top of the viewport reads as "this site is measured and deliberate."

```html
<div id="scroll-progress" aria-hidden="true"></div>
```

```css
#scroll-progress {
  position: fixed;
  inset: 0 0 auto 0;
  height: 1px;
  background: linear-gradient(90deg,
    transparent 0%,
    var(--wol-gold) 20%,
    var(--wol-gold-2) 80%,
    transparent 100%);
  transform: scaleX(0);
  transform-origin: left center;
  z-index: 60;
  pointer-events: none;
  filter: drop-shadow(0 0 6px rgba(201, 164, 74, 0.45));
}
```

```js
// motion/progress.js
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.to("#scroll-progress", {
  scaleX: 1,
  ease: "none",
  scrollTrigger: {
    trigger: document.body,
    start: "top top",
    end:   "bottom bottom",
    scrub: 0.4,
  },
});
```

**`scrub: 0.4`** (not `1.2`) — the bar should feel *live* with scroll, not behind it. This is the single place a faster scrub is appropriate.

---

## 6. Section motion spec

The page has five sections. Each gets: **entrance**, **scroll-driven behavior**, **exit**, **code skeleton**. All scripts assume the shared `gsap`/`ScrollTrigger` setup from §1.

### 6.1 Hero — "Threshold" (`#hero`)

*Tone. Slow, dark, fog. The viewer feels they are arriving somewhere, not being shouted at.*

- **Entrance.** Particles fade in (`autoAlpha 0→1`, 2.0 s, `revelation`). The headline ("Woloshin Club") mask-reveals at 0.6 s. Sub-headline blur-up at 1.4 s. Scroll indicator fades in at 2.6 s.
- **Scroll-driven.** Hero pinned for 1 viewport. As user scrolls, the gold arc rotates `rotationY 0→20°`, particles drift (`drift`), camera pulls back (`z 5→9`, scrubbed). At the pin release, fog density drops from `0.06` to `0.02`.
- **Exit.** Whole canvas crossfades to next section background. Headline autoAlpha 0.

```js
function buildThreshold(tl) {
  tl.addLabel("intro", 0);

  tl.from(".hero-particles", { autoAlpha: 0, duration: 2.0, ease: ease("revelation") }, "intro");
  tl.from(".hero-headline .clip", { clipPath: "inset(0 100% 0 0)", duration: 1.6, ease: ease("ritual") }, "intro+=0.6");
  tl.from(".hero-sub p", { filter: "blur(12px)", autoAlpha: 0, y: 18, duration: 1.1, ease: ease("settle"), stagger: 0.12 }, "intro+=1.4");
  tl.from("#scroll-progress", { autoAlpha: 0, duration: 1.0, ease: ease("settle") }, "intro+=2.6");

  tl.addLabel("drift", 4.0);
  tl.to(".hero-arc", { rotationY: 20, duration: 4.0, ease: ease("drift") }, "drift");
  tl.to(camera.position, { z: 9, duration: 4.0, ease: ease("drift") }, "drift");
  tl.to(scene.fog.density, { density: 0.02, duration: 4.0, ease: ease("drift") }, "drift");

  tl.addLabel("exit", 8.0);
  tl.to("#hero", { autoAlpha: 0, duration: 1.2, ease: ease("settle") }, "exit");
}
```

**ScrollTrigger config.** `trigger: "#hero"`, `pin: true`, `scrub: 1.2`, `end: "+=200%"`.

### 6.2 Membership stats (`#stats`)

*Tone. Three numbers in cream serif, generous spacing, gold accent rule above each.*

- **Entrance.** Section eyebrow ("Cifre") mask-reveals (0.0 s). Each `.stat` block rises from `y: 60` with `autoAlpha` (stagger 0.18). Numbers start counting **0.6 s** after the block lands (see counter system §4 — independent trigger fires when the number element crosses 85 %).
- **Scroll-driven.** Background darkens 4 % as user scrolls past 50 %. No parallax (numbers should feel planted, not floating).
- **Exit.** Nothing — this section sits on a quiet plateau before "Ritual."

```js
function buildStats(tl) {
  tl.from(".eyebrow .clip", { clipPath: "inset(0 100% 0 0)", duration: 1.2, ease: ease("ritual") }, 0);
  tl.from(".stat", {
    y: 60, autoAlpha: 0, duration: LUX_DUR("revelation"),
    ease: ease("revelation"), stagger: { each: 0.18, from: "start" },
  }, 0.2);
  // counters fire from their own ScrollTrigger (see §4)
}
```

### 6.3 Ritual — "Cele trei ritualuri" (`#ritual`)

*Tone. Three steps, each a slow panel. This is where `snap` earns its keep.*

- **Entrance.** Section headline split-words (1.4 s, `revelation`). Each `.ritual-card` rises with `settle`, 0.25 s stagger.
- **Scroll-driven.** Pinned for 2.5 viewports. Three labels (`scrollTo`-style) — at 33 %, 66 %, 100 % of the pin, the active card lifts via `y: -12` + `boxShadow` deepen via `dropShadowFilter`. Inactive cards `autoAlpha: 0.4`. `snap: { snapTo: 1/3, duration: 0.4, ease: "power2.inOut" }`.
- **Exit.** Cards collapse to single column; the personal section underneath fades in behind them.

```js
function buildRitual(tl) {
  tl.from(".ritual-headline .word", {
    yPercent: 110, autoAlpha: 0,
    duration: LUX_DUR("revelation"),
    ease: ease("revelation"),
    stagger: { each: 0.06, from: "start" },
  }, 0);

  tl.addLabel("panels", 2.0);
  const cards = gsap.utils.toArray(".ritual-card");
  cards.forEach((c, i) => {
    tl.from(c, {
      y: 80, autoAlpha: 0, duration: LUX_DUR("settle"),
      ease: ease("settle"),
    }, `panels+=${i * 0.25}`);
    tl.to(c, { y: -12, boxShadow: "0 30px 80px rgba(0,0,0,0.6)", duration: 1.4, ease: ease("settle") }, `panels+=${0.8 + i * 0.6}`);
  });
}
```

### 6.4 Personal — admin invitation (`#personal`)

*Tone. The orb scene (Scene B) lives here. Copy is short and quiet.*

- **Entrance.** Headline split-words. Eyebrow mask. Portrait copy blur-up.
- **Scroll-driven.** The orb itself rotates `rotationY` from the WebGL scene. Text stays still.
- **Exit.** Orb drifts off-stage right; copy autoAlpha 0.

```js
function buildPersonal(tl) {
  tl.from(".personal-headline .word", { yPercent: 110, autoAlpha: 0, duration: LUX_DUR("revelation"), ease: ease("revelation"), stagger: 0.06 }, 0);
  tl.from(".personal-eyebrow .clip", { clipPath: "inset(0 100% 0 0)", duration: 1.2, ease: ease("ritual") }, 0.2);
  tl.from(".personal-copy p", { filter: "blur(12px)", autoAlpha: 0, y: 18, duration: 1.1, ease: ease("settle"), stagger: 0.12 }, 0.6);
}
```

### 6.5 Closing — CTA (`#cta`)

*Tone. Fog parts. The single line "Aplică pentru membership" lands. One button. Amber.*

- **Entrance.** NO scroll-driven scrub. Hard `toggleActions: "play none none reverse"`. Fog shader `uDensity` 0.08 → 0.0 over 1.5 s (`ritual`).
- **Scroll-driven.** None — this is a *moment*, not a sequence.
- **Exit.** CTA stays visible after exit; only the ambient fog stays in.

```js
function buildClosing(tl) {
  tl.from(".cta-headline .word", { yPercent: 110, autoAlpha: 0, duration: LUX_DUR("revelation"), ease: ease("revelation"), stagger: 0.06 }, 0);
  tl.from(".cta-button", { y: 24, autoAlpha: 0, duration: 1.1, ease: ease("magnetic") }, 0.6);
  tl.to(fogUniforms.uDensity, { value: 0.0, duration: 1.5, ease: ease("ritual") }, 0);
}
```

---

## 7. Three.js scenes

**Three.js r163+.** Plain ES modules. **No R3F** — R3F's reconciler overhead is wasted on three objects, and we want direct control of the render loop.

**One renderer, one canvas, one scene root per state.** Switching scenes = unmount the old `THREE.Group` from `sceneRoot` and mount the new one. No new `WebGLRenderer`, no new context.

### 7.1 Scene A — "Threshold" (Hero)

Fog + 300 particles + gold-rim arc + filmic grain.

```js
// three/scenes/threshold.js
import * as THREE from "three";

export function createThreshold({ renderer, scene, camera }) {
  scene.fog = new THREE.FogExp2(0x06080F, 0.06);
  scene.background = new THREE.Color(0x06080F);

  const root = new THREE.Group();
  scene.add(root);

  // ── Particles: 300 points, slow noise drift via shader.
  const COUNT = 300;
  const positions = new Float32Array(COUNT * 3);
  const seeds     = new Float32Array(COUNT);
  for (let i = 0; i < COUNT; i++) {
    positions.set([
      (Math.random() - 0.5) * 20,
      (Math.random() - 0.5) * 12,
      (Math.random() - 0.5) * 14,
    ], i * 3);
    seeds[i] = Math.random() * 1000;
  }
  const geo = new THREE.BufferGeometry();
  geo.setAttribute("position", new THREE.BufferAttribute(positions, 3));
  geo.setAttribute("aSeed",    new THREE.BufferAttribute(seeds, 1));

  const mat = new THREE.ShaderMaterial({
    uniforms: { uTime: { value: 0 }, uColor: { value: new THREE.Color(0xE8C492) } },
    vertexShader: /* glsl */`
      attribute float aSeed;
      uniform float uTime;
      varying float vAlpha;
      // simplex noise fbm
      float hash(vec3 p) { return fract(sin(dot(p, vec3(127.1, 311.7, 74.7))) * 43758.5453); }
      float noise(vec3 p) {
        vec3 i = floor(p), f = fract(p);
        f = f*f*(3.-2.*f);
        return mix(mix(mix(hash(i+vec3(0,0,0)), hash(i+vec3(1,0,0)), f.x),
                       mix(hash(i+vec3(0,1,0)), hash(i+vec3(1,1,0)), f.x), f.y),
                   mix(mix(hash(i+vec3(0,0,1)), hash(i+vec3(1,0,1)), f.x),
                       mix(hash(i+vec3(0,1,1)), hash(i+vec3(1,1,1)), f.x), f.y), f.z);
      }
      void main() {
        vec3 p = position;
        p.x += sin(uTime*0.15 + aSeed) * 0.6;
        p.y += noise(vec3(uTime*0.05, aSeed*0.1, 0.0)) * 1.2;
        p.z += cos(uTime*0.12 + aSeed) * 0.5;
        vec4 mv = modelViewMatrix * vec4(p, 1.0);
        gl_Position = projectionMatrix * mv;
        gl_PointSize = (180.0 / -mv.z) * (0.6 + 0.4 * sin(uTime + aSeed));
        vAlpha = 0.4 + 0.4 * sin(uTime*0.4 + aSeed);
      }`,
    fragmentShader: /* glsl */`
      uniform vec3 uColor;
      varying float vAlpha;
      void main() {
        vec2 uv = gl_PointCoord - 0.5;
        float d = length(uv);
        if (d > 0.5) discard;
        float a = smoothstep(0.5, 0.0, d) * vAlpha;
        gl_FragColor = vec4(uColor, a);
      }`,
    transparent: true,
    depthWrite: false,
    blending: THREE.AdditiveBlending,
  });

  const particles = new THREE.Points(geo, mat);
  root.add(particles);

  // ── Gold-rim arc: a torus segment, MeshStandardMaterial with rim light via Fresnel.
  const arcGeo = new THREE.TorusGeometry(2.8, 0.04, 32, 200, Math.PI);
  const arcMat = new THREE.ShaderMaterial({
    uniforms: { uColor: { value: new THREE.Color(0xC9A24A) } },
    vertexShader: /* glsl */`
      varying vec3 vN; varying vec3 vView;
      void main() {
        vec4 mv = modelViewMatrix * vec4(position, 1.0);
        vN = normalize(normalMatrix * normal);
        vView = normalize(-mv.xyz);
        gl_Position = projectionMatrix * mv;
      }`,
    fragmentShader: /* glsl */`
      uniform vec3 uColor;
      varying vec3 vN; varying vec3 vView;
      void main() {
        float fres = pow(1.0 - max(dot(vN, vView), 0.0), 2.4);
        gl_FragColor = vec4(uColor * (0.4 + 1.6 * fres), 0.7 + 0.3 * fres);
      }`,
    transparent: true,
    blending: THREE.AdditiveBlending,
  });
  const arc = new THREE.Mesh(arcGeo, arcMat);
  arc.position.set(0, 0.3, 0);
  arc.rotation.z = Math.PI;
  root.add(arc);

  camera.position.set(0, 0, 5);

  // ── Mouse parallax target (lerped in update).
  const mouse = { x: 0, y: 0, tx: 0, ty: 0 };
  window.addEventListener("mousemove", (e) => {
    mouse.tx = (e.clientX / window.innerWidth  - 0.5) * 0.6;
    mouse.ty = (e.clientY / window.innerHeight - 0.5) * 0.4;
  });

  // ── Filmic grain post-pass.
  const composer = new EffectComposer(renderer);
  composer.addPass(new RenderPass(scene, camera));
  const grainPass = new ShaderPass({
    uniforms: { tDiffuse: { value: null }, uTime: { value: 0 }, uAmount: { value: 0.06 } },
    vertexShader: `varying vec2 vUv; void main() { vUv = uv; gl_Position = projectionMatrix * modelViewMatrix * vec4(position,1.0); }`,
    fragmentShader: /* glsl */`
      uniform sampler2D tDiffuse;
      uniform float uTime, uAmount;
      varying vec2 vUv;
      float hash(vec2 p) { return fract(sin(dot(p, vec2(127.1, 311.7))) * 43758.5453); }
      void main() {
        vec4 c = texture2D(tDiffuse, vUv);
        float g = hash(vUv * vec2(1920.0, 1080.0) + uTime * 60.0) - 0.5;
        gl_FragColor = vec4(c.rgb + g * uAmount, c.a);
      }`,
  });
  composer.addPass(grainPass);

  return {
    root,
    update(dt, t) {
      mat.uniforms.uTime.value = t;
      grainPass.uniforms.uTime.value = t;
      mouse.x += (mouse.tx - mouse.x) * 0.08;
      mouse.y += (mouse.ty - mouse.y) * 0.08;
      camera.position.x = mouse.x;
      camera.position.y = -mouse.y;
      camera.lookAt(0, 0, 0);
    },
    composer, // renderer.render is replaced by composer.render() in the loop
    dispose() { window.removeEventListener("mousemove", () => {}); }
  };
}
```

**Notes.** `FogExp2` not `Fog` — exponential reads more cinematic. The Fresnel rim is *cheaper* than a real rim light and works without a directional light at all. AdditiveBlending on both particles and the arc lets them add into fog without occluding it.

### 7.2 Scene B — "Personal" (orb)

```js
// three/scenes/personal.js
import * as THREE from "three";

export function createPersonal({ renderer, scene, camera }) {
  scene.fog = new THREE.FogExp2(0x0F1B2D, 0.04);
  scene.background = new THREE.Color(0x0F1B2D);

  const root = new THREE.Group();
  scene.add(root);

  // Outer glass sphere.
  const outer = new THREE.Mesh(
    new THREE.SphereGeometry(1.0, 64, 64),
    new THREE.MeshPhysicalMaterial({
      color: 0x10203A,
      roughness: 0.05,
      metalness: 0.1,
      transmission: 0.85,
      thickness: 0.6,
      ior: 1.4,
      clearcoat: 1.0,
      clearcoatRoughness: 0.05,
      envMapIntensity: 1.2,
    })
  );

  // Inner "liquid" mesh — vertex-displaced by 3D noise.
  const innerGeo = new THREE.IcosahedronGeometry(0.78, 64);
  const innerMat = new THREE.ShaderMaterial({
    uniforms: {
      uTime: { value: 0 },
      uColor: { value: new THREE.Color(0xC9A24A) },
    },
    vertexShader: /* glsl */`
      uniform float uTime;
      varying vec3 vNormal; varying float vDisp;
      // hash + noise (Ashima)
      vec3 mod289(vec3 x){return x-floor(x*(1./289.))*289.;}
      vec4 mod289(vec4 x){return x-floor(x*(1./289.))*289.;}
      vec4 perm(vec4 x){return mod289(((x*34.)+1.)*x);}
      float noise(vec3 p){
        vec3 a=floor(p), f=fract(p);
        f=f*f*(3.-2.*f);
        return mix(mix(mix(dot(perm(a+vec3(0,0,0))+vec4(0,0,0,0), f-vec3(0,0,0)),
                            dot(perm(a+vec3(1,0,0))+vec4(0,0,0,0), f-vec3(1,0,0)), f.x),
                          mix(dot(perm(a+vec3(0,1,0))+vec4(0,0,0,0), f-vec3(0,1,0)),
                              dot(perm(a+vec3(1,1,0))+vec4(0,0,0,0), f-vec3(1,1,0)), f.x), f.y),
                      mix(mix(dot(perm(a+vec3(0,0,1))+vec4(0,0,0,0), f-vec3(0,0,1)),
                              dot(perm(a+vec3(1,0,1))+vec4(0,0,0,0), f-vec3(1,0,1)), f.x),
                          mix(dot(perm(a+vec3(0,1,1))+vec4(0,0,0,0), f-vec3(0,1,1)),
                              dot(perm(a+vec3(1,1,1))+vec4(0,0,0,0), f-vec3(1,1,1)), f.x), f.y), f.z);
      }
      void main() {
        vec3 p = position;
        float n = noise(p * 1.6 + vec3(uTime * 0.25));
        float n2 = noise(p * 4.0 - vec3(uTime * 0.4));
        float d = n * 0.12 + n2 * 0.04;
        p += normal * d;
        vDisp = d;
        vNormal = normalize(normalMatrix * normal);
        gl_Position = projectionMatrix * modelViewMatrix * vec4(p, 1.0);
      }`,
    fragmentShader: /* glsl */`
      uniform vec3 uColor;
      varying float vDisp;
      varying vec3 vNormal;
      void main() {
        float rim = pow(1.0 - abs(vNormal.z), 2.0);
        vec3 c = mix(uColor * 0.35, uColor, rim);
        gl_FragColor = vec4(c, 0.85);
      }`,
    transparent: true,
  });
  const inner = new THREE.Mesh(innerGeo, innerMat);
  outer.add(inner);
  root.add(outer);

  camera.position.set(0, 0, 3.2);

  const mouse = { tx: 0, ty: 0 };
  window.addEventListener("mousemove", (e) => {
    mouse.tx = (e.clientX / window.innerWidth  - 0.5) * 0.3;
    mouse.ty = (e.clientY / window.innerHeight - 0.5) * 0.2;
  });

  return {
    root,
    update(dt, t) {
      innerMat.uniforms.uTime.value = t;
      outer.rotation.y += (mouse.tx - outer.rotation.y) * 0.06;
      outer.rotation.x += (-mouse.ty - outer.rotation.x) * 0.06;
      outer.position.y = Math.sin(t * 0.5) * 0.05;
    },
    dispose() { /* remove listeners */ },
  };
}
```

**Notes.** `MeshPhysicalMaterial` requires `envMap` for `transmission` to read right. Use `RoomEnvironment` from `three/examples/jsm/environments/RoomEnvironment.js` baked once via `PMREMGenerator`. No real lights needed.

### 7.3 Scene C — "Closing" (fog parting)

A fullscreen plane with a depth-displaced fog shader. As the user enters the section, `uDensity` tweens down — the CTA reveals from inside the mist.

```js
// three/scenes/closing.js
import * as THREE from "three";

export function createClosing({ renderer, scene, camera }) {
  scene.background = new THREE.Color(0x06080F);

  const root = new THREE.Group();
  scene.add(root);

  // Depth fog plane.
  const geo = new THREE.PlaneGeometry(2, 2);
  const mat = new THREE.ShaderMaterial({
    uniforms: {
      uTime:    { value: 0 },
      uDensity: { value: 0.85 },     // GSAP animates this 0.85 → 0.0
      uColor:   { value: new THREE.Color(0x0F1B2D) },
      uGrain:   { value: new THREE.Color(0x06080F) },
      uMouse:   { value: new THREE.Vector2(0.5, 0.5) },
    },
    vertexShader: /* glsl */`
      varying vec2 vUv;
      void main() { vUv = uv; gl_Position = vec4(position.xy, 0.0, 1.0); }`,
    fragmentShader: /* glsl */`
      uniform float uTime, uDensity;
      uniform vec2  uMouse;
      uniform vec3  uColor, uGrain;
      varying vec2 vUv;

      float hash(vec2 p){return fract(sin(dot(p, vec2(127.1, 311.7)))*43758.5453);}
      float noise(vec2 p){
        vec2 i=floor(p), f=fract(p); f=f*f*(3.-2.*f);
        return mix(mix(hash(i), hash(i+vec2(1,0)), f.x),
                   mix(hash(i+vec2(0,1)), hash(i+vec2(1,1)), f.x), f.y);
      }
      float fbm(vec2 p){ float v=0., a=0.5; for(int i=0;i<5;i++){ v+=a*noise(p); p*=2.02; a*=0.5; } return v; }

      void main() {
        vec2 uv = vUv;
        // Mouse pulls fog away.
        float d = distance(uv, uMouse);
        float pull = smoothstep(0.5, 0.0, d) * 0.6;

        // Drift
        vec2 q = uv * vec2(2.4, 1.6) + vec2(uTime*0.02, uTime*0.015);
        float n = fbm(q);
        float fog = smoothstep(0.45, 1.0, n) * uDensity;
        fog *= 1.0 - pull;

        vec3 col = mix(uGrain, uColor, fog);
        gl_FragColor = vec4(col, fog + 0.05);
      }`,
    transparent: true,
    depthWrite: false,
  });
  const plane = new THREE.Mesh(geo, mat);
  root.add(plane);

  // Orthographic camera for a fullscreen quad.
  const cam = new THREE.OrthographicCamera(-1, 1, 1, -1, 0, 1);

  const mouse = { x: 0.5, y: 0.5, tx: 0.5, ty: 0.5 };
  window.addEventListener("mousemove", (e) => {
    mouse.tx = e.clientX / window.innerWidth;
    mouse.ty = 1.0 - e.clientY / window.innerHeight;
  });

  return {
    root,
    update(dt, t) {
      mat.uniforms.uTime.value = t;
      mouse.x += (mouse.tx - mouse.x) * 0.05;
      mouse.y += (mouse.ty - mouse.y) * 0.05;
      mat.uniforms.uMouse.value.set(mouse.x, mouse.y);
    },
    setDensity(v) { mat.uniforms.uDensity.value = v; },
    orthoCam: cam,
    scene, // use ortho cam for this scene
    dispose() {},
  };
}
```

**Notes.** Ortho camera for a fullscreen post-style quad — no perspective, no projection matrix drama. The fog plane sits *behind* the CTA text in the DOM (`z-index: 0`), letting the headline carry its own gradient and be readable as fog clears.

---

## 8. Performance budget

Hard limits. Anything over budget gets cut, not slipped.

| Item | Budget | How |
| --- | --- | --- |
| Three.js memory | **< 50 MB** | `renderer.info.memory` inspected per second in non‑prod. Reuse geometries/materials. |
| WebGL contexts | **1** | Single canvas; switch scene roots on `IntersectionObserver`. Never `new WebGLRenderer`. |
| Device pixel ratio | **cap 1.5** | `renderer.setPixelRatio(Math.min(1.5, window.devicePixelRatio))`. |
| Active draw calls | < 20 per frame | Particles use `Points` (1 call), arc uses `Mesh`, orb uses `Mesh`+inner. |
| Three render loop | **pause when off-screen** | `IntersectionObserver` on each scene container; call `cancelAnimationFrame` when `isIntersecting === false`. |
| GSAP timelines | **pause off-screen** | `gsap.matchMedia()` reverts; `ScrollTrigger.create` is killed on section leave. No idle ticking. |
| First Contentful Paint | < 1.5 s on 4G | Three.js scene A `dispose`/`unmount` is **not** in the critical path. HTML/CSS hero lands first; canvas mounts *after* `requestIdleCallback`. |
| ScrollTrigger refresh | on resize only | `ScrollTrigger.addEventListener("refreshInit", () => window.dispatchEvent(new Event("woloshin:layout-ready")))`; no refresh on font load (use `font-display: swap`). |

```js
// three/manager.js
import * as THREE from "three";
import { createThreshold } from "./scenes/threshold.js";
import { createPersonal  } from "./scenes/personal.js";
import { createClosing   } from "./scenes/closing.js";

export function createSceneManager() {
  const canvas = document.getElementById("wol-canvas");
  const renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true, powerPreference: "high-performance" });
  renderer.setPixelRatio(Math.min(1.5, window.devicePixelRatio));
  renderer.setSize(window.innerWidth, window.innerHeight, false);
  renderer.outputColorSpace = THREE.SRGBColorSpace;

  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(38, window.innerWidth / window.innerHeight, 0.1, 100);

  let current = null;
  const mounts = {
    "#hero":    createThreshold({ renderer, scene, camera }),
    "#personal": createPersonal({ renderer, scene, camera }),
    "#cta":     createClosing({ renderer, scene, camera }),
  };

  let raf = 0;
  const clock = new THREE.Clock();
  function loop() {
    raf = requestAnimationFrame(loop);
    const t = clock.getElapsedTime();
    if (current) current.update(clock.getDelta(), t);
    if (current?.composer) current.composer.render();
    else renderer.render(scene, camera);
  }

  function mount(selector) {
    if (current?.dispose) current.dispose();
    if (current?.root) scene.remove(current.root);
    current = mounts[selector];
    if (!current) return;
    if (current.root) scene.add(current.root);
    if (current.orthoCam) { /* swap to ortho */ }
  }

  // IntersectionObserver drives mount + raf.
  const io = new IntersectionObserver((entries) => {
    entries.forEach((e) => {
      if (!e.isIntersecting) return;
      mount(`#${e.target.id}`);
    });
  }, { rootMargin: "20% 0px 20% 0px", threshold: 0.01 });

  document.querySelectorAll("[data-three]").forEach((el) => io.observe(el));

  // Pause when nothing visible.
  const visibility = new IntersectionObserver((entries) => {
    if (entries.every((e) => !e.isIntersecting)) cancelAnimationFrame(raf);
    else if (!raf) loop();
  }, { threshold: 0 });
  document.querySelectorAll("[data-three]").forEach((el) => visibility.observe(el));

  // WebGL fallback.
  try {
    renderer.getContext().getExtension("WEBGL_debug_renderer_info");
  } catch {
    document.documentElement.dataset.three = "fail";
    document.querySelector(".hero-static-fallback")?.removeAttribute("hidden");
  }

  return { renderer, scene, camera, mount };
}
```

---

## 9. Compatibility & accessibility

### 9.1 `prefers-reduced-motion`

```js
const mm = gsap.matchMedia();

mm.add(
  { reduce: "(prefers-reduced-motion: reduce)" },
  () => {
    // Scrub → instant snap, durations → 0.01, particles → static, fog → no update.
    ScrollTrigger.getAll().forEach((st) => {
      st.vars.scrub = false;
      st.vars.toggleActions = "play none none none";
      st.progress(1); // jump to end
    });
    gsap.globalTimeline.timeScale(0.01);
    // Disable three.js render loop entirely.
    document.documentElement.dataset.motion = "reduced";
  }
);

mm.add(
  { desktop: "(min-width: 1024px)", mobile: "(max-width: 1023.99px)" },
  (ctx) => {
    const { isDesktop } = ctx.conditions;
    if (!isDesktop) {
      // Mobile: shorten all durations 30 %, drop pin, drop snap, drop particle count.
      gsap.defaults({ duration: () => gsap.defaults().duration * 0.7 });
      ScrollTrigger.getAll().forEach((st) => { st.vars.pin = false; st.vars.snap = false; });
      // Pass a smaller particle count into threshold scene on init.
    }
  }
);
```

Static states still match the final visual (`autoAlpha: 1`, `clipPath: inset(0)`, `filter: blur(0)`) so the page looks *finished* without motion — never half-built.

### 9.2 WebGL fallback

```js
function detectWebGL() {
  try {
    const c = document.createElement("canvas");
    return !!(c.getContext("webgl2") || c.getContext("webgl"));
  } catch { return false; }
}

if (!detectWebGL()) {
  document.documentElement.dataset.three = "fail";
  // Hero renders a static radial-gradient + an SVG arc instead. Same DOM structure.
}
```

### 9.3 Screen reader

- Each counter: `<span aria-label="50" data-target="50">0</span>` — animate `textContent` only, leave `aria-label` as the final value.
- Decorative WebGL canvases: `aria-hidden="true"` and `role="presentation"`.
- `prefers-reduced-motion`: also tag the `<html>` so CSS `@media (prefers-reduced-motion: reduce)` rules apply (no transitions on hover).

### 9.4 Battery / tab visibility

```js
document.addEventListener("visibilitychange", () => {
  if (document.hidden) cancelAnimationFrame(raf);
  else if (!raf) loop();
});
```

---

## 10. Top motion moves (one-screen summary)

1. **Five-ease luxury vocabulary** (`revelation` / `settle` / `drift` / `magnetic` / `ritual`) — every tween names one. No defaults, no `power1.out`. This is the single biggest signal of "expensive."
2. **Split-words mask-reveal** on every headline, 0.06 s stagger, `revelation` — quiet wave, not typewriter.
3. **Three.js Threshold scene**: 300 additive particles + Fresnel-rim gold arc + filmic grain post-pass on a single shared renderer; fog density is *scrubbed* with scroll, not animated.
4. **One WebGL renderer, three scenes**, mounted by `IntersectionObserver` — never more than one GL context.
5. **Top progress bar only** (1 px gold line, `scrub: 0.4`) — no side dots, no custom cursor; hush over chrome.
6. **Snap-scroll on "Ritual"** with three panel cards (`snapTo: 1/3`), cinematic but discrete.
7. **Counters fire on their own per-element ScrollTrigger** (not on the parent scrubbed timeline) so they resolve in 1.2 s instead of dragging.
8. **`prefers-reduced-motion` → static end-states, not motion-disabled mid-states**, and the page still feels complete.

---

*End of motion spec. Hand to copy + design for narrative threading; hand to frontend for build wiring (`data-composition-id` keys match the section ids in §1).*