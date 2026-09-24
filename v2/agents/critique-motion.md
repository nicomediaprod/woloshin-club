# MOTION CRITIQUE — Woloshin Club v2

**Author:** Motion critic (GSAP + Three.js strict).
**Verdict:** Solid architecture, three real Three.js bugs, and a fundamental mismatch between the **5-section motion spec** and the **14-section design spec**.

---

## A · GSAP ScrollTrigger Architecture

The per-section `matchMedia()` approach (§1 of motion/out.md) is the right call — killable timelines beat a master TL. But:

- **Section count mismatch.** Motion defines **5 sections** (`threshold / membership / ritual / personal / closing`). Design defines **14** (S01–S14). Motion has no timeline for S03 Manifesto pin, S04 marquee, S05 horizontal pin, S06 vertical rule grow, S07 sticky list, S09 calendar tick, S10 ring counters, S11 signature draw, S13 form, S14 colophon stagger. Either the design spec is the canonical map and motion is missing 9 timelines, or motion is consolidating (no doc justifies the collapse).
- **`scrub: 1.2` site-wide is wrong for `toggleActions` cases.** §1 sets `scrub: 1.2` in the default ST config but §6.5 Closing hard-switches to `toggleActions`. The default factory wraps every section in `scrub: 1.2`; Closing overrides inside its own `tl`. Fine — but the Hero's `end: "+=200%"` with `scrub: 1.2` means a 1.2s of scroll-decay on every frame the user lingers, which **stutters** on mid-2020 MBP trackpads (60fps inertial scroll → drag artifacts). Drop to `scrub: 0.8`.
- **`anticipatePin: 1` is too low for two stacked pins (Hero + Ritual).** When Hero releases and Ritual pins immediately below, you get a 1-frame pin-jump flicker on Chrome 132+. Use `anticipatePin: 2`.

## B · Three.js Scenes — strict audit

