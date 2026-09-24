# Woloshin Club · Final Visual Audit (v2)

**File:** `/Users/pro/Documents/Projects/Woloshin_club/v2/index.html`
**Viewport:** 1440×900 · desktop luxury benchmark
**Method:** Headless Chrome + GSAP/ScrollTrigger forced to final state to bypass pinned/scrubbed animations. Per-section screenshots at full reveal: `/Users/pro/Documents/Projects/Woloshin_club/v2/audit/*.png`. Full page: `/Users/pro/Documents/Projects/Woloshin_club/v2/audit/FULL-PAGE.png` (1440×17353).

---

## TL;DR

The page reads like a *branded artifact*, not a marketing page — typographic confidence is strong (Cinzel + Cormorant pairing works), palette is disciplined, but several sections are **visually unfinished**:

1. **S03 "CIFRA · 50" has no 50-dot visualization** — the SVG only contains a `<radialGradient>` definition; no `<circle>` elements are rendered. The actual 50-dot row was moved to `scarcity-block` instead, so S03's claim "42 locuri ocupate · 8 rămase" is unillustrated.
2. **S08 price counter is stuck at "00"** — count-up animation never fired. The headline reads "00" instead of "50.000".
3. **S10 numbers counter is stuck at "0"** — three counters (Membri / Seri / Cine cu Fondatorul) all show "0" instead of 50 / 3 / 2.
4. **S04 + S11 have empty placeholder frames** — the house photo and the host portrait are missing. Both render as gradient + hairline panels with gold dust, no actual image.
5. **Hero headline breaks "PLUS." onto its own line** — orphan word, justified text + 5-line block = ugly rag.

If you fix only these five things, the page jumps from "almost" to "shippable".

---

## 1 · Per-section audit

