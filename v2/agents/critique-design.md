# Critique · Design perspective on copy / research / motion

> Read: `copy/out.md`, `research/out.md`, `motion/out.md` (peer deliverables).
> Self-review: `design/out.md` (mine — assumed). All findings below are anchored to that file.

---

## A · DESIGN ↔ COPY INTEGRATION

Design has 14 sections (S01–S14). Copy has 8 blocks (A–H). Mapping:

| Design § | Copy home | Status |
|---|---|---|
| S01 Pre-loader (01→50 counter) | — | OK (no copy) |
| S02 Hero | A (nav) + B (hero + epigraph) | ✓ |
| S03 Manifesto (200vh pin, 60 words) | — | **MISSING COPY** — copy's epigraph (3 lines, 29 words) could live here, but copy placed it as decoration above hero H1 instead |
| S04 The House (split 60/40 portrait + quote) | — | **MISSING COPY** — no Romanian voice for "the house", no founder voice, no body lines |
| S05 The Spaces (5 horizontal arch cards) | — | **MISSING COPY** — copy never describes the spaces (sauna, banya rooms, ritual rooms) |
| S06 The Ritual (7 beats: arrival, pour, steam…) | — | **MISSING COPY** — copy F has events, not rituals; copy D has robe/hat/admin, not arrival sequence |
| S07 The Privileges (8 rows w/ SVG icons) | E (4 privileges) | **PARTIAL** — design wants 8, copy supplies 4; icon list (door, bottle, book, calendar, steam, monitor, champagne, plane) has no copy provenance for monitor/workstation |
| S08 Membership (50 000 numeral composition) | C (ce deschide ușa) | ✓ |
| S09 Calendar (5–6 events) | F (3 evenimente/an) | **CONFLICT** — copy says 3 nights/year, design S10 stats card says 12, calendar lists 5–6 |
| S10 The Numbers (50 / 12 / 1 rings) | — | **CONFLICT** — "12 evenimente" contradicts copy's "trei seri pe an" |
| S11 The Host (founder portrait) | D (administrator) | ✓ but **BURIED** — see §C |
| S12 The Door (fog parting) | — | OK (the moment IS the design) |
| S13 Apply form | G ("ziua ta e a noastră" + final CTA) | **WRONG HOME** — copy G is gift/birthday, not form labels |
| S14 Colophon | H (footer) | ✓ |

**Copy with no design home:** Section G (the birthday gift ritual) — copy calls it a closing beat with its own CTA, but design has no corresponding section. Either kill the copy or add a section. Section F's "cerc de Telegram" and "cina cu fondatorul" also have no design surface.

**Critical gap:** S04 / S05 / S06 are *unwritten*. The page is half-built in copy.

---

## B · DESIGN ↔ MOTION INTEGRATION

Motion spec covers 5 sections (threshold, stats, ritual, personal, closing). Design needs motion for 14. Missing:

- **S01 Pre-loader ticker** — motion §10 mentions counter system but never wires the 01→50 pre-loader reveal.
- **S03 Manifesto 200vh pinned sentence reveal** — biggest motion moment in design, zero coverage.
- **S04 The House** — marquee + portrait parallax both unaddressed.
- **S05 The Spaces horizontal pin** — not in motion spec at all; needs an explicit horizontal-scrub recipe or the section will be implemented ad-hoc.
- **S07 Privileges sticky-left + scrolling-right** — motion's "ritual" section is close but uses pin-snap, not sticky-pin. Different mechanic.
- **S08 Membership 50 000 numeral count-up** — motion §4 counters go to 50 max (members, events, discount). 50 000 needs a new `format` (thousand separators during count).
- **S09 Calendar day-count** — 6 individual counters for days, not specified.
- **S13 Apply form morph** — no spec.
- **S14 Colophon stagger** — trivial but not specified.
- **Custom cursor** — design §6 specifies ring expand, magnetic snap, hide <720px. Motion §5 actively rejects it ("no custom cursor; hush over chrome"). **Conflict.**
- **Side dots scroll-spy** — motion silent; design §8 specifies dot states, label fade.
- **Nav CTA gold→amber swap after S12** — design specifies; motion silent.

