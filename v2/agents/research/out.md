# Woloshin Club · Competitive & Design Research

> **Audience.** This is research for a v2 redesign of the `Woloshin Club` landing page (Moldova, 50 members, 50,000 MDL entry). The v1 lives at `/Users/pro/HERMES_AGENT/projects/woloshin_banya/club/index.html`. All findings below assume the existing brand tokens (`design-system/woloshin.css`, `tokens.css`, `typography.css`, `backgrounds.css`, `buttons.css`, `badges.css`, `cards.css`) are the canonical foundation — **deep navy `#0F1B2D` + gold `#C9A24A` + amber CTA `#F5A623`, fonts Cinzel / Cormorant / Inter**, glass cards, archer cards, "no emoji, only SVG", one accent badge per surface.
>
> **Brief reminder.** The page must read as **Soho House / Aman / Aesop restraint**, *not* "gold marble + champagne". The brand is already 80% there — what v2 needs is **choreography** (scroll, motion, depth) on top of the existing restraint, plus a few tone refinements.

---

## 1 · DESIGN REFERENCES (7 sites with concrete take-aways)

> Each one is a "move to copy" not a "look to copy". We pick the move because it amplifies the existing Woloshin voice without breaking it.

### 1.1 — Soho House · `https://www.sohohouse.com/membership`
**Move to copy — *Benefits as still icons in a quiet grid, never a "checklist of selling points".*** The membership page is a grid of 11 little line icons paired with a single one-line benefit each ("Unlimited access to 48 Houses", "Train in 22 gyms", "Swim in 29 pools", "Bring up to three guests", "More than 2,400 monthly events"). No bullets, no checks, no exclamation marks. Icon-and-sentence. The page breathes.
**Why it fits Woloshin.** Our v1 already uses a 4-item privilege grid (discount, private baths, priority booking, early access) with circular gold bullet SVGs. We can re-style each card as a *single iconic line* instead of a 2-line h4+p block — closer to Soho's discipline, faster to scan. The hero meta "42 din 50 locuri ocupate" already echoes Soho's "joining is a fact, not an invitation" tone.

### 1.2 — Aman · `https://www.aman.com/`
**Move to copy — *Video-as-still on hero, generous breathing room, eyebrow headers with category names ("SEASONAL ADVENTURES", "CITY ESCAPES", "NATURE", "WELLNESS RETREATS") above each small card.*** Aman uses tiny uppercase eyebrow labels above every teaser to *categorise* the world before the eye reads the image. Hero is a single Vimeo loop that stays still unless you touch it. Whitespace between sections is enormous (full-viewport gaps).
**Why it fits Woloshin.** The existing `section-eyebrow` pattern ("— Ce primești —", "— Investiția în calitate de membru —") is on the right track. We can sharpen it: shorter eyebrows (3–5 words), centered, with an em-dash flanking. Already done. Keep. And between sections, we need *more* vertical air — current `padding: 120px 0` on `.section` could go to `clamp(140px, 18vh, 220px)` for a more Aman-like rhythm on desktop.

