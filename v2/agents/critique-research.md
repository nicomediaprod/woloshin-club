# Research Critique — Woloshin Club v2

**Reviewer:** research critic
**Scope:** design/out.md, copy/out.md, motion/out.md — peer deliverables for the 14-section premium club landing page (Moldova, 50 members, 50,000 MDL entry, Romanian).

---

## A · CONTRADICTIONS (concrete, file:section refs)

1. **Price architecture is split-brain.** Design S08 (line 235–248) commits to a *single* numeral "50 000" with subtitle "lei moldovenești", explicitly forbidding comparison, FAQ, or "from/to": *"Single tier, no comparison, no 'from', no FAQ inline"*. Copy C ("Ce deschide ușa", line 69–92) breaks this with a hard two-component breakdown: **10 000 MDL cotizație anuală + 40 000 MDL sold personal**. Worse: copy's "cotizație anuală" directly contradicts design's clarifying line "no monthly dues". Research §4.4 (*"The single number IS the brand. Forcing a single decision is what Soho House, Aman, Cheval Blanc, and every Awwwards luxury SOTD do"*) is on design's side. **Copy has to die here, not design.**

2. **Calendar count: 12 vs 3.** Design S09 eyebrow (line 254): *"ANUL I · 12 EVENIMENTE"*. Design S10 ring (line 290): *"12 — closed events a year"*. Copy F headline (line 160): *"Trei nopți pe an. Cincizeci de oameni."* and body #1 (line 169): *"Trei evenimente pe an"*. Copy F #4 (line 178) further divides events into *"Cina cu fondatorul" — De două ori pe an* — making the count internally inconsistent *inside copy itself*. Pick one: the brand either has a calendar of 12 events or three signature nights, not both.

3. **Motion §5 says no side dots and no custom cursor.** Motion §5 (line 229): *"Side dots and a custom cursor compete with the WebGL canvas for attention and break the Aman hush... no side dots, no custom cursor; hush over chrome."* Design §6 (line 462–467) mandates a 4px gold magnetic cursor and §6 line 477 specifies 8 right-edge side dots with Cormorant labels. Design and motion are literally opposite on two of the page's most-visible chrome elements.

4. **Motion Scene A and Design S02 disagree on what's in the hero.** Motion §7.1 (line 393–540): *"Scene A — Threshold (Hero). Fog + 300 particles + gold-rim arc + filmic grain."* The spec includes a *Fresnel-rim gold arc* that *rotates 0→20°* on scroll. Design S02 (line 107–114) describes *"Scene A: Volumetric Fog Chamber"* with FBM noise, gold-amber tint, and *"A single thin light-shaft ray (1px-wide) drifts left → right over 24s"* — no arc, no Fresnel. Two specs, one canvas. Engineering will build whichever they read first.

5. **Section count mismatch.** Motion's §6 maps to 5 sections: `#hero`, `#stats`, `#ritual`, `#personal`, `#cta`. Design has 14 sections (S01–S14). Nine of design's sections (S04 The House, S05 Spaces horizontal cards, S06 Ritual timeline, S07 Privileges, S09 Calendar, S11 Host, S13 Form, S14 Colophon) have **zero** corresponding motion spec. The build agent will receive a page that's 9 sections with no animation contract.

6. **Content diverges on privileges.** Design S07 (line 211–219) lists 8 named-object privileges — "The Door", "The Cellar", "The Library", "The Calendar", "The Steam", "The Studio", "The Salon", "The Off-Season" — with thin-line SVG icons. Copy E (line 137–148) lists 4 functional privileges: "Preț de membru", "Camerele private", "Rezervarea", "Produsele noi". Different number, different content, different register. Copy's register (functional benefits) clashes with design's register (named rooms).

7. **Administrator count contradiction.** Copy D micro-meta (line 120): *"Cincizeci de administratori, da. Fiecăruia — un singur membru."* — 50 dedicated administrators for 50 members. Design §11 says "the host portrait" implies one host ("Rareș") and one signature. Body copy in Copy D says "administratorul tău" — singular per member — but the meta-quantifier of 50 is operationally implausible and reads like Soho-House-membership-deck arithmetic.

---

## B · MISSED RESEARCH OPPORTUNITIES