Motion is doing 30% of the work design needs. Either trim design or expand motion.

---

## C · LUXURY GRADE

**Verdict: Aman-tier in intent, "Moldovan premium" in three places.**

1. **Personal-administrator is buried.** Copy §D says it is the *literal* heart ("dacă un paragraf trebuie tăiat, nu-l tăia pe acesta", "aici respiră toată pagina"). Design parks it at S11 of 14 — Chapter IV "Closing", *after* privileges, *after* pricing, *after* calendar. The reader has already decided before meeting the host. **Move §D's content to S04** (right after the hero), or split the founder portrait into a Ch II anchor.

2. **Two new colors slipped in.** Design §10 adds `--wol-velvet: #2A1A38` and `--wol-sand: #C9B68C`. Research §6.5 explicitly says "No new color. The palette is complete. Adding a new color breaks the 9-token discipline." Velvet especially reads as nightclub, not banya.

3. **Glass card + radial glow on the form (S13).** "Glass card" + "1500px diameter, 8% opacity gold radial" is the closest the page gets to SaaS-marketing aesthetic. Research §1.7 / §6.5 favors pointlight without container chrome. Either drop the glass blur or drop the radial glow — not both.

4. **Pricing presentation: editorial.** Good. No "from", no FAQ inline, single composition. Aesop discipline honored.

5. **Logo treatment: restrained.** Good — gold wordmark, no shadow, no backdrop.

6. **Fog-parting door moment: real.** Motion §7.3 + design S12 align. Density scrubbed by scroll, mouse pulls fog aside. The single dramatic gesture on the page.

---

## D · RESPONSIVE REALITY

Spec is real but **silent on the most failure-prone things**.