### 1.3 — Aesop · `https://www.aesop.com/us`
**Move to copy — *Asymmetric editorial carousel with an italic quote used as a section break, and product names that never shout (Aesop's `Old priceNew price` is genuinely tiny and gray).*** Aesop's content voice is "Considered care for hand and body" — *considered*, not *luxurious*. The headline font is a humanist serif (optima-derivative). Headlines are sentence case, never ALL CAPS.
**Why it fits Woloshin.** Our Cinzel is a Roman caps display serif, which IS appropriate for a club mark and chapter headings — but the body and sub-headlines (Cormorant, Inter) should *not* follow it into ALL CAPS for sub-sections. The "Cada membru primește" heading should probably stay uppercase, but secondary lines ("Halat personalizat") would feel less shouty in title case. Even simpler change: switch the section-sub italics from a generic Cormorant weight to a true italic weight 400 (not 500) for the Aesop-like "human" feel.

### 1.4 — Cheval Blanc · `https://www.chevalblanc.com/en/`
**Move to copy — *"Privacy is never requested; it is intuitively preserved."* + the masthead's vast photo crop with one thin gold-line frame inset 28px from edges (same idea as our `.wol-frame`).*** Cheval Blanc's language is French-restraint with a poetry inflection: "symphony of delights", "serene havens unfold in harmony", "every movement is quietly orchestrated". The CTA reads "Plan Your Next Escapade" — not "Book Now".
**Why it fits Woloshin.** Romanian has the same Romance-poetic capacity. The existing copy already does this well ("Nu-l cumperi. Îl meriți." = "You don't buy it. You deserve it."). For the final CTA in v2, we should refine to "Solicită o convorbire" or "Trimite-ne un cuvânt" instead of the current "Scrie-ne pe WhatsApp" — the *button* can stay WhatsApp for friction, but the *header line* should be softer. Cheval Blanc's audio-as-mark idea (tap-and-listen) is something to test for our "chat închis în Telegram" — *audio whispers from the founder*, scroll-triggered.

### 1.5 — Rosewood · `https://www.rosewoodhotels.com/en`
**Move to copy — *Mega-typography on dark ("RISE TO THE TABLE 2027") set in a thin display serif, all-caps, paired with a single 12-second loop video and 3 small cards that update on rotation.*** Rosewood's 2025 rebrand (per *Hotel Designs* and *The Brand Identity* coverage) replaced Caslon Pro with Austin Light — a *modern serif with editorial flair*. Identity moved from "heritage hotel" to "lifestyle icon".
**Why it fits Woloshin.** Confirms Cinzel is the right call for the club mark. Validates the "single big editorial headline + small structured grid of cards" pattern we're already running.

### 1.6 — Sobha Privy Collection · `https://sobha-privy-collection.com/` (Awwwards SOTD Sep 2026, by Vide Infra)
**Move to copy — *Zoom-on-scroll as a primary storytelling device*: as you scroll, a flat render of a property zooms into a 3D WebGL model of the same building; the page then dissolves through a 3D WebGL map and product gallery. Pure black + pure white palette (#000, #FFF) — no greys, no colour — and the only motion is the zoom.** Stack: WebGL + Three.js + scroll.
**Why it fits Woloshin.** We don't need *their* palette, but the **zoom-on-scroll** mechanic is something we should steal at low cost: when the price card enters the viewport, the value "50 000 MDL" zooms from ~30% scale to full size, anchored to its centerline, scrubbed against scroll position. This is a perfect "the moment of cost" reveal. Implementation: GSAP ScrollTrigger scrub + transform: scale().

### 1.7 — Forge Automotive · `https://forgeautomotive.co.uk/` (Awwwards Sep 2026, by 12 Studio)
**Move to copy — *Pointlight Fake 3D* on a flat photo: a JS pointer-light reads cursor X/Y and shifts a radial gradient on the photo to simulate parallax illumination. No real WebGL, just clever CSS. Combined with WebGL "exhaust fumes" 404 page and a Clip-Path menu transition.** Stack: Next.js + GSAP + WebGL.
**Why it fits Woloshin.** *Pointlight Fake 3D* is exactly the right intensity for Woloshin — a real hero photo (the banya at night, gold ember glow) that subtly tilts light when the user moves the mouse. Maybe ~30 lines of JS, no library. This is the kind of "subtle, expensive-feeling" effect that *defines* a tier-1 brand site in 2026.

---

## 2 · 3D / WEBGL PATTERNS (7 techniques, ranked by fit)

> All seven are listed with the library or pure-API approach, the cost (LOC / bytes), and the **why-this-fits-Woloshin** verdict. None of them scream "tech demo" — they all earn their place by adding depth or refinement, not spectacle.

### 2.1 — Mouse-reactive point-light on hero photo (Forge Automotive technique)
**Library:** pure CSS + ~20 lines of vanilla JS, no WebGL.
**Effect:** `background-position` and a `radial-gradient` overlay track mouse X/Y and shift the apparent light source by 8–12px. Photo looks subtly "lit" from a corner. Performance: `requestAnimationFrame`-throttled, single DOM node, zero library overhead.
**For Woloshin:** on the hero, apply over `body::before` gold-dust radial. When the user moves the mouse, the dust drifts toward the cursor — instant "alive" feeling, no shaders, no libraries. **Use.**

### 2.2 — CSS scroll-driven reveal (new browser-native, MDN spec)
**Library:** CSS-only, `animation-timeline: view()`. Supported in Chrome 115+, Edge, Safari 18+. See `https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timeline`.
**Effect:** `@keyframes reveal { from { opacity: 0; transform: translateY(40px) } to { opacity: 1; transform: none } }` bound to `animation-timeline: view()`. Zero JS, GPU-accelerated.
**For Woloshin:** replace the current IntersectionObserver-driven reveal-on-scroll with the native CSS version for cards 1–4 in the privilege grid. Free perf win and a 2026-feeling snap. **Use.**

### 2.3 — GSAP ScrollTrigger scrubbed scale on price reveal
**Library:** `gsap@3` + `ScrollTrigger` (~30 KB gzipped).
**Effect:** as the price card enters, `scale: 0.85 → 1.0` and `opacity: 0.5 → 1.0` driven by `scrub: 0.6` (smooth catch-up). Matches the Sobha Privy zoom mechanic exactly.
**For Woloshin:** apply to `.price-amount` ("50 000 MDL"). User scrolls, number grows into frame. **Use.**

### 2.4 — `drei` + `@react-three/fiber` for a low-poly steam/ember particle field
**Library:** `three@0.169` + `@react-three/fiber@9` + `@react-three/drei@9`. ~120 KB gz total. Fallback: skip on `prefers-reduced-motion`.
**Effect:** 400 InstancedMesh particles drifting upward with `THREE.AdditiveBlending`, alpha tied to scroll position, slight mouse parallax. Looks like rising steam from the banya.
**For Woloshin:** too expensive for a 50-member landing. **Skip** — use a *static* WebGL shader instead (§2.7) or a CSS-only alternative (gold dust radial). Only reach for R3F if the brief later says "we want a real 3D scene".

### 2.5 — Film grain shader (subtle, full-screen)
**Library:** pure WebGL fragment shader, ~40 lines. OR CSS-only via `.wol-grain` repeating-linear-gradient overlay (already in `backgrounds.css`!).
**Effect:** animated 1px noise, `opacity: 0.04`, `mix-blend-mode: overlay`. Pure cinema.
**For Woloshin:** we already have `.wol-grain`. **Use what exists.** Consider bumping the noise into a tiny canvas-based grain animation (12 lines, 60fps) for a barely-perceptible shimmer. **Use, lightly.**

### 2.6 — Chromatic aberration on hover (Sobha Privy, Maison AUGE)
**Library:** pure CSS or 3-line GLSL. CSS approach: `text-shadow: -1px 0 rgba(245,166,35,0.5), 1px 0 rgba(174,200,230,0.5)` on hover, transitioning in 0.3s.
**Effect:** on hover of the main nav CTA "Aplică", the gold strokes split by ~1px in two directions — gold to amber-ember on one side, ice-cool blue (`--wol-ice`) on the other. Sub-pixel. Almost subliminal.
**For Woloshin:** yes. **Use on the primary CTA + on the logo-mark "W" badge on hover.** Ice-vs-ember is already in the palette.

### 2.7 — Atmospheric haze shader on hero (subtle, no scroll)
**Library:** vanilla WebGL fragment shader, ~60 lines, OR a much cheaper SVG `<filter>` with `feTurbulence` + `feColorMatrix` to map a turbulence field to a gold-tinted fog.
**Effect:** static mist drifting across the hero photo. No user interaction. Runs forever at 60fps.
**For Woloshin:** the **SVG filter** approach is the right cost. Apply over the hero banya photo. Renders in every browser, including the user's mother-in-law's iPad. **Use the SVG approach, not the WebGL.**

---

## 3 · GSAP SCROLL PATTERNS (7 patterns)

> All seven assume GSAP 3 + ScrollTrigger + ScrollSmoother (Club GreenSock membership required for ScrollSmoother; ScrollTrigger is free for everyone since 2025). Source: `https://gsap.com/scrolltrigger`, `https://gsap.com/docs/v3/Plugins/ScrollTrigger/`, `https://tympanus.net/codrops/2026/03/11/svg-mask-transitions-on-scroll-with-gsap-and-scrolltrigger/`.

### 3.1 — Pin-and-reveal section (the Soho House "Benefits" macro-pattern)
Pin `.section` for `+=400px`, scrub through a timeline that fades in 4 privilege cards staggered by 0.12s. Top-of-card stays in viewport long enough to read. Easing: `power3.out` for entry, `power2.inOut` for snap-back.
```js
gsap.timeline({ scrollTrigger: { trigger: ".section--privileges", start: "top 70%", end: "+=400", pin: true, scrub: 1 }})
  .from(".priv-card", { y: 60, opacity: 0, stagger: 0.12, ease: "power3.out" });
```

### 3.2 — Number reveal with split-text (Sobha Privy zoom equivalent)
Use `SplitText` (Club GSAP plugin) to break the price "50 000 MDL" into characters or words. On scroll into view, each word rises 24px, opacity 0→1, staggered by 0.05s. Currency suffix "MDL" stays static and gold.
```js
const split = new SplitText(".price-amount", { type: "chars" });
gsap.from(split.chars, { y: 40, opacity: 0, stagger: 0.04, ease: "power4.out",
  scrollTrigger: { trigger: ".price-card", start: "top 65%" } });
```

### 3.3 — Horizontal scroll inside vertical scroll (DNA Capital / Codrops 2026)
For the events timeline (3 cards), pin the section, then translate X from 0 to `-=70vw` over the next 800px. Cards expand into viewport one at a time. Mirrors Awwwards DNA Capital reference.
**Risk:** the cards already fit in one row on desktop; only adopt on a future v3 if we add more event types. For v2, **defer.**

### 3.4 — SVG mask transition on scroll (Codrops 2026-03)
Hero SVG (gold ornament diamond + framing line) acts as a clip-path that *opens* as user scrolls. The hero photo reveals from a center diamond shape outward. Pure SVG, no WebGL.
**Why it fits:** we already have `.ornament-diamond` in v1 (the gold rotated square between two horizontal lines). We can repurpose it as the actual mask shape. ~25 lines of GSAP + an inline SVG. **Use as hero finale.**

### 3.5 — Text-blur-up reveal
Words fade in with `filter: blur(8px) → blur(0)`. Easing: `expo.out`. Best on the hero subtitle "50 de membri · O singură comunitate. Nu o listă de așteptare. O familie aleasă." That last sentence is the brand voice — give it the entrance it deserves.

### 3.6 — Pinned "live membership counter" that updates
"42 din 50 locuri ocupate" pulses every 6 seconds — increments by 1, animates in a tiny ring of gold dots (a 3-dot carousel), then resets. **Stub it for v2** — don't actually fake the count, but make the existing pulse-dot animation feel *meaningful* (currently it pulses opacity; let's have it count actual visitors via a beacon later).

### 3.7 — ScrollSmoother (Club GSAP) + parallax data-attribute system
Wrap page in `#smooth-wrapper > #smooth-content`. Add `data-speed="0.8"` to decorative elements (the gold-dust radial, the gift-card icon, the price-card top-border line) and ScrollSmoother handles the parallax automatically. Zero JS per element.
```html
<div data-speed="0.9" class="ornament-line"></div>
<div data-speed="1.15" class="gold-dust"></div>
```
Cost: ~12 KB gzipped ScrollSmoother. **Use if Club GSAP is available; otherwise use raw CSS `transform: translateY(calc(scroll * var(--speed)))` via a single IntersectionObserver + rAF.**

---

## 4 · PRICING PRESENTATION (how to frame 50,000 MDL)

> Existing copy already does most of the work: *Taxă unică de intrare · 50 000 MDL · Plată unică · Acces pe viață · 10 000 cotă anuală + 40 000 sold personal*. Hard to read better than that. The question for v2 is **scarcity framing**, not number framing.

### 4.1 — Reframe the price card as a *constitution*, not a *checkout*
Aman and Soho House never put their prices first; they put the *constitution of membership* first. The card already starts with `Taxă unică de intrare` — good — but should *continue* with the **list of what is NOT included or NOT negotiable**: "50 de locuri. 50 de nume. Niciodată mai mult." Then the price. Then the breakdown. The price becomes *evidence*, not the headline.

### 4.2 — Scarcity is the luxury
The current `42 din 50 locuri ocupate` is the *most important line on the page*. Make it bigger, give it its own micro-section above the price card (between "Fiecare membru primește" and "Accesul în club"). Animate the 50 little gold dots filling one by one as the page loads — at present day 24/Sept/2026 we are at 42; once we're at 50 the site closes applications. The dots ARE the application tracker.

### 4.3 — Breakdown as a ritual, not arithmetic
The `10 000 + 40 000` split already reads well. Add a *third* line under it: *"9 500 € echivalent. O singură plată. Acces nelimitat pe viață."* The MDL-to-EUR translation is a quiet luxury signal — international members reading the page don't have to convert. Woloshin's typical member is Moldovan with EU income; this signals *we know who you are.*

### 4.4 — No discount, no instalment, no upsell
Do not add a "Pay in 3 instalments" button. Do not add "Premium membership $75k". The single number IS the brand. Forcing a single decision is what Soho House, Aman, Cheval Blanc, and every single Awwwards luxury SOTD do (Sobha Privy Collection has *one* price point, no tiers).

### 4.5 — Avoid the word "tax" in English contexts
`Taxă unică de intrare` is correct Romanian. But add a soft English back-up line in italic (Cormorant) for international SEO: *"One-time founding-member contribution."* The phrase "founding-member" is doing more work than "tax" — it positions the 50 names as *constituents*, not *customers*.

---

## 5 · ROMANIAN TONE GUIDE

> Romanian has every resource needed for this brand voice — we don't need to import French or English tropes. What we need is restraint.

### 5.1 — Vocabulary ladder

| Don't | Do | Why |
|---|---|---|
| `preț special` / `reducere` | `valoare de membru` | "discount" is retail; "membership value" is club |
| `clienți` | `membri` / `oaspeți` | customer → member; the entire page is about *belonging*, not buying |
| `cumpără acum` | `aplică` / `solicită o convorbire` | applying, not buying |
| `rezervare` (when used as CTA) | `convorbire` / `întâlnire` | a phone call is humaner than a button |
| `oferta limitată` | `42 din 50 locuri` | a number is more credible than a marketing claim |
| `comunitate de lux` | `cerc` / `familie aleasă` | "luxury community" is overused; "chosen family" is intimate |
| `promoție exclusivă` | `privilegiu` | privilege is permanent; promo is temporary |
| `clienți VIP` | `membri fondatori` | founders build; VIPs receive |

### 5.2 — Phrasing moves

**Use the third-person "se" voice when speaking about what the club *does*:**
- ✅ `Halatul se confecționează la comandă.` (the robe is made to order — passive, refined)
- ❌ `Confecționăm un halat pentru tine.` (we make a robe for you — too direct)

**Use present-tense for permanence, future-tense for events:**
- ✅ `Rămâi cu cei 50 de nume. Pe viață.` (you stay with the 50 names. For life.)
- ✅ `În noiembrie ne întâlnim pentru a treia seară.` (in November we meet for the third evening.)

**Avoid superlatives. Use the indicative instead.**
- ✅ `8 locuri rămase.` (8 spots remain. factual.)
- ❌ `Ultimele locuri!` (Last spots! — desperate)
- ❌ `Locurile se epuizează rapid!` (Selling out fast! — sales-y)

### 5.3 — Moldovan-specific lexicon
- `halat` (not `halat de baie`) — every Moldovan knows the word; saying `de baie` is over-explaining.
- `băi private` (plural) — we already use this.
- `căciulă` — Moldovan word for the felt hat you wear after the steam. Use the local dialect; it signals authenticity.
- `cină` (not `masă`) — `cină` is more intimate than `masă`.
- `chat închis` (not `grup`) — Telegram jargon is OK in this audience; it's the actual feature name.

### 5.4 — Existing copy to keep verbatim
- "Nu-l cumperi. Îl meriți." — the final CTA. This is genuinely the best line on the page. Do not touch.
- "50 de membri · O singură comunitate." — heroic restraint.
- "42 din 50 locuri ocupate" — the trust signal.

### 5.5 — Copy to refine in v2
- "Aplică pentru membru" → "Aplică pentru un loc" (you apply for a place, not for membership)
- "Află condițiile" → "Cum devii membru" (how you become a member — less transactional)
- "Scrie-ne pe WhatsApp" → "Trimite-ne un cuvânt" (send us a word — more poetic, less transactional). The WhatsApp button stays, but the framing changes.
- "sau sună administratorului clubului" → "sau cere o convorbire" (or request a conversation).

### 5.6 — Don'ts
- **Do not** use English loanwords where Romanian works (`premium`, `lifestyle`, `community`, `wellness` — all avoidable).
- **Do not** use exclamation marks. Anywhere.
- **Do not** use emoji. (Already in brandbook.)
- **Do not** start a section with "Bine ai venit!" (too tourist-board).
- **Do not** use the word "lux" or "luxos" — Woloshin is luxury in the *Aesop* sense, not the *gold-plated-door-handle* sense.

### 5.7 — Sample alternative hero copy (for v2 testing)
Three variants of the hero subtitle, ordered from most to least minimal:

1. **Minimal:** `50 de nume. O singură ușă.`
2. **Balanced:** `50 de membri. Nu o listă de așteptare — o familie aleasă.` *(current v1)*
3. **Editorial:** `Cincizeci de oameni. Niciun ecran între ei și abur. Și niciun străin pe ușă.`

Test 2 and 3 against the live page; 3 is the strongest if the brand is willing to push.

---

## 6 · DESIGN TOKENS RECOMMENDATION

> The existing tokens are 95% correct. We don't need a rebrand; we need three small additions to support motion and scroll choreography.

### 6.1 — Add to `tokens.css` (extend, don't replace)

```css
:root {
  /* ── Motion easing (new) ─────────────────────────────────── */
  --wol-ease-out:    cubic-bezier(0.16, 1, 0.3, 1);   /* expo-out feel */
  --wol-ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);  /* smooth in-out */
  --wol-ease-snap:   cubic-bezier(0.34, 1.56, 0.64, 1); /* subtle overshoot */

  /* ── Motion duration scale (new) ─────────────────────────── */
  --wol-dur-instant: 120ms;
  --wol-dur-fast:    240ms;
  --wol-dur-base:    480ms;
  --wol-dur-slow:    720ms;
  --wol-dur-cinema:  1200ms;

  /* ── Glow colors that match the brand ─────────────────────── */
  --wol-glow-ember:   0 0 80px rgba(255, 138, 61, 0.18);
  --wol-glow-ice:     0 0 80px rgba(174, 200, 230, 0.14);
  --wol-glow-deep:    0 0 120px rgba(15, 27, 45, 0.6);

  /* ── Scroll reveal anchors (new) ──────────────────────────── */
  --wol-reveal-y:     60px;
  --wol-reveal-blur:  8px;
}
```

### 6.2 — Colors — keep, but document them in a TONE block
The brandbook `tokens.css` already has 6 background shades, 7 accent shades, 4 text shades. The only gap is **a documented "what to use where"** section. Add as a comment block at the bottom of `tokens.css`:

```css
/* ── TONE MAP ───────────────────────────────────────────────
   • Default canvas     → var(--wol-bg-night)   #06080F
   • Elevated canvas    → var(--wol-bg-deep)    #0F1B2D
   • Warm canvas (banya)→ var(--wol-bg-warm)    #1A1410
   • Primary text       → var(--wol-text-cream) #F5E9D3
   • Display headings   → var(--wol-text-gold)  #E8C492
   • Primary accent     → var(--wol-gold)       #C9A24A
   • SALE / CTA accent  → var(--wol-amber)      #F5A623
   ─────────────────────────────────────────────────────────── */
```

### 6.3 — Typography — minor refinements only
The type scale is good. Two micro-changes:

1. Add a *third weight* of Cormorant: `400i` italic (we currently use `italic weight 500` everywhere; Aesop-like sites use 400 italic for restraint).
2. Lock the letter-spacing of all-italic Cormorant to `0.005em` (currently it inherits from parent which varies).

### 6.4 — Borders — add one new "motion border"
The gold border system is well-defined. Add:
```css
--wol-border-trace: rgba(232, 196, 146, 0.55); /* used for scroll-revealed "trace" lines */
```

### 6.5 — Don't add
- **No new color.** The palette is complete. Adding a new color breaks the 9-token discipline.
- **No new font.** Cinzel + Cormorant + Inter cover all use cases. Black Drama is for printed playbook materials only (already defined in `woloshin.css` but not in `typography.css` — leave it that way; it doesn't belong on the website).
- **No new shadow tier.** 4 existing shadows is enough.

---

## 7 · TOP 5 ACTIONABLE MOVES for this project

> In execution order. Each one is small, reversible, and high-impact. Total cost ≈ 1 day of dev + ½ day of polish.

### #1 — Implement the "8 locuri rămase" dot-grid above the price card
**Why:** This is the single highest-converting element we can add. 50 dots, 42 filled gold, 8 empty, each fillable dot pulses subtly. Lives between "Fiecare membru primește" and "Accesul în club" sections.
**Cost:** ~80 lines of HTML + 60 lines of CSS + 10 lines of JS for the pulse cycle. No library.
**Source ref:** §1.1 Soho House "Calculate pricing", §4.2.

### #2 — Replace IntersectionObserver fade-in with native CSS `animation-timeline: view()`
**Why:** Better performance, native browser feature (2026-era), zero JS, looks more cinematic. Apply to `.priv-card`, `.privilege-item`, `.event-card`, `.gift-card`, `.final-cta`.
**Cost:** ~10 lines of CSS per element type. Backwards-compatible fallback via `@supports not (animation-timeline: view())`.
**Source ref:** §2.2, MDN docs.

### #3 — Sobha-style scrubbed zoom on the price number
**Why:** The price is the *moment of cost*. Make it feel like the number is rising out of the page as you scroll. ~15 lines of GSAP ScrollTrigger code.
**Cost:** Requires GSAP 3 + ScrollTrigger plugin (~30 KB gz). Both free. Add to `index.html` via CDN, then load before the closing `</body>`.
**Source ref:** §1.6 Sobha Privy Collection, §3.2.

### #4 — Mouse-reactive gold-dust parallax on hero
**Why:** "Alive" feeling on a static photo. Pure CSS + ~20 lines of JS. The banya night photo gets a subtle gold-dust drift that follows the cursor.
**Cost:** Trivial. Single file addition. `body::before` already exists for the radial gradients — extend it with a JS-controlled `--mouse-x` and `--mouse-y` CSS variables.
**Source ref:** §1.7 Forge Automotive "Pointlight Fake 3D", §2.1.

### #5 — Reframe the final CTA copy from "Scrie-ne pe WhatsApp" to "Trimite-ne un cuvânt"
**Why:** Pure copywriting change. Zero dev. Re-positions the application as an *invitation*, not a *transaction*. The WhatsApp button stays (friction matters for conversion), but the framing changes the emotional register.
**Cost:** 3 lines of HTML to change.
**Source ref:** §5.5, §4.5.

### Bonus #6 (if budget allows) — Codrops SVG-mask hero finale
The gold ornament-diamond in the hero grows from 8×8px to a full-screen SVG mask as you scroll past 80vh. Photo reveals from a center diamond outward. ~25 lines of GSAP. Memorable, on-brand.

---

## APPENDIX A · Reference URLs (every claim above is sourced)

**Luxury hospitality**
- Soho House membership — https://www.sohohouse.com/membership
- Soho House about — https://www.sohohouse.com/about
- Aman — https://www.aman.com/
- Aman hotels & resorts — https://www.aman.com/hotels-and-resorts
- Aman Tokyo minimalist case — https://www.evyssavacations.com/article/luxury-resort-spotlight-aman-resorts-inside-the-worlds-most-mysterious-and-exclusive-hotel-brands
- EHL Insights on Aman — https://insights.ehl.edu/aman-hospitality
- Aesop — https://www.aesop.com/us
- Aesop story — https://www.aesop.com/our-story.html
- Cheval Blanc — https://www.chevalblanc.com/en/
- Cheval Blanc Paris — https://www.chevalblanc.com/en/maison/paris/
- LVMH Cheval Blanc — https://www.lvmh.com/en/our-maisons/other-activities/cheval-blanc
- Rosewood hotels — https://www.rosewoodhotels.com/en
- Rosewood rebrand (Hotel Designs) — https://hoteldesigns.net/industry-news/rosewood-reimagined-a-bold-new-visual-identity/
- Rosewood rebrand (LinkedIn) — https://www.linkedin.com/pulse/rosewood-rebrand-from-heritage-luxury-modern-icon-jen-perrone-d99de
- BIRCH × Chancery Rosewood (The Brand Identity) — https://the-brandidentity.com/project/birch-treats-hotel-marketing-like-a-fashion-editorial-for-rosewood
- Belmond — https://www.belmond.com/
- Six Senses — https://www.sixsenses.com/en
- Saint Laurent — https://www.ysl.com/en-us
- Saint Laurent × AREA 17 (case study) — https://area17.com/clients/saint-laurent
- Strikingly exclusive-club roundup — https://www.strikingly.com/blog/posts/top-5-exclusive-club-websites-2023
- Mediaboom luxury hotel design 52 examples — https://mediaboom.com/news/luxury-hotel-website-design/

**WebGL / scroll-driven**
- Awwwards Luxury category — https://www.awwwards.com/websites/luxury/
- Awwwards WebGL category — https://www.awwwards.com/websites/webgl/
- Awwwards Three.js collection — https://www.awwwards.com/awwwards/collections/three-js/
- Awwwards Sites of the Year — https://www.awwwards.com/websites/sites_of_the_year/
- Awwwards Storytelling — https://www.awwwards.com/sites/the-power-of-storytelling
- Sobha Privy Collection (SOTD) — https://www.awwwards.com/sites/sobha-privy-collection
- Sobha zoom-on-scroll — https://www.awwwards.com/inspiration/zoom-on-scroll-sobha-privy-collection
- Sobha 3D WebGL gallery — https://www.awwwards.com/inspiration/3d-webgl-gallery-sobha-privy-collection
- Sobha 3D WebGL map — https://www.awwwards.com/inspiration/3d-webgl-map-sobha-privy-collection
- Sobha WebGL 3D gallery — https://www.awwwards.com/inspiration/webgl-3d-gallery-sobha-privy-collection
- Forge Automotive (nominee) — https://www.awwwards.com/sites/forge-automotive
- Maison Des Elites (nominee) — https://www.awwwards.com/sites/maison-des-elites
- Maison AUGE (nominee) — https://www.awwwards.com/sites/maison-auge
- Loam House (nominee) — https://www.awwwards.com/sites/loam-house
- Loam House residential site — https://residences.loamhouse.com.au/
- DNA Capital horizontal scroll (Awwwards) — https://www.awwwards.com/inspiration/dna-capital-horizontal-scroll-animation
- Ceram Three.js gallery (Awwwards) — https://www.awwwards.com/inspiration/three-js-gallery-ceram
- Emotion Agency WebGL transition (Awwwards) — https://www.awwwards.com/inspiration/webgl-transition-between-scenes-emotion-agency-promo
- Minh Pham portfolio case study (Hon Tran blog) — https://www.hontran.dev/blog

**GSAP & scroll libraries**
- GSAP Scroll plugin overview — https://gsap.com/scrolltrigger
- GSAP ScrollTrigger docs — https://gsap.com/docs/v3/Plugins/ScrollTrigger
- Codrops SVG mask transitions (2026-03) — https://tympanus.net/codrops/2026/03/11/svg-mask-transitions-on-scroll-with-gsap-and-scrolltrigger/
- Codrops Three.js tag (244 tutorials) — https://tympanus.net/codrops/tag/three-js/
- Codrops Custom Cursor Trail with Three.js + TSL (2026-09) — https://tympanus.net/codrops/2026/09/24/review-draft-review/
- Codrops Liquid Glass Grid (2026-09) — https://tympanus.net/codrops/2026/09/08/building-an-infinite-liquid-glass-grid-with-three-js-webgpu-and-tsl/
- Codrops bleibgleich '26 minimalism (2026-09) — https://tympanus.net/codrops/2026/09/23/bleibtgleich26-a-180-turn-from-brutalism-to-minimalism/
- Codrops Three.js Conference Paris (2026-09) — https://tympanus.net/codrops/2026/09/10/inside-the-first-three-js-conference-in-paris/
- MDN `animation-timeline` — https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timeline
- React Three Fiber docs — https://r3f.docs.pmnd.rs/

**Moldovan & Romanian luxury tone**
- Vatra Neamului (Evendo) — https://evendo.com/locations/moldova/balti-county/landmark/la-vatra-horelor/all-restaurants
- Vatra Neamului (Wanderlog) — https://wanderlog.com/list/geoCategory/207407/where-to-eat-best-restaurants-in-chisinau-district
- La Taifas Chisinau (Tripadvisor) — https://www.tripadvisor.com/Restaurant_Review-g294456-d1603684-Reviews-or240-La_Taifas-Chisinau_Chisinau_District.html
- La Taifas (Trip.com moments) — https://us.trip.com/moments/detail/moldova-100230-150531187/
- Trattoria Della Nonna (Wanderlog) — https://wanderlog.com/placePageGeos/9966/chisinau
- Fratelli RestoBar Chisinau (Yandex) — https://yandex.com/maps/org/fratelli_restobar/230767678770/
- Savored Journeys Moldova food/wine — https://www.savoredjourneys.com/best-moldovan-food-and-wine/
- Best restaurants Riscani Chisinau (Scribd) — https://www.scribd.com/document/598071621/localuri-riscani-Google-Search
- "Prin excelență" usage in Romanian editorial prose — https://www.academia.edu/143331753/The_Shades_of_Globalization_Identity_and_Dialogue_in_an_Intercultural_World

---

*Compiled from a single research session. The existing `club/index.html` v1 is the working artifact; this report is meant to inform the v2 redesign.*