1. **The 42/50 scarcity dot-grid is the single highest-impact element research called out (§1.1, §4.2, §7 Action #1) and is missing from all three peer outputs.** The brandbook copy *"42 din 50 locuri ocupate"* already exists in v1. Design §1 Page Map has 14 sections and Design §4 has the density table — none allocate a section, micro-section, or surface for the live dot-grid. Copy never references 42/50 either. This is research's #1 action item and zero peer picked it up.

2. **Sobha Privy scrubbed zoom-on-scroll on the price (§1.6, §3.2) is not in any motion spec.** Design S08 specifies count-up only. Motion §4 also specifies count-up only (`gsap.to({v:0},{v:50000,duration:1.2})`). Research explicitly recommends: *"as the price card enters the viewport, the value '50 000 MDL' zooms from ~30% scale to full size, anchored to its centerline, scrubbed against scroll position."* Neither peer did it.

3. **Forge Automotive point-light fake 3D on the hero photo (§1.7, §2.1) is the 2026 move research recommended.** Design S02's 3D plan is shader-only (FBM noise + ray), Motion §7.1 is Fresnel-arc + particles. The pure-CSS point-light trick (≈20 lines JS, no shader) is the cheapest path to "the banya photo feels lit when I move my mouse" — and it explicitly maps to the banya night photo research §1.7 names. Both peers went heavy when light was the right move.

4. **Codrops SVG-mask hero finale (research §3.4) reuses the existing gold ornament-diamond.** Design's hero exit (line 105) is a subtitle parallax + 3D fog rotation. Research explicitly: *"the gold ornament-diamond grows from 8×8px to a full-screen SVG mask as you scroll past 80vh. Photo reveals from a center diamond outward."* — and the diamond is already in v1 brand assets. Neither peer used it.

5. **Native CSS `animation-timeline: view()` (research §2.2) for the privilege cards is the free 2026 perf win.** Motion §1 (line 22–57) builds a whole GSAP matchMedia + ScrollTrigger scaffold for what Chrome 115+/Safari 18+ does natively with 10 lines of CSS. Research explicitly: *"replace the current IntersectionObserver-driven reveal-on-scroll with the native CSS version for cards 1–4 in the privilege grid."*

6. **The Cheval Blanc "audio-as-mark" idea (research §1.4) for the closed Telegram chat is worth $50 of polish.** Copy F §3 (line 175–176) lists the Telegram circle as a plain privilege item. Research suggests *"tap-and-listen"* — a 6-second audio whisper from Rareș, scroll-triggered, replacing the bullet. Motion has the scroll infrastructure for it; copy writes the words; design has no surface. All three missed it.

---

## C · TONE / LUXURY GRADE — slips out of Aman

1. **Copy C subhead (line 79)** — *"O singură plată. Două componente: o cotizație anuală, care ține clubul viu, și un sold personal — depozitul tău în comunitate, folosibil oricând în complexele noastre."* The phrase "folosibil oricând în complexele noastre" reads like a hotel brochure. Aman would never end a poetic sentence with "anytime in our premises". Strip the operational tail.

2. **Copy D #3 (line 117)** — *"Ea îți răspunde la mesaje, îți rezervă baia privată fără să întrebi, îți aduce ceaiul înainte să-l ceri, îți amintește data nunții prietenului tău dacă vrei să-l inviți. Îți scrie dimineața dacă nu ai mai venit de trei săptămâni."* The last sentence — *"writes to you in the morning if you haven't come in three weeks"* — slides from concierge into surveillance. Aesop wouldn't write that. Cut the last sentence entirely.

3. **Copy G body (line 199)** — *"Cadoul nu este un voucher și nu este un e-mail automat. Este un obiect sau un ritual, ales anul acesta pentru tine: o sticlă din producția casei, o ședință cu un anume meșter, un coș cu ceaiuri noi, o seară pentru două persoane în baia pe care o iubești. Nu știi ce va fi. Asta face parte."* The colon-then-list (*"o sticlă… o ședință… un coș… o seară…"*) is product-description register. Aman would name one thing or none. The list also violates the page's "no enumeration" rule (Design §4 density rule: lists max 2 lines per item).

4. **Design S08 micro-detail (line 240)** — *"Below that: stamp-style small frame 'INCLUD · ACCES PE VIAȚĂ' (like a passport stamp, `--wol-stamp` reuse but smaller)."* A literal passport-stamp frame is novelty-tier, not Aman-tier. Aman doesn't need a stamp to confirm what an italic Cormorant line just said. Kill the stamp.

---

## D · KILL LIST

1. **Copy C "Body — structură" block (lines 81–89)**: the 10 000 + 40 000 MDL breakdown. It destroys the single-number discipline every reference (Aman, Soho House, Cheval Blanc, Sobha Privy) commits to. *Replace with one italic line: "O singură plată. Acces pe viață."*

2. **Design §6 "Cursor" (line 462–467) AND "Side dots" (line 477)**. Motion §5 explicitly rejected both: they compete with WebGL for attention and break the Aman hush. Keep the top progress bar only. Engineering gets *one* chrome decision, not two contradictory ones.

3. **Design S07's named-object icon set (line 211–219) and copy F's four-bullet operational events list (line 167–179)** — together they produce two competing privilege/event registers. Design says "The Cellar / The Library / The Studio"; copy says "Preț de membru / Camerele private / Rezervarea / Produsele noi". Pick the copy register (functional benefits, no objects) and rewrite design S07 to match. Aman privileges are 4 short italic sentences, not 8 named rooms.

---

## E · PRIORITY FIXES (5 concrete edits)

1. **Copy out.md §C (lines 81–89)** → DELETE the 10 000 + 40 000 breakdown. Replace with one italic Cormorant line: *"O singură plată. Acces pe viață."* Aligned with Design S08's "Single tier, no comparison" rule and Research §4.4.

2. **Design out.md §6 "Cursor" (line 462–467) + "Side dots" (line 477)** → DELETE both. Add a 2-line note in §6 Microinteractions that aligns with Motion §5: *"Top progress bar is the only persistent chrome. No side dots, no custom cursor. The hush is the brand."*

3. **Design out.md §11 (line 312–313) → reconcile 12-vs-3 events.** Decision: 3 signature nights (intimate, named, hosted) + 9 open calendar entries = 12 total. Update Design S10 ring label from "12 — closed events" to *"12 evenimente · 3 închise"* and adjust Copy F (line 160, 169) to match: the headline stays *"Trei nopți pe an"* (poetic register), the body clarifies *"calendarul complet, douăsprezece seri"* once.

4. **Design out.md → INSERT a new micro-section between S07 and S08**, the 42/50 scarcity dot-grid (research §7 Action #1). 50 SVG circles, 42 filled gold, 8 hollow cream, 8px each, 6px gap. Pulsing breath on the 42nd at 6s interval. This is the highest-impact element research identified; missing from all peers.

5. **Motion out.md §7.1 (line 471–495)** → DROP the Fresnel-rim gold arc (`THREE.TorusGeometry` + Fresnel shader). Replace with design S02's spec: FBM fog + a single 1px-wide gold light-shaft ray drifting left→right over 24s. This aligns Motion's canvas with Design's canvas and removes the heaviest shader (the Fresnel pass costs ~6 draw calls + per-fragment math). Per research §1.7, point-light fake 3D is the cheaper 2026 move if any portrait lighting effect is wanted.

---

## F · NEW IDEAS from research, not picked up

1. **Sobha Privy zoom-on-scroll on the 50 000 numeral** (research §1.6, §3.2): combine the count-up motion spec already in place with a scrubbed `scale: 0.85 → 1.0` on the same element as the price card enters. Cost: 8 lines of GSAP, no new library. Implementation: in Motion §4 `animateCounter()`, add `scrollTrigger: { trigger: el, start: "top 80%", end: "top 30%", scrub: 0.6 }` and animate `scale` from `gsap.timeline().to(el, { scale: 1, scrollTrigger: ... }, 0)`.

2. **Codrops SVG-mask hero finale using the existing ornament-diamond** (research §3.4): design S02's hero exit (line 105) currently ends on a subtitle parallax. Replace with an inline `<svg viewBox="0 0 100 100">` rotated-square mask whose `transform: scale(0.04) → scale(80)` is scrubbed to scroll 80vh → 110vh. Hero photo reveals from the diamond outward. The asset is already in v1. Cost: 25 lines of GSAP + 1 SVG node. Implementation hook: Motion §6.1 `buildThreshold()` exit block, line 300–302, *replace* `tl.to("#hero", { autoAlpha: 0 })` with the mask-reveal timeline.

3. **Native CSS `animation-timeline: view()` for the privilege rows** (research §2.2): replace Motion's IntersectionObserver reveal-on-scroll (used implicitly in §1) with the native CSS approach for S07 privilege rows + S09 calendar rows + S06 ritual beats. Fallback via `@supports not (animation-timeline: view())` keeps the GSAP path for older browsers. Implementation: add a single CSS block at `tokens-extensions.css`:

```css
@supports (animation-timeline: view()) {
  .priv-row, .ritual-beat, .event-row {
    animation: wol-reveal linear both;
    animation-timeline: view();
    animation-range: entry 0% cover 30%;
  }
  @keyframes wol-reveal {
    from { opacity: 0; transform: translateY(40px); filter: blur(8px); }
    to   { opacity: 1; transform: none; filter: blur(0); }
  }
}
```

This is 12 lines of CSS, removes IntersectionObserver observers for ~24 DOM nodes, and is the 2026-native-feeling perf win.

---

**Top-line summary:** the page is *almost* Aman but is being held back by (a) copy's two-component price breakdown which kills single-number discipline, (b) motion/design disagreeing on what fills the hero canvas, and (c) the 42/50 scarcity dot-grid — research's highest-impact element — being absent from all three peers. Fix those three and the page earns its restraint.