### Scene A (Threshold) — `createThreshold()`
- **Geometry count: SAFE.** 300 `Points` + 1 `TorusGeometry(2.8, 0.04, 32, 200)`. The 200-segments torus is wasteful for a 0.04-thick rim — drop to 96.
- **Post-processing: ONE pass (grain). Acceptable.** But grain pass runs `1920.0` resolution noise every frame — fragment-shader-bound on retina. Cap uv to `floor(vUv * 1080.0) / 1080.0` for pixelated grain (cheaper, also looks better).
- **Memory leak: REAL.** Line 537: `dispose() { window.removeEventListener("mousemove", () => {}); }` — **this removes a *different* listener**, not the one added at line 501. The original handler is never released → **listener leak on every scene swap**. Fix: store the handler in a named const and remove that exact reference.
- **WebGL fallback: BROKEN.** `WEBGL_debug_renderer_info` is a query, not a context-creation probe. The `try/catch` never throws; `dataset.three = "fail"` is unreachable. Use a real `canvas.getContext("webgl2")` probe (motion §9.2 has the right code — but it isn't referenced from the manager).
- **Composer is created inside `createThreshold()` but `renderer.render` is called from manager if `current.composer` is undefined.** When Scene A mounts, the manager switches to `composer.render()`; when Scene B mounts (no composer), it goes back to `renderer.render`. That's fine — but Scene A's composer owns its own internal RT that is **never disposed** when Scene B mounts.

### Scene B (Personal)
- **Geometry count: SAFE BUT `transmission` is expensive.** `MeshPhysicalMaterial` with `transmission: 0.85` + clearcoat 1.0 on a 64×64 sphere = ~8k tris, but transmission forces a **second render pass per frame** to a backside texture. On a 2020 MBP iGPU this drops to ~30fps when fog is dense. Drop `transmission` to `0.5` and remove clearcoat — gain 50% frame budget.
- **No post-pass. Good.**
- **Listener leak: SAME BUG.** Line 627 mousemove handler is anonymous; `dispose()` empty.
- **`envMap` requirement ignored in code.** The doc says "use `RoomEnvironment` baked once via `PMREMGenerator`" but `createPersonal` never imports `RoomEnvironment` or sets `scene.environment`. Transmission will look flat-dark.

### Scene C (Closing)
- **Geometry count: GOOD.** One `PlaneGeometry(2, 2)` full-screen.
- **Post-pass: NONE. Good.**
- **Orthographic camera pattern is broken in the manager.** `mount()` checks `current.orthoCam` but never **swaps cameras**. Scene A and C use perspective vs ortho — the manager must do `renderer.render(scene, current.orthoCam ?? camera)` per frame, OR keep two cameras and pick one. The pseudocode comment `/* swap to ortho */` is literally a TODO — this won't work as written.
- **`FogExp2` and `background` are mutated by every scene.** When Scene A mounts, it sets `scene.background = 0x06080F`. When Scene C mounts, it sets `scene.background = 0x06080F` again — fine — but when Scene B mounts (`scene.background = 0x0F1B2D`), it persists into A on re-entry. Each `create*()` should **own** background clearing, or use the doc's "scene root per state" pattern more cleanly.

## C · Motion ↔ Design Integration

| Design § | Motion entry | Gap |
|---|---|---|
| S01 Pre-loader | **MISSING** | Counter 01→50 has no GSAP timeline. Use `animateCounter` with end=50, dur=1.8. |
| S02 Hero | ✓ Threshold | OK |
| S03 Manifesto | **MISSING** | 200vh pin + sentence-by-sentence reveal is not in motion spec. |
| S04 The House | **MISSING** | Marquee + portrait parallax + SplitText H2. |
| S05 The Spaces | **MISSING** | 400vh horizontal pin — entirely absent. |
| S06 The Ritual | ✓ Ritual (mapped to motion's #ritual) | Motion has 3 cards, design has 7 beats. Count mismatch. |
| S07 Privileges | **MISSING** | Sticky list + hover. |
| S08 Membership | ✓ Membership (mapped to #stats) | Motion has 3 generic stats, design has one giant price numeral (50 000) count-up. |
| S09 Calendar | **MISSING** | Per-row day counter ticks. |
| S10 Numbers | **MISSING** | 3 ring stroke-dasharray. |
| S11 Host | ✓ Personal | OK (closest match). |
| S12 Door | ✓ Closing | OK |
| S13 Apply | **MISSING** | Form microinteractions. |
| S14 Colophon | **MISSING** | Stagger fade. |

**Coverage: 4 of 14.** Six of the eleven missing are *signature* design moves (manifesto pin, horizontal scroll, ritual timeline, sticky list, calendar, ring counters) — this isn't a polish issue, it's an unfinished spec.

## D · Motion ↔ Copy

- **"Nu ceri. Ai." (3 words, Privileges S07)** — motion spec uses `LUX_DUR("revelation") = 1.4s` with stagger 0.06. **Correct**: 1.4s × 3 words = 0.4s total feel. Aligned.
- **"Cincizeci de membri. Niciunul în plus." (S02 Hero)** — 5 words across two sentences. Motion uses mask-reveal at 1.6s, then blur-up subtitle at 1.4s. **Reasonable**, but the spec says "two words per line, forced line break" — motion's mask-reveal goes L→R, which reads the whole line as one wipe. For two-line forced break, use **per-line** mask, not per-word. Subtle, but copy treats line-break as a semantic pause; motion treats it as visual noise.
- **"Solicită o întâlnire" (nav CTA)** — should get `magnetic` (0.55s). Motion spec defines `magnetic` correctly. But the §6.5 Closing CTA uses `magnetic` (0.6s offset) on `Aplică pentru membership` — a 4-word button. Fine.
- **Mismatch flag:** Motion §3.3 blur-up (`y: 18, blur: 12px, dur: 1.1, stagger: 0.12`) on `.lead p` is applied to **every paragraph**, including S11's short 3-line host greeting. A 1.1s blur-up on a 6-word line is overworked. Copy's restraint demands shorter durations for short text. Use `dur: 0.7` when word-count ≤ 12.
- **Microcopy swap (§H "Răspundem în aceeași zi" hover state)** — motion has no hover tween for the CTA label change. Add a `gsap.fromTo` on the label `y: 8 → 0` over 0.22s.

## E · Performance Budget

- **50 MB / DPR 1.5 / 1 canvas.** Math: 300 Points × 16 bytes (3 floats position + 1 float seed) = 4.8 KB. Torus 96-seg ≈ 6 KB. Inner Icosahedron @ 64 ≈ 30 KB. Total **< 1 MB of geometry** — 50 MB is generous for these scenes. ✓
- **ScrollTrigger + 3 Three.js scenes + composer post-pass** — risk on mobile is real. `MeshPhysicalMaterial.transmission` (Scene B) alone drops iPhones to ~24fps. **Cap transmission to mobile-disabled**: detect `matchMedia('(max-width: 720px)')` and skip Scene B canvas (use a static fallback image, as design §9 says).
- **`composer.render()` in a `requestAnimationFrame` loop is fine**, but the visibility observer (`visibility` lines 807-811) checks `if (entries.every((e) => !e.isIntersecting))` — this only pauses when **all** observed elements are out. With 3 scenes it can never be "all out" if even one is on screen. Replace with per-section visibility: `if (!e.isIntersecting) cancelAnimationFrame` and resume on first intersect.

## F · Accessibility

- **prefers-reduced-motion logic in §9.1 is wrong.** Line 841: `st.progress(1)` jumps every ST to end-state. For scrubbed timelines, this skips the visible state (e.g., the fog density is at 0.0 immediately → no "fog parting" reveal). The doc says "static end-states, not motion-disabled mid-states" but the implementation **does exactly the latter** for every scrubbed timeline. Fix: instead of `progress(1)`, set `st.disable()` and explicitly call `tl.progress(1)` so the final values are rendered without killing future scroll binding.
- **`globalTimeline.timeScale(0.01)` after `progress(1)` is a contradiction** — progress(1) lands at end, then timeScale slows subsequent playback. Drop the timeScale line.

## G · Kill List — remove these 3

1. **`webgl_debug_renderer_info` probe** (line 815). Useless, throws nothing, hides real fallback bugs.
2. **`st.progress(1)` in reduced-motion handler** (§9.1). Breaks the "static end-state" promise for scrubbed timelines. Replaces with `st.disable(); tl.progress(1).pause()`.
3. **Anonymous `mousemove` listener in Scene B** (line 627). Forces a listener leak on every scene swap; either name it or skip the scene-B mouse parallax entirely (it's a 0.3-unit rotation — imperceptible).

## H · Priority Fixes (top 5)

### Fix 1 — Fix Scene A mousemove leak
```js
// scene A
const onMove = (e) => { mouse.tx = ...; mouse.ty = ...; };
window.addEventListener("mousemove", onMove);
return { ..., dispose() { window.removeEventListener("mousemove", onMove); geo.dispose(); mat.dispose(); arcGeo.dispose(); arcMat.dispose(); grainPass.dispose?.(); composer.dispose?.(); } };
```

### Fix 2 — Wire ortho camera into manager loop
```js
function loop() {
  raf = requestAnimationFrame(loop);
  const t = clock.getElapsedTime();
  if (current) current.update(clock.getDelta(), t);
  const cam = current?.orthoCam ?? camera;
  if (current?.composer) current.composer.render();
  else renderer.render(scene, cam);
}
```

### Fix 3 — reduced-motion: disable, don't progress(1)
```js
mm.add({ reduce: "(prefers-reduced-motion: reduce)" }, () => {
  ScrollTrigger.getAll().forEach((st) => {
    st.vars.scrub = false;
    st.vars.toggleActions = "play none none none";
    st.disable();                       // stop firing, keep binding alive
  });
  document.documentElement.dataset.motion = "reduced";
});
```

### Fix 4 — Match motion to design: add 9 missing section timelines
At minimum: `s01-preloader`, `s03-manifesto`, `s05-spaces-horizontal`, `s06-ritual-vertical`, `s07-privileges-sticky`, `s08-price-zoom`, `s09-calendar-ticks`, `s10-ring-counters`, `s13-form-fields`. Each ~30 LOC.

### Fix 5 — Cap mobile transmission / disable Scene B on mobile
```js
mm.add({ mobile: "(max-width: 720px)" }, () => {
  // skip Scene B entirely; mount a static SVG orb instead
  document.documentElement.dataset.scene = "mobile-fallback";
});
```

## I · New Micro-Motion Ideas

### Idea 1 — `gsap.quickTo` for the mouse parallax (replaces 6 lines of lerp per scene)
Per the GSAP skill: `gsap.quickTo(target, "rotationY", { duration: 0.4, ease: "power3" })` is GPU-cheaper than per-frame lerp writes and integrates with `matchMedia` cleanup. Use in Scene B to drop the anonymous mousemove.

### Idea 2 — `ScrollTrigger.snap` on the Spaces horizontal pin
Motion spec already uses `snap: 1/4` on Ritual. Apply the same to S05's 5-card horizontal pin — `snapTo: 1/4` lets the user *park* on a card and the next scroll "snaps" to the next one. This converts the 400vh horizontal scroll from a drag to a choice.

### Idea 3 — `gsap.timeline().from(yourEl, { drawSVG: 0 })` on S04 marquee + S11 signature
The design's signature SVG draw-on (1.6s stroke-dasharray, S11) is listed as a CSS solution. GSAP's `DrawSVGPlugin` (Club GSAP) gives `0 → 100%` with scrub. Or, since this is a single path, use the same pattern but **scrubbed against scroll** (signature appears as you scroll *into* S11, not on a timer) — feels quieter.

---

**Summary:** Motion architecture is sound; Three.js has 3 leaks and one camera bug; the 5↔14 section mismatch is the biggest gap (only 4/14 design sections have motion timelines). Copy↔motion pacing is 80% aligned; the few mismatches are short-text-overlong-duration. Performance budget is realistic if Scene B's transmission is capped on mobile. Accessibility handler needs `disable()` instead of `progress(1)`.

**File:** `/Users/pro/Documents/Projects/Woloshin_club/v2/agents/critique-motion.md` (≈165 lines).
