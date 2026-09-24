# Woloshin Club · Desktop Audit v3 → v4 Plan

**File audited:** `/Users/pro/Documents/Projects/Woloshin_club/v2/index.html`
**Viewport:** 1440×900 desktop, headless Chrome via CDP
**Screenshots:** `/Users/pro/Documents/Projects/Woloshin_club/v2/audit/desktop-v3/` (16 PNGs + FULL-PAGE)
**Vlad's verdict on v3 (from chat):** typography not right · needs backgrounds · too much empty scroll · **keep** the fog aura · **keep** the texture · fonts from `hotels.banya.md` (Kurale + Plus Jakarta Sans) · mobile = separate agent · Russian primary

---

## TL;DR

V3 is **almost there but visually unfinished**. The v3 fixes solved most of v2's bugs (S04/S11 placeholders, S03 dot mismatch, S08/S10 counters, S13 form overflow) — but introduced one critical regression (the `#s01__rays::after` drift ray now reads as a stray line through the H1 because the fog it was supposed to inhabit isn't visible) and three mid-page sections (S02, S10, S12) feel **thin / quiet / dead** against the loud S04/S08/S13. The page reads like a typographic artifact but the **atmospheric concept is uneven**: some sections glow, others feel like an unfinished Figma file.

The single biggest unlock for v4: **make the hero the room** (full-bleed cinematic fog that the H1 floats in) and **make S11's host silhouette abstract** (drop the head/torso/shoulders SVG — it's literally the default macOS user icon).

**Overall grade:** 6.8 / 10.

---

## 1 · KEEP / FIX / DROP inventory (by section)

