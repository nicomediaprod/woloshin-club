# AGENTS.md — Conventions for AI Agents Working on Woloshin Club

You are an AI agent working on the Woloshin Club landing page (`index.html`). This file tells you what is sacred, what is flexible, and what will make Vlad reject your work.

---

## Read first

Before making ANY change, read in this order:
1. **HANDOFF.md** — current state + what's pending
2. **ARCHITECTURE.md** — technical deep-dive
3. **agents/copy-ru.md** — the Russian copy register

---

## Sacred (do NOT change without explicit instruction)

### File structure
- `index.html` is **the single source of truth**. Single self-contained file, no build step.
- The HTML structure has 14 `<section>` blocks numbered S01–S14 (S14 is `<footer>`). Do NOT add or remove sections.
- The `data-ru` and `data-ro` attribute contract is how the language toggle works. Every translatable text string has BOTH attributes. The default-rendered textContent (between the opening and closing tag) must be the Russian version.

### Visual identity (from `woloshin.css`)
- **Palette is sacred.** Only these tokens may be used:
  - `--wol-bg-night: #06080F`
  - `--wol-bg-deep: #0F1B2D`
  - `--wol-bg-warm: #1A1410`
  - `--wol-bg-card: #10203A`
  - `--wol-text-cream: #F5E9D3`
  - `--wol-text-white: #FFFFFF`
  - `--wol-text-muted: #A0A8B8`
  - `--wol-text-muted-warm: #9A8870`
  - `--wol-text-gold: #E8C492`
  - `--wol-gold: #C9A24A`
  - `--wol-gold-2: #D4A93B`
  - `--wol-gold-bright: #F2A900`
  - `--wol-amber: #F5A623`
  - `--wol-amber-deep: #D68A1F`
  - `--wol-ember: #FF8A3D`
  - `--wol-ice: #AEC8E6`
- Do NOT introduce new colors. The page is dark + gold + amber by design. No teals, no purples, no "tech blue."

### Typography
- **Kurale** (serif, Cyrillic + Latin) — display headings, subheads, italic subheads
- **Plus Jakarta Sans** (sans, Cyrillic + Latin) — body, microcopy, UI labels
- **Do NOT** add new font families. Do NOT switch to system fallbacks unless Google Fonts CDN is unreachable.
- Display headings: weight 400-700 Kurale, italic 400 for subheads
- Body: 300-600 Plus Jakarta Sans

### Brand voice (Russian)
- **Direct, concrete, dry.** Not poetic for the sake of poetry. Poetic only when concrete.
- **Vlad speaks plainly.** If a sentence sounds like a Tolstoy novel, rewrite.
- **Banned words** (Russian): `привилегия`, `премиальный`, `эксклюзивный`, `уникальный`, `абонемент`, `бенефиты`, `почувствуйте`, `откройте для себя`, `привилегированный`, `редкий`, `особенный`
- **Banned patterns**: `Это не X — это Y` (more than once per section), `Здесь [verb]` poetic openers, `В современном мире`, `Сегодня мы`, empty intensifiers (`абсолютно`, `поистине`, `действительно`)
- **Forbidden characters**: mixed Cyrillic + Latin in the SAME word (e.g. `Анти-реvelion`). Either full Cyrillic or transliterate.

### Brand voice (Romanian)
- Use the master copy in `agents/copy/out.md` as the source of truth.
- Banned Romanian words: `abonament`, `reducere`, `promoție`, `cel mai bun`, `client`, `card VIP`
- Prefer: `membru`, `acces`, `privilegiu`, `ritual`, `administrator dedicat`, `ediție`, `cotizație`, `depozit`

---

## Flexible (you can change these)

### Motion timing
- Easing, durations, stagger order — adjust per section. Don't break the 5-ease luxury vocabulary: `revelation` / `settle` / `drift` / `magnetic` / `ritual`.

### Background SVG opacity per section
- Each section has a `bg-svg-opacity` range. Tune by feel — too high competes with text, too low doesn't register.

### Three.js scenes
- Hero fog + particles: tunable density, particle count (currently 240), drift speed
- Closing fog-parting: tunable density scrub rate

### Copy microcopy (hover, loading, errors)
- Tooltip strings, button states, etc. — feel free to polish, but apply the Russian banned-words list.

### Spacing rhythm
- Section padding `clamp(40px, 6vh, 64px)` (mobile) / `clamp(48px, 7vh, 80px)` (desktop). Adjustable if a section feels cramped.

### New backgrounds
- Add new SVGs to `backgrounds/` (vector format, brand palette only). Don't replace existing ones unless explicitly asked.

---

## Process for any change

1. **Before changing copy**: read `agents/copy-ru.md` to absorb voice.
2. **Before changing motion**: read `agents/motion/out.md` to understand the 5-ease vocabulary.
3. **Before changing layout**: read `agents/design/out.md` to understand the chapter structure.
4. **Always preserve**: 14 sections, palette tokens, font families, RU/RO attribute contract.
5. **Always validate**: open in browser, scroll through, screenshot critical sections, check `prefers-reduced-motion` still works.
6. **Always document**: append a one-paragraph entry to HANDOFF.md saying what you changed and why.

---

## Validation checklist (before claiming done)

- [ ] `wc -l index.html` — should be ~3,400-3,500
- [ ] `grep -c "<section" index.html` — must be exactly 14
- [ ] `grep -c "data-ru=" index.html` — must equal `grep -c "data-ro=" index.html`
- [ ] `grep -ci "привилегия\|премиальный\|эксклюзивный\|уникальный\|абонемент\|бенефиты" index.html` — must be 0
- [ ] No mixed-script words: `grep -P "[а-я][a-z]|[a-z][а-я]" index.html` — must be 0 (or only in attribute values like `class` names)
- [ ] Browser test at 1440x900 + 390x844 — no console errors
- [ ] RU/RO toggle works — text actually swaps
- [ ] `prefers-reduced-motion: reduce` — no animation, all counters show final value

---

## Things that will make Vlad angry

- Adding new font families without asking
- Adding new color tokens without asking
- Adding a `<section>` block
- Removing the language toggle
- Removing the Three.js fog aura (he explicitly liked it)
- Removing the grain texture (he explicitly liked it)
- Using "Привилегия" / "Премиальный" / "Эксклюзивный" in any Russian copy
- AI-poetic slop ("Это не просто X, это Y" patterns)
- Mixed Cyrillic/Latin in the same word
- Emoji in copy or title
- Em-dash abuse ("—") — use at most 1 per paragraph
- Removing the RU/RO toggle (Vlad is bilingual and will toggle)
- Breaking the `prefers-reduced-motion` fallback
- Breaking the IntersectionObserver pause for Three.js

---

## How to verify your work

```bash
# File integrity
wc -l index.html
grep -c "<section" index.html

# RU/RO parity
grep -c "data-ru=" index.html
grep -c "data-ro=" index.html

# Banned words
grep -ci "привилегия\|премиальный\|эксклюзивный\|уникальный\|абонемент\|бенефиты" index.html

# Mixed-script check
grep -P "[а-я][a-z]|[a-z][а-я]" index.html | head -5

# Open in browser
open index.html

# Mobile test (after page loads, resize window to 390px or use DevTools)
```

---

## Questions?

Vlad is bilingual (Russian primary, Romanian native) and uses WhatsApp as primary chat. Don't ask permission for obvious moves — act, document in HANDOFF.md, keep moving.