- **3D hero mobile:** both spec a static JPEG fallback + CSS conic-gradient ✓. But motion says canvas mounts after `requestIdleCallback` — design doesn't reference this; without it, mobile FCP slips.
- **Horizontal-pin section mobile:** design §9 says "vertical stack of 5 arch cards". Motion says nothing. The horizontal-scrub → vertical-stack transition is the *hardest* responsive build on the page; neither spec gives a code skeleton.
- **Custom cursor:** design §6 disables <720px ✓. Motion says remove it entirely. **Pick one** (recommend: keep design's, simpler).
- **Romanian diacritics:** Romanian adds 6 characters (ă â î ș ț) that are typically 1.05–1.15× wider than Latin equivalents at display weights. Cinzel 168px "ÎNAINTE DE MIEZUL NOPȚII" needs an explicit letter-spacing of `-0.01em` and a `text-wrap: balance` or it will overflow on 1280px viewports. **Neither design nor motion addresses this.** Test on the hero H1, S06 timeline titles, and the manifesto paragraph.
- **Page weight:** 14 sections × 120vh = ~1680vh. On mobile this is 60+ screens of scroll. No anchor-link strategy specified. No "back to top" handling for nav.
- **iOS Safari WebGL:** motion spec says "renders in every browser, including the user's mother-in-law's iPad" — but doesn't address iOS Safari 17's known issue with `MeshPhysicalMaterial.transmission` (Scene B orb). Add an explicit iOS fallback (skip orb, render a static radial-gradient).

---

## E · INFOGRAPHIC SYSTEM — does it scale?

The "Editorial Numbered Chapters" pattern is applied to S06, S07, S09.

- **S06 (Ritual) and S09 (Calendar) share a near-identical template:** vertical gold rule at col 6, alternating left/right, Cinzel number + Cormorant italic title + Inter body. Two sections in a row with the same skeleton = the reader's eye checks out by S09 beat 2. **Differentiate:** calendar should use a date-stamp (month eyebrow + day number, no big "01–06"), ritual should keep the chapter numerals. Visual rhyme ≠ identical structure.
- **S07 (Privileges) is the right break** — sticky left + scrolling right with thin-line icons. Different enough to feel like a third mode.
- **Icons in S07:** "monitor" (private workspace) and "plane" (off-season travel) read as SaaS-feature-list. The other 6 (door, bottle, book, calendar, steam, champagne) earn their place. Cut 2, keep 6 privileges, or replace with banya-specific objects (oak leaf, felt hat, embroidered initial).

---

## F · KILL LIST — 3 elements to remove

1. **Side dots scroll-spy** (design §8). Motion spec already chose "top progress bar only, hush over chrome". Two scroll indicators is design-by-committee. **Kill the side dots.**
2. **S01 Pre-loader 2.4–3s block with 01→50 counter.** The 50 → 50 000 rhyme is cute but blocking first paint for 3 seconds on a luxury site that should feel fast reads as broken to non-designers. **Replace** with an instant gold-line + sigil fade (200ms) or skip the pre-loader entirely.
3. **S05 The Spaces horizontal-pin 400vh section.** 400vh of scroll to display 5 room cards = "look how fancy we are with horizontal scroll" — a 2020 trick that Aman and Cheval Blanc do not use. **Stack the 5 cards vertically** in editorial columns (Cinzel number + Cormorant italic title + 2 lines body, full-bleed photo every other). Saves ~300vh, removes the heaviest responsive build, and reads more editorial.

---

## G · PRIORITY FIXES — top 5

1. **Move Personal/Administrator (copy D) to S04 or new S04b.** The page's stated heart is at position 11/14. Promote it.
2. **Resolve the event-count contradiction.** Pick a number: "trei seri pe an" (copy F) OR "12 evenimente" (design S10) OR 5–6 visible events (design S09). Currently the page claims all three.
3. **Remove `--wol-velvet` and `--wol-sand` from design §10.** Research explicitly forbids new colors. Velvet especially breaks the banya tone.
4. **Write copy for S03, S04, S05, S06.** Manifesto, the house, the spaces, the ritual. The page is half-written.
5. **Add Romanian-diacritic typography pass.** Test Cinzel 168px + Cormorant italic 56px with the full Romanian character set. Add `text-wrap: balance`, tighten letter-spacing by 1% on display headlines, and re-measure every clamped value.

---

## H · NEW IDEAS — 3 moves nobody picked up

1. **"8 locuri rămase" dot grid above S08.** Research §4.2 and §1.1 (Soho House) both recommend it; copy §B supplies the line ("Cincizeci de membri. Niciunul în plus."). Design has *nothing*. Add a 50-dot row (42 filled, 8 empty, 8th pulses) between S07 and S08 — visualises the copy's claim without becoming a marketing counter.

2. **Hand-lettered closing colophon.** Design §14 has a `stroke-dasharray` signature animation but no content. Copy §G supplies the perfect 3-line closing poem ("Un club nu este o listă / Este o masă, într-o casă, lângă o pădure / cu cincizeci de oameni care se recunosc."). Commission a real calligrapher's SVG path for those three lines and animate it as the page's final gesture — replaces the generic sigil in S14.

3. **Audio whisper from founder** in S11 (Host). Research §1.4 (Cheval Blanc audio-as-mark) and motion §10 mention nothing. A 22-second voice memo from Rareș, gated behind a tap on the portrait, is the kind of detail that survives every screenshot — and Telegram distribution is free.

---

## Summary

Design is 80% there. Three real failures: (1) copy is half-written for the middle of the page, (2) the page's stated heart (the administrator) is buried at position 11/14, (3) motion spec covers only 5 of the 14 sections motion is needed for. Two contradictions need resolving (event count 3 vs 12, new colors vs research mandate) before build. The kills are the side dots, the pre-loader, and the horizontal-pin section — all three are "design-speak" moves Aman would not make.