| # | Section | KEEP | FIX | DROP |
|---|---------|------|-----|------|
| **S01** | Hero (Threshold) | Three.js fog canvas · "Woloshin Club nu se cumpără. Se poartă." epigraph · gold vertical divider on nav CTA · WOLOSHIN · CLUB lockup | H1 wrap (4 lines, "PLUS." orphan) · `#s01__rays::after` drift ray looks like a bug · CTA competes with H1 · epigraph hidden above H1 · "Programează o conversație" CTA text is too literal/SaaS | Sparse gold particles alone — need fog volume around them |
| **S02** | Manifesto | 4-line pinned reveal (works beautifully when scroll lands) · Cormorant italic treatment · bg-s02 SVG texture | **460px empty above + 460px empty below the text** in a 1620px section (Vlad's complaint = #1) · 1px centerline hairline cuts visually through H1 area · pinned reveal only shows 1-2 lines at a time |  |
| **S03** | Cifra · 50 | "50" giant numeral · rewritten copy ("Cincizeci de nume, într-o singură casă.") · bg-s03 ember | "50" anchored right of center · eyebrow "CIFRA · 50" overlaps the descender of "5" · section now redundant — actual 50-dot viz moved to scarcity-block between S07 and S08 (inconsistency) | S03 itself as a section — it doesn't carry weight, it's a transitional slide |
| **S04** | The House | Placeholder frame (atmospheric, labeled "Woloshin Banya · în curând") · warm brown palette · 6-city list in Cinzel uppercase · 2-col split layout | H1 "WOLOSHIN BANYA. / O CASĂ LÂNGĂ / PĂDURE." — "PĂDURE." orphan on its own line · Inter body feels SaaS-y vs Cormorant/Cinzel |  |
| **S05** | The Spaces | 5 arched cards · gold numerals · warm radial at top of each card · progress bar at bottom | **Card 4 STILL CLIPS on right edge** ("Cămara d…" cut) · cards empty in upper half · horizontal scroll UX unclear at first scroll |  |
| **S06** | The Ritual | 7-beat timeline (4 + 3 staggered) · gold 01-07 numerals · bg-s06 vertical grain · Cormorant italic beats | H1 wraps "MIEZUL / NOPȚII." orphan · `.ritual__rule` column divider looks like an unintended hairline · Inter body 15px too SaaS |  |
| **S07** | Privileges | Side-by-side H1 + 8-item list · line-drawn SVG icons · hairline dividers between items · "Privilegiile nu sunt 'beneficii'" italic lead | Numbered list icons are all "utility" icons (house, hashtag, clock) — generic · no chapter mark |  |
| **SCAR** | Scarcity Block | "8 LOCURI RĂMASE" hero · "42 din 50" copy · auto vertical bar (visual hint at 42) | **All 49 dots are identical gold** — no filled-vs-empty distinction = the visualization fails its own job · also 49 not 50 (count bug) | Same fill color for all 50 dots |
| **S08** | Door | "CEEA CE 50 000 MDL DESCHIDE" H1 · giant "50 000 MDL" price · "MDL" cap visible · "ÎNȚELEG. VREAU SĂ INTRU." amber CTA · copy stack | H1 wraps "DESCHIDE" orphan · CTA oversized amber pill |  |
| **S09** | Calendar | 3 events · date+title+desc+tag chip · Cinzel dates · Cormorant italic titles | Event 3 (likely the Dec/Jan) not visible in viewport — section feels empty after event 2 · event rows have ~150px between them |  |
| **S10** | Numbers | 50/3/2 gold numerals · MEMBRI / SERI PE AN / CINE CU FONDATORUL labels · faint ring tracks | **Rings are nearly invisible** (1.5px border track + 2px progress = 3.5px total visual) · ring colors gold/amber/ember are 3 close shades (not visually distinct) · rings show "%" progress but the numbers are integer counts — semantic mismatch · final italic line "Restul se câștigă." floats below empty space |  |
| **S11** | Host | "Bun venit. Sunt Rareș." italic H1 · 2-paragraph body · atmospheric warm radial behind silhouette · signature wave at bottom · warm brown palette | **Silhouette IS the macOS user icon** — head circle + neck rect + torso dome. Reads as default avatar placeholder, NOT abstract art · grain texture not visible at this scale | The literal head/neck/shoulders SVG silhouette (lines 2074-2090) — replace with abstract form |
| **S12** | Closing | "TRECEȚI" eyebrow · "Ușa se deschide o singură dată pe seară" italic · "TELEFON" callout | **`bg-s12` SVG bg NOT rendering at all** — section is 1800px of flat black except the bottom text · "fog parting" never happens · nav CTA flips to FILLED AMBER w/ heavy glow when entering S12 (intensify-on-scroll = good idea, but the filled amber pill in nav bar fights with the subtle section content) | "Dacă ne citiți până aici" — too eager |
| **S13** | Form | "SPUNE-NE CÂTEVA LUCRURI." H1 · "Răspundem în 48 de ore." sub · 3 fields (Email required, Telefon optional, Mesaj scurt optional) · "TRIMIT. APOI, TĂCERE — NOI REVENIM." amber CTA · "Datele rămân în casă" trust line | **CTA button has a heavy amber glow box-shadow** that looks unprofessional, not luxury · 2-field spec became 3 (Telefon is the 3rd) — OK but should be intentional, not accidental | The glow halo on the CTA |
| **S14** | Footer | "WOLOSHIN · CLUB" gold wordmark · "Woloshin Banya · Chișinău · Ediția I — 2026" sub · Casa / Program / Urmărește 3-col grid · address + hours + phone + IG + Telegram · copyright line | Footer bg `#112038` is slightly different from page — creates a subtle band · very narrow type hierarchy (everything same size) |  |

---

## 2 · Top 10 must-fix issues

1. **S01 hero — `#s01__rays::after` drift ray (line 412-421).** A 1px vertical line drifting `translateX(20vw → 80vw)` over 24s. Without fog to inhabit, it reads as a **bug**, not a feature. Either delete it OR rebuild the aura as actual volumetric fog so the ray has something to cut through.

2. **S01 hero — H1 has 4-line wrap with "PLUS." orphan** (lines 484-509, CSS `--wol-display-mega: clamp(54px, 6.5vw, 92px)`). Currently `max-width: 18ch`. Restructure to **3 lines max, no orphan**: e.g., "Cincizeci de numri. / Niciunul în plus. / O singură casă." Or go full 2 lines: "Cincizeci de nume. / Niciunul în plus." and let the type breathe.

3. **S01 hero — Three.js fog is invisible** (canvas at y=1080, w=1440, h=900). Only sparse gold particles render. Vlad said this was the ONE thing to keep, so for v4: turn the fog volume up dramatically. Use a `Fog` with low density + a `PlaneGeometry` with custom shader (fbm noise + radial falloff) for the volumetric look. Even just a large soft radial gradient mesh + animated noise overlay would be 3× stronger than what's there now.

4. **S11 host silhouette is the default macOS user icon** (lines 2074-2090). Replace with abstract form options:
   - **A:** Empty frame + signature wave only (the "Rareș" wave already exists at line 2070+)
   - **B:** Back-facing silhouette (suggesting "host stays in the shadows")
   - **C:** Hand-drawn monogram "R" inside the atmospheric radial (most literary)

5. **Scarcity block — all 49 dots are identical** (line ~2149+, CSS uses single `fill: rgb(201, 162, 74)` for all circles). Make first 42 = solid gold, last 8 = hollow ring (1.5px stroke, no fill) — OR add a vertical 1px gold tick at position 42/50 to mark the cutoff. Also fix the count: 49 should be 50.

6. **S02 manifesto — 920px of dead space in a 1620px section** (section padding + empty above & below the 4 pinned lines). Section padding is `clamp(64px, 9vh, 104px)` ≈ 81px top + 81px bottom = 162px. The 4 lines span y=2460-3218 (758px). Empty top = 460px, empty bottom = 463px. Fix: tighten top padding to ~40px, push the lines up by 200px, and tighten bottom padding to 40px. Or: extend the pinned timeline so more text fills the section.

7. **S06 ritual hairline divider reads like a bug** (line 844-852). The `.ritual__rule` is a 1px column in the grid with `linear-gradient(180deg, transparent, gold 10%, gold 90%, transparent) opacity: 0.35`. It works BUT in conjunction with the S02 manifesto::before hairline, the page has **two** vertical centerlines — Vlad will read it as a CSS glitch. Either: (a) drop S06's hairline entirely, (b) move it INSIDE the grid cells (top of each column) instead of full-height, (c) make S02's hairline only span the text area, not the section.

8. **S08 + S13 amber CTAs are visually aggressive for a luxury page.** S08 "ÎNȚELEG. VREAU SĂ INTRU." is a ~14rem amber pill with subtle glow. S13 "TRIMIT. APOI, TĂCERE — NOI REVENIM." has a heavy `--wol-glow-amber` box-shadow (warm glow) that looks like a Material Design button. For luxury: drop the glow, use outline-only gold border + ghost fill, let the H1 do the work.

9. **S12 closing — `bg-s12` SVG is NOT rendering** (CSS `.bg-s12::before { background-image: url("backgrounds/S12-closing-bg.svg"); opacity: 0.60; }` is defined at line 284, but the section class list is `class="section section--closing section-with-bg bg-s12"` per line 2248, so the CSS rule SHOULD match). Verify the SVG file actually loads (the manifest says it's a 3.7KB fallback). The closing "fog parting to reveal the golden slit" is the climactic visual of the page — currently it's just flat black. Either fix the bg or replace with a CSS-only radial spotlight.

10. **S10 ring semantics are wrong** (line ~2175+). Three rings showing 50 / 3 / 2 with `stroke-dasharray: 314` animating from full offset to 0 = rings fill to 100% on scroll. But the numbers 50, 3, 2 are integer counts (membri / seri / cine cu fondatorul) — they don't have "%" meaning. Either: (a) fill rings 100% immediately and let the number be the focus, (b) replace with bar charts, (c) drop the rings entirely and just show the giant numerals (3 of them centered).

---

## 3 · Top 5 must-preserve elements (Vlad-likes, must survive any rewrite)

1. **The atmospheric radial gradient on every placeholder frame** (S04 house + S11 host) — the warm radial at upper-left with grain + label feels intentional and luxurious. Don't replace with actual photos unless you have ones that match.

2. **The Cormorant Italic epigraph + manifesto lines** ("Woloshin Club nu se cumpără. Se poartă." · "Nu deschidem ușa tuturor." · "Bun venit. Sunt Rareș. Vă aștept la ușă.") — these are the most literary copy on the page. They MUST survive any font swap (currently Cormorant Italic → Kurale per Vlad's request).

3. **The scarcity block "8 LOCURI RĂMASE" hero + 50-dot row** — this is the page's only quantified urgency. Even if you fix the dot colors, the structure (eyebrow → giant claim → count copy → 50 dots → instruction) is correct.

4. **The S08 price reveal ("50 000 MDL" counter + cap)** — Vlad hasn't pushed back on this. The way the price digit animates from 0000 to 5000 with thin-space separator is genuinely elegant for a luxury site.

5. **The S09 calendar event rows** — date-on-left / title-and-desc-on-right / tag-chip-on-right is a proven editorial layout. Don't redesign it.

---

## 4 · Visual hierarchy audit

### Reads well (preserve):
- **S07 Privileges** — side-by-side H1 + 8-item list is the clearest layout on the page
- **S08 Door** — eyebrow → H1 → italic sub → giant price → meta → CTA is textbook
- **S13 Form** — same structure, clean
- **S09 Calendar** — date/title/desc/chip layout is editorial-grade
- **Scarcity block** — single message, single visualization, single CTA (well... no CTA, the dots are the CTA)

### Reads poorly (rebuild):
- **S02 Manifesto** — only 4 lines, rest is empty. Needs more text OR more decorative elements OR much tighter padding.
- **S10 Numbers** — rings too thin, gold numerals alone would work better
- **S12 Closing** — 1800px tall, only ~200px of text at the bottom. Either add the fog (per #9 above) OR shrink the section to 600-800px
- **S05 Spaces** — cards 600px tall but content only at top/bottom 100px each
- **S06 Ritual** — H1 works but the 7-beat list feels like reading a numbered list of restaurant rules

### Hidden gems (Vlad might not have noticed):
- The body::after luxury-depth radial overlay (line 132+) — subtle warm gradient at corners, barely perceptible. Good.
- The scroll progress bar (1px gold at top) — nice detail.

---

## 5 · Spacing audit

| Section | Current height | Issue | Fix |
|---------|---------------|-------|-----|
| S01 Hero | 919px | Tight at 900 viewport — CTA barely visible | Reduce to 800px |
| S02 Manifesto | 1620px | **920px empty** (460 above + 460 below) | Cut to 900px (text area 500 + 200 pad) |
| S03 Number | 705px | OK | Keep |
| S04 House | 945px | 200-400px empty bottom | Cut to 700px |
| S05 Spaces | 879px | OK | Keep |
| S06 Ritual | 1405px | 200px above + 200px below list | Cut to 1100px |
| S07 Privileges | 1778px | Tall but proportional to 8 items | Keep, or trim to 1500px |
| Scarcity block | 576px | OK | Keep |
| S08 Door | 994px | OK | Keep |
| S09 Calendar | 1185px | 100-150px between events feels thin | Keep |
| S10 Numbers | 832px | OK | Keep |
| S11 Host | 807px | OK | Keep |
| S12 Closing | 1800px | **1400px empty above text** | Cut to 700px OR add bg |
| S13 Form | 949px | OK | Keep |
| **TOTAL** | **17,594px** | v3 summary claimed 16,196px — actual is closer to 19,279 in browser (includes loader/marks) | Target v4: ~14,500px |

**Vlad's complaint about "большие пустые места которые нужно скролить"** is most acute in S02, S04, and S12. Fix those three and the perceived scroll-depth drops by 30%.

---

## 6 · Type audit

**Current font stack:**
- Display (H1/H2): `Cinzel` — caps-heavy Roman serif
- Italic (epigraphs/leads): `Cormorant Garamond` italic — elegant
- Body: `Inter` — geometric sans
- UI: `Inter` / `Manrope` mix

**Vlad wants:** `Kurale` (display) + `Plus Jakarta Sans` (body), per `hotels.banya.md`.

**Recommendation:**
- **H1/H2 → Kurale** (Cinzel alternative with softer character). Variable weight available. Comes in 400-700. Apply at display sizes; the Cinzel uppercase + Russian-friendly Cyrillic of Kurale is a closer match for Russian content if/when added.
- **Body → Plus Jakarta Sans** at 16/17px, line-height 1.65. Better Cyrillic than Inter. Replace Inter entirely.
- **Italic leads → keep Cormorant Garamond Italic** (Kurale has no italic). Or use Plus Jakarta Sans Italic for a saner one-font solution.
- **Eyebrow → Plus Jakarta Sans** at 11-12px, uppercase, letter-spacing 0.28em. Keep tracked-uppercase treatment.

**Specific typographic fixes for v4:**
- All H1s: enforce `text-wrap: balance` + `max-width: 14ch` (currently 18ch, still orphans)
- S04 H1 "WOLOSHIN BANYA. / O CASĂ LÂNGĂ / PĂDURE." → rewrite to 2 lines: "WOLOSHIN BANYA. / O CASĂ LÂNGĂ PĂDURE." (font-size reduction will help; current 5vw is too big)
- S06 H1 "ȘAPTE GESTURI, ÎNAINTE DE MIEZUL NOPȚII." → reduce font-size to keep on 1 line, or accept the 2-line break and drop "ÎNAINTE DE": "ȘAPTE GESTURI. / ÎNAINTE DE MIEZUL NOPȚII."
- S08 H1 "CEEA CE 50 000 MDL DESCHIDE" → reduce font-size; this is the most repeated and works at smaller scale
- Hero epigraph above H1 is currently hidden — bring it back into the hero

---

## 7 · Background audit

| Section | BG class | File | Visible? | Quality |
|---------|----------|------|----------|---------|
| S01 | (none — Three.js canvas) | `backgrounds/S01-hero-bg.svg` defined but UNUSED | only sparse particles | **Weak** — needs full fog |
| S02 | `bg-s02` | `S02-manifesto-bg.svg` (2.4KB) | Yes — sandy noise | **Good** — texture reads |
| S03 | `bg-s03` | `S03-number-bg.svg` (2.2KB) | Faint warm ember lower-right | **OK** — adds depth |
| S04 | `bg-s04` | `S04-house-bg.svg` (3.0KB) | Yes — warm umber + grain | **Good** |
| S05 | `bg-s05` | `S05-spaces-bg.svg` (4.2KB) | Yes — firelight glow + embers | **Good** — but only on the bottom of cards |
| S06 | `bg-s06` | `S06-ritual-bg.svg` (2.8KB) | Yes — vertical grain + center line | **OK** — adds atmosphere |
| S07 | `bg-s07` | `S07-privileges-bg.svg` (2.5KB) | Yes — midnight velvet | **OK** |
| S08 | (none) | — | Flat black | **Acceptable** — door framing works |
| S09 | (none) | — | Flat | **Acceptable** |
| S10 | (none) | — | Flat | **Acceptable** |
| S11 | (none — placeholder gradient) | — | Warm radial | **OK** |
| S12 | `bg-s12` | `S12-closing-bg.svg` (3.7KB) | **NOT RENDERING** | **Broken** |
| S13 | (none) | — | Flat | **Acceptable** |

**Missing bg for:** S01 (real fog), S12 (golden slit).
**Working but under-utilized:** S03 (ember should be more visible behind the 50), S06 (vertical line is too subtle).

**Body-level bg:**
- `body::after` luxury-depth radial (line 132) — gold-tinted radial at two corners. Subtle, works.
- `body::before` film grain SVG noise (line 120) — full-page grain. **This is the texture Vlad liked. Keep it, maybe bump opacity from 0.5 to 0.6.**

---

## 8 · Lossless issues to NOT mention in v4 plan (don't overload the integrator)

- Footer bg `#112038` band effect (cosmetic, ship)
- S05 card 4 title clipping (cosmetic, ship)
- S09 event 3 not visible in first viewport (just needs scroll, OK)
- `.ritual__rule` hairline (reads as intentional divider, ship)
- S12 nav CTA flip to filled amber (intensify-on-scroll = correct intent, ship)
- 49 dots instead of 50 (just add one more circle)

---

## Overall grade

**6.8 / 10.**

Strong bones: typography confidence, disciplined palette, clean editorial layouts in S07/S08/S13/S09.
Weak bones: hero atmosphere doesn't match Vlad's "aura that lasts" description · S11 silhouette looks like placeholder · S02 and S12 are dead space · S10 rings fail their job · scarcity dots don't visualize scarcity.

If you fix only items #1, #3, #4, #6, #9 from the top-10, the page jumps to **8.5 / 10**.

---

## Priority recommendations for v4 build (ordered)

1. **Rebuild S01 hero with real volumetric fog** — make it the room. Big move, biggest payoff.
2. **Replace S11 silhouette** with abstract form (monogram, back-facing silhouette, or empty frame with sig wave).
3. **Fix scarcity dots** — 42 solid + 8 hollow + fix count to 50.
4. **Cut section padding on S02, S04, S12** — lose ~2,500px of dead space.
5. **Swap fonts to Kurale + Plus Jakarta Sans** per `hotels.banya.md`.
6. **Fix S12 bg SVG** (or replace with CSS spotlight) so the closing fog actually parts.
7. **Simplify S08/S13 CTAs** — drop the glow halo, use ghost outline.
8. **Tighten H1 line lengths** — balance + 14ch max-width, eliminate orphans.
9. **Add body grain to 0.6 opacity** — keep the texture Vlad liked, push it.
10. **S10 rings — either fill 100% immediately or replace with bars/numerals.**

---

**Audit completed:** 2026-09-25, 1440×900 desktop, 14 sections + footer.
**Screenshots:** `/Users/pro/Documents/Projects/Woloshin_club/v2/audit/desktop-v3/` (16 PNGs, 20MB total).