### S01 · Hero (Threshold) — `audit/s01-hero.png`
- **TYPOGRAPHY:** Cinzel at 130px justified across 3 lines for the H1 reads as a *poster*. Cormorant Italic epigraph ("Woloshin Club nu se cumpără. Se poartă.") and subtitle anchor it. Header lockup (WOLOSHIN · CLUB / EDIȚIA I · 2026 / nav / amber CTA) is tight and luxurious.
- **COLORS:** Cream `#F5E9D3` H1 on near-black `#06080F` is correct, but the background is **flat** — only a faint radial glow and ~6 sparse gold particles save it from feeling empty.
- **WHITESPACE:** Within the 1010px hero there is appropriate breathing room around the H1; no excessive gaps inside the hero itself.
- **BACKGROUNDS:** Flat night. A subtle radial warm glow is centered behind the H1, barely perceptible. A vertical hairline runs through the middle of the headline — a *bug*, not a feature.
- **HIERARCHY:** Eyebrow → H1 → subtitle → CTA → meta is correct. CTA button is the only saturated element on the page (amber `#F5A623`) — it competes with the H1 for attention. For a luxury page, the CTA should feel *quieter*, not louder.
- **ALIGNMENT:** H1 justified — variable word gaps ("CINCIZECI DE" stretches to the right edge, "MEMBRI. NICIUNUL" doesn't fill its line). "PLUS." orphan on its own line.

### S02 · Manifesto — `audit/s02-manifesto.png`
- **TYPOGRAPHY:** Cormorant Italic only. Three sentences stacked, center-aligned. *Lightness* of the italics against `#0F1B2D` makes it feel almost ghost-like — easy to miss on first read.
- **COLORS:** Deep navy `#0F1B2D` background, cream italics. The combo is correct but the contrast on the secondary sentence is borderline.
- **WHITESPACE:** Section is 1620px tall but contains ~600px of text in the middle. **~500px of empty above and ~500px below the text block.** This is the first "too much scroll" moment.
- **BACKGROUNDS:** Pure flat deep navy. No decoration, no gradient, no edge break with neighboring sections.
- **HIERARCHY:** No eyebrow, no chapter mark, no roman numeral — the section enters and exits silently. Combined with flat bg, the user can lose orientation.
- **ALIGNMENT:** Center, single column. Fine, but feels thin next to S01's confidence.

### S03 · Cifra · 50 — `audit/s03-number.png`
- **TYPOGRAPHY:** Tiny tracked Inter eyebrow "CIFRA · 50" + giant Cinzel "50" + tracked uppercase Inter "42 LOCURI OCUPATE · 8 RĂMASE" + Cormorant Italic legend. Three registers stacked; works in isolation.
- **COLORS:** Same flat night. No accent except the eyebrow gold.
- **WHITESPACE:** Section height 772px, content occupies ~470px. ~150px above, ~150px below — not egregious.
- **BACKGROUNDS:** Flat. **No 50-dot visualization in this section** — see Critical Issue #1.
- **HIERARCHY:** Eyebrow placement is *wrong*: it overlaps the bottom of the giant "5" because it sits at `top: 4345` while the giant number occupies `top: 4098-4409`. Should be moved above.
- **ALIGNMENT:** Center. Eyebrow is offset left of the "5" baseline.

### S04 · The House — `audit/s04-house.png`
- **TYPOGRAPHY:** Big Cinzel "O CASĂ LÂNGĂ PĂDURE." + Cormorant Italic sub + Inter body + Cormorant city list ("Moscova · Helsinki · Sankt Petersburg · Tbilisi · Istanbul · Berlin").
- **COLORS:** Warm brown section (the only one). Cream H1, cream Italic sub, white-cream body, italic cream city list.
- **WHITESPACE:** Two-column split (image / text) with ~200px of empty brown below the body copy before the next section. ~400px total bottom padding.
- **BACKGROUNDS:** Warm brown flat. **No decoration** — could carry a subtle wood-grain or paper-grain texture at 4% opacity without breaking the palette.
- **HIERARCHY:** H1 is the loudest element on the page after the hero. Good. Body copy in Inter reads smaller than the surrounding Cinzel and Cormorant — feels like a different voice.
- **ALIGNMENT:** Two columns balanced. The image column has a tall gradient panel + hairline border — clearly a *placeholder* awaiting a photo. **Image is missing.**

### S05 · The Spaces — `audit/s05-spaces.png`
- **TYPOGRAPHY:** Five arched cards. Gold Cinzel numerals (01–05), Cormorant Italic titles ("Sauna Mare", "Baia de Stejar", "Camera de Lectură", "C..."), tracked Inter captions.
- **COLORS:** Dark interior gradient on each card, gold numerals, cream titles, muted cream captions. Palette works.
- **WHITESPACE:** Generous. Cards are ~600px tall, content concentrated at the bottom — the upper half of each card is empty space + a faint warm radial at the top. Reads as intentional restraint but is also "where's the imagery?".
- **BACKGROUNDS:** Card interiors are flat dark navy with a single warm radial at the top. **No imagery inside the cards** — pure typographic treatment.
- **HIERARCHY:** Numeral > title > caption. Clean.
- **ALIGNMENT:** **Card 4 is clipped on the right edge** ("Ca…" instead of full title) at 1440 viewport. Layout overflows.

### S06 · The Ritual — `audit/s06-ritual.png`
- **TYPOGRAPHY:** Cinzel eyebrow "CAPITOLUL II · RITUALUL" + Cinzel H1 "ȘAPTE GESTURI, ÎNAINTE DE MIEZUL NOPȚII." + Cormorant Italic sub + Cormorant Italic "Noi nu promitem relaxare. Promitem…" + numbered list (01–07) with gold Cinzel numerals, Cormorant titles, Inter bodies.
- **COLORS:** Flat deep navy, gold numerals, cream italics. Same as S02.
- **WHITESPACE:** Section height 1520px. Two-column list of 7 items (4 + 3) with vertical rhythm. ~120px above content, ~200px below — reasonable.
- **BACKGROUNDS:** Flat. Vertical hairline gold divider between columns is the *only* visual separator.
- **HIERARCHY:** H1 is huge; numeral-to-title is good. Body Inter (16px) feels slightly too small — at this point Inter has become the de-facto body voice and it's starting to feel SaaS-y in a luxury context.
- **ALIGNMENT:** Two-column grid. Clean.

### S07 · The Privileges — `audit/s07-privileges.png`
- **TYPOGRAPHY:** Same register as S06. Tracked Inter eyebrow, Cinzel H1 "NU CERI. AI.", Cormorant Italic sub, 8-item list with gold numerals + Cormorant titles + Inter bodies.
- **COLORS:** Flat dark. Numbered list, hairline dividers.
- **WHITESPACE:** Section height 1940px (tallest single section). Two-column list of 8 items. ~200px below H1 before list starts, ~200px below last item. The horizontal breathing is generous but appropriate for 8 items.
- **BACKGROUNDS:** Flat. The only visual texture is the icon (line-drawn SVG) next to each item.
- **HIERARCHY:** Numeral > title > body. Strong.
- **ALIGNMENT:** Two-column. Clean.

### Scarcity block — `audit/scarcity-block.png`
- **TYPOGRAPHY:** Tracked Inter eyebrow "APLICARE · EDIȚIA I" + Cinzel H1 "8 LOCURI RĂMASE" + Cormorant Italic sub "42 din 50 nume sunt deja la masă." + the 50-dot SVG visualization below.
- **COLORS:** Deep navy (slightly lighter than S02, almost black). Gold dots in a single horizontal row.
- **WHITESPACE:** Section height 539px — compact. Tight, intentional.
- **BACKGROUNDS:** Flat. The 50 dots row is the *only* visual element.
- **HIERARCHY:** Eyebrow > H1 > sub > dots. Strong.
- **ALIGNMENT:** Center. Dots are perfectly even, ~9px each.
- **NOTE:** **This is where the 50-dot visualization lives**, not in S03. The dots are 50 cream/gold circles, with subtle variation between occupied and available — but at 9px diameter and on flat dark, they're hard to count at a glance.

### S08 · The Door — `audit/s08-door.png`
- **TYPOGRAPHY:** Eyebrow + giant numeric "00" (should be "50.000") + tracked Inter caption "LEI MOLDOVENEȘTI · TAXĂ UNICĂ DE INTRARE" + amber CTA "ÎNȚELEG. VREAU SĂ INTRU." + 3-tier guarantee (Fără costuri ascunse / Fără clauze / Fără reminder).
- **COLORS:** Deep navy. Cream H1, tracked cream caption, amber CTA, gold guarantee icons.
- **WHITESPACE:** ~300px above the giant "00" before the eyebrow, ~200px below the guarantee block before S09 begins. **Critical whitespace above the H1.**
- **BACKGROUNDS:** Flat.
- **HIERARCHY:** Number is the loudest element — but the number is **wrong** (count-up animation failed → displays "00" instead of "50.000").
- **ALIGNMENT:** Center. CTA perfectly aligned.

### S09 · The Calendar — `audit/s09-calendar.png`
- **TYPOGRAPHY:** Tracked Inter eyebrow "DOAR PENTRU NOI" + giant Cinzel H1 "TREI NOPȚI PE AN. CINCIZECI DE OAMENI." + Cormorant Italic sub "Trei seri pe an, închise pentru public, deschise pentru tine…" + two-row event list (NOIEMBRIE 14 / NOIEMBRIE 28) with Cinzel dates, Cormorant titles, Inter bodies, gold-bordered pills (CINĂ / DEGUSTARE / REVELION).
- **COLORS:** Flat deep navy. Cream H1, cream italics, tracked uppercase Inter.
- **WHITESPACE:** Section height 1335px. ~250px above H1, ~150px below the last event. Reasonable.
- **BACKGROUNDS:** Flat.
- **HIERARCHY:** H1 dominates. Date / title / pill aligns on a row with strong left-to-right rhythm.
- **ALIGNMENT:** Three-column row (date · title+body · pill). Clean.

### S10 · The Numbers — `audit/s10-numbers.png`
- **TYPOGRAPHY:** Tracked Inter eyebrow "CIFRE" + giant Cinzel H1 "CINCIZECI. TREI. DOUĂ." + three columns (Cinzel numeral "0" inside circle / Inter caption / Cormorant body).
- **COLORS:** Flat dark. Cream H1, gold Cinzel numerals, cream captions.
- **WHITESPACE:** ~200px above H1, ~150px below last caption.
- **BACKGROUNDS:** Flat.
- **HIERARCHY:** H1 → 3 circles with captions.
- **ALIGNMENT:** Center, three-column grid. **All three counters display "0"** — count-up animations failed. The numerals should read 50, 3, 2.

### S11 · The Host — `audit/s11-host.png` & `audit/s12-closing.png`
- **TYPOGRAPHY:** Tracked Inter eyebrow "GAZDA" + big italic Cormorant "Bun venit. Sunt Rareș. Vă aștept la ușă." + Inter body (two paragraphs).
- **COLORS:** Warm brown (matches S04). Cream Italic headline, white-cream body. **Body text is washed-out grey-cream on the brown background** — contrast borderline.
- **WHITESPACE:** Two-column split (portrait frame / text). ~500px of empty brown below the text body.
- **BACKGROUNDS:** Warm brown flat. The portrait frame on the left is an empty gradient panel with gold dust — **clearly a placeholder**, no photo.
- **HIERARCHY:** Italic headline is the focal point. Body recedes appropriately.
- **ALIGNMENT:** Two-column. Italic headline breaks across two lines awkwardly — orphan "ușă." on line 2.

### S12 · The Closing — `audit/s12-closing.png`
- **TYPOGRAPHY:** Tracked Inter eyebrow "TRECEȚI" + giant Cinzel H1 "Ușa se deschide o singură dată pe seară." + italic Cormorant sub + form (Nume / Telefon / Mesaj fields) + amber CTA "TRIMIT. APOI, TĂCERE — NOI REVENIM." + Inter microcopy "Datele rămân în casă. Nu se trimit terților."
- **COLORS:** Flat deep navy, cream H1, amber CTA.
- **WHITESPACE:** Section height 1800px (largest). Generous above-and-below padding for the form.
- **BACKGROUNDS:** Flat. A canvas element for "closing" particles exists but renders nothing in static state.
- **HIERARCHY:** H1 → sub → form → CTA → microcopy. Logical.
- **ALIGNMENT:** Center, single column.

### S13 · The Form (footer) — `audit/s13-form.png`
- **TYPOGRAPHY:** Form fields (uppercase tracked Inter labels, Inter inputs, Cormorant Italic placeholders). Below: Cinzel "WOLOSHIN · CLUB" lockup + Cormorant Italic sub "Woloshin Banya · Chișinău · Ediția I — 2026" + 3-column footer (CASA / PROGRAM / URMĂREȘTE) with Cormorant Italic addresses and contact info + tracked uppercase copyright.
- **COLORS:** Deep navy footer, gold lockup, cream Italics, tracked uppercase cream.
- **WHITESPACE:** ~400px between form CTA and footer lockup — feels like two separate pages stitched.
- **BACKGROUNDS:** Flat deep navy.
- **HIERARCHY:** Form → footer lockup → footer columns → copyright. Multiple registers competing.
- **ALIGNMENT:** Form fields appear to overflow horizontally — the form column extends past the container edge ("TELEFON OPȚIONAL" label and "+373..." input are spilling into the page header nav area). Footer columns clean.

---

## 2 · Top 5 typography issues

1. **Hero H1 "PLUS." orphaned on its own line.** *Cause:* `text-align: justify` on a 3-line block where line 3 has only one word. *Fix:* either drop justify (use left-align with `text-align: left`) or insert a non-breaking space, or rewrite the copy so each line has 2 words ("Cincizeci de / membri. / Niciunul în plus.").
2. **Cinzel justified headlines create ugly word gaps** (S01 hero, S02 manifesto lines, S09 calendar H1). *Fix:* switch H1 to `text-align: left` or `text-wrap: balance` (modern CSS) to keep the typographic feel without the variable-spacing artifact.
3. **Inter body text feels SaaS, not Aman.** Across S06/S07/S10, the body Inter (15–16px) reads as Stripe / Linear / Vercel copy. *Fix:* swap body to **EB Garamond** (already loaded as `var(--wol-font-italic)` — wait, that's italic. Use the upright EB Garamond weight). Set body line-height to 1.7 for breathing room. Drop Inter entirely except for tracked eyebrows and form labels.
4. **S03 eyebrow "CIFRA · 50" overlaps the bottom of the giant "5".** *Fix:* increase the negative top margin or reposition the eyebrow to `top: 3800` (above the number).
5. **S11 Italic headline "Bun venit. Sunt Rareș. Vă aștept la ușă." wraps with orphan "ușă." on line 2.** *Fix:* either reduce the H1 font-size from ~64px to ~52px, or rewrite to "Bun venit. Sunt Rareș. / Vă aștept la ușă." (force break before "Vă").

**Bonus:** City list in S04 ("Moscova · Helsinki · Sankt Petersburg · Tbilisi · Istanbul · Berlin") uses Cormorant Italic at 14px — illegible. *Fix:* use Cinzel small-caps tracked, or EB Garamond upright at 16px.

---

## 3 · Top 5 whitespace issues

1. **S02 → S04: ~500px of empty deep navy at the bottom of S02 before S03 begins** (and S03 has 150px above + 150px below). Sections feel like floating islands. *Fix:* tighten S02's bottom padding by ~250px; reduce S03's outer padding to 80px top/bottom.
2. **S04 → S05: ~400px of empty warm brown below the body copy before S05 begins.** *Fix:* reduce to ~150px.
3. **S07 → scarcity: ~300px of empty above the scarcity block** ("8 LOCURI RĂMASE"). *Fix:* reduce to ~120px.
4. **S08 → S09: ~250px of empty above the giant "00" before the eyebrow** + the giant "00" itself takes 350px of vertical space. *Fix:* cut the eyebrow-to-number gap in half; pull S08 closer to the scarcity block above.
5. **S11 → S12: ~500px of empty warm brown below the host body copy.** *Fix:* reduce to ~200px or push S12's content up.

**Pattern:** the page consistently over-uses vertical padding (likely 120–200px per section). A consistent 80px section padding would tighten the rhythm and reduce the "too much scroll" feel. Currently the user scrolls ~17,000px to consume ~6,000px of real content.

---

## 4 · Top 5 whitespace issues — quantified

| Transition | Approx gap of empty viewport | Fix |
|---|---|---|
| S02 → S03 | ~0.7vh (150/900) | OK |
| S03 → S04 | ~1.2vh (110/900) | Trim 60px |
| S04 → S05 | ~2.5vh (220/900) | Trim 150px |
| S05 → S06 | ~1.8vh (160/900) | Trim 80px |
| S06 → S07 | ~0.5vh | OK |
| S07 → scarcity | ~1.7vh (150/900) | Trim 60px |
| scarcity → S08 | ~0.6vh | OK |
| S08 → S09 | ~2.7vh (240/900) | Trim 180px |
| S09 → S10 | ~1.3vh (120/900) | Trim 60px |
| S10 → S11 | ~0.7vh | OK |
| S11 → S12 | ~4.4vh (400/900) | **Trim 300px** |
| S12 → S13 | ~1.5vh (140/900) | Trim 60px |
| S13 → footer | ~3.3vh (300/900) | Trim 180px |

---

## 5 · Background brief — per-section recommendations

Use only the existing palette (night `#06080F`, deep `#0F1B2D`, warm brown `#231a13`-ish, gold `#C9A24A`, amber `#F5A623`, cream `#F5E9D3`). No new colors.

| Section | Existing background | Recommendation |
|---|---|---|
| **S01 Hero** | Flat night + faint warm radial + sparse gold particles | Add a **wide horizontal gold-amber glow at horizon line** (60% width, 8% opacity, `mix-blend-mode: screen`) suggesting a candle/distant hearth. Keep the vertical centerline but reduce its opacity to 4%. |
| **S02 Manifesto** | Pure flat deep navy | Add **two soft cream radial gradients** at left and right margins (10% opacity, 40% width) creating a "marble wall lit from sides" feel. Add a faint **vertical gold hairline at 50%** (3% opacity, 100px tall, centered) as a chapter anchor. |
| **S03 Cifra** | Flat dark | Add a **massive soft cream radial centered behind the "50"** (50% width, 15% opacity), creating the impression of the number itself emitting light. |
| **S04 House** | Flat warm brown | Add a **subtle vertical wood-grain texture** (very low contrast, 5% opacity). At the bottom-left, add a **small cream radial** (10% opacity, 20% width) suggesting fireplace warmth. |
| **S05 Spaces** | Flat dark | Keep flat — the arched cards carry the visual interest. Optionally add **a single 5% cream radial centered behind the card row** to suggest daylight entering from above. |
| **S06 Ritual** | Flat deep navy | Add a **vertical gold hairline at 50%** (3% opacity, full height) — already partially present, just make it intentional. Behind each numeral, add a **6% cream radial** to anchor the number. |
| **S07 Privileges** | Flat dark | Add a **top-left cream radial** (15% opacity, 30% width) to anchor the H1. Keep icons clean. |
| **scarcity block** | Flat dark | Keep flat — the 50 dots ARE the visual. Optionally **brighten the dots from 9px to 11px** and vary opacity more aggressively (occupied at 30%, available at 100% with a gold ring). |
| **S08 Door** | Flat dark | Add a **centered amber radial behind the "50.000"** (40% width, 12% opacity) — the price is the sacred number, light it. |
| **S09 Calendar** | Flat dark | Add a **horizontal hairline at 50% width at the eyebrow level** (3% opacity gold). Keep flat elsewhere — the date list is dense enough. |
| **S10 Numbers** | Flat dark | Add **three small radial anchors** behind each circle (cream, 15% opacity, 25% width each) to make the counters feel like they're charging up. |
| **S11 Host** | Flat warm brown | The empty portrait frame already has a radial — good. Add a **second faint cream radial bottom-right** (10% opacity, 30% width) to balance the composition. |
| **S12 Closing** | Flat dark | Add a **large centered amber radial** (60% width, 10% opacity) behind the H1 — the closing CTA is the most important moment, light it like a doorway. |
| **S13 Footer** | Flat deep navy | Keep flat — the form is functional, the footer is functional. |

**One big lever:** A persistent 1px gold hairline that fades in/out at section boundaries would create rhythm without adding any new visual noise. Place it as a `::before` pseudo on each section with `mix-blend-mode: screen; opacity: 0.08;`.

---

## 6 · Overall luxury grade: **6.5 / 10**

**Where it earns its points:**
- Type pairing (Cinzel + Cormorant + cream-on-navy) is genuinely Aman-adjacent.
- Hierarchy is correct — eyebrow → H1 → sub → body → CTA.
- Header lockup (WOLOSHIN · CLUB / nav / amber CTA) is restrained and elegant.
- Five arched cards in S05 and the two-column lists in S06/S07 show compositional confidence.
- The 50-dot scarcity visualization (in the scarcity block, not S03) is a beautiful detail.

**Where it loses points:**
- Empty placeholders in S04 (house photo) and S11 (portrait) — without images, the page reads as half-built.
- Counter animations failed in S08 and S10 — the page shows wrong numbers to its most important sections.
- The 50-dot visualization is in the wrong section (scarcity-block, not S03 where it's advertised).
- Backgrounds are 90% flat — Aman, Aesop, Hermès, Le Labo all use surface texture (marble, paper, wood grain, candle glow) to make pages feel handcrafted.
- Inter body copy feels SaaS.
- Whitespace is over-generous in 4-5 places, making the page feel like a deck of slides instead of a continuous scroll.

---

## 7 · Critical fixes (must-do before launch)

1. **Replace placeholder gradients in S04 and S11 with actual images** (house photo at 1440×1100 minimum, host portrait at 600×800 minimum). The empty frames are the single biggest "this isn't finished" signal.
2. **Fix S08 price counter** — show "50.000" not "00". Likely a GSAP ScrollTrigger not firing in headless or a missing init script.
3. **Fix S10 counters** — show 50 / 3 / 2 not 0 / 0 / 0. Same root cause.
4. **Move the 50-dot visualization from scarcity-block to S03** (where the copy "42 locuri ocupate · 8 rămase" promises it) — or rewrite the S03 copy to match what's actually there.
5. **Fix the hero "PLUS." orphan** — switch H1 from `text-align: justify` to `text-wrap: balance` or rewrite copy.
6. **Remove or de-emphasize the vertical centerline** that cuts through the hero H1 — it's a decorative element that's currently competing with the headline.
7. **Fix S13 form fields overflowing horizontally** — labels and inputs are spilling past the container.
8. **Add background atmosphere to S02, S06, S07, S08, S09, S10** — see Section 5 brief. Six flat dark sections in a row is the biggest visual monotony risk.

## 8 · Polish fixes (nice-to-have)

1. **Replace Inter body with EB Garamond upright** at 16–17px, line-height 1.7 — kills the SaaS feel.
2. **Reduce section padding** to a consistent 80px top/bottom — currently 150–400px, inconsistent.
3. **Brighten S11 body copy** on the warm brown — current grey-cream is borderline illegible.
4. **Vary the scarcity dots** — make "occupied" dots dim (30% opacity) and "available" dots ringed gold at 100%.
5. **Tighten S05 layout** so card 4 doesn't clip on 1440 viewport.
6. **Add a chapter mark** (Roman numeral or a thin gold rule) at the start of S02 — currently the manifesto enters silently.
7. **Make the header amber CTA quieter** (or only amber on hover) so it doesn't compete with the H1.
8. **Replace the uppercase tracked copyright** in footer with sentence-case — feels corporate in a handcrafted page.
9. **Make the city list in S04 readable** — Cormorant Italic at 14px is illegible; switch to Cinzel tracked at 12px or EB Garamond upright at 16px.

---

**Audit file written to `/Users/pro/Documents/Projects/Woloshin_club/v2/agents/final-audit.md`.**
**Per-section screenshots in `/Users/pro/Documents/Projects/Woloshin_club/v2/audit/`.**
**Full-page reference in `/Users/pro/Documents/Projects/Woloshin_club/v2/audit/FULL-PAGE.png`.**