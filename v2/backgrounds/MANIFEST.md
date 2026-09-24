# Backgrounds Manifest — Woloshin Club v2

> **Status:** All entries below are **SVG CSS fallbacks** — generated because
> `gflow` auth was **expired** at the time of execution. Re-run via gflow when
> auth is restored and replace the `.svg` files with `.png` outputs.
>
> **Reason for fallback:** `gflow auth --status` returned
> *"Cookies saved but session expired: Session endpoint returned no access_token."*
> Per task rules: do NOT automate re-auth. User must run
> `gflow auth --clear && gflow auth` manually.

## Files (this batch — 5 mid-page backgrounds)

| File | Section | Aspect | Format | Size | gflow? | Notes |
|------|---------|--------|--------|------|--------|-------|
| `S02-manifesto-bg.svg` | S02 Manifesto | 16:9 (1600×900) | SVG fallback | ~2.4 KB | ❌ expired | Deep darkness + subtle warm radial glow upper-left, soft candlelight blur, vignette + heavy film grain. No symbols/text. |
| `S04-house-bg.svg`     | S04 The House   | 16:9 (1600×900) | SVG fallback | ~3.0 KB | ❌ expired | Abstract stone-wood ritual texture (anisotropic noise overlay), warm umber base + faint amber haze upper-right, heavy grain. No figures/text. |
| `S05-spaces-bg.svg`    | S05 The Spaces  | 21:9 (2100×900) | SVG fallback | ~4.2 KB | ❌ expired | Cinematic dark + bottom-center firelight glow + horizontal fog bands + scattered warm embers along bottom edge + vignette + heavy grain. |
| `S06-ritual-bg.svg`    | S06 The Ritual  | 9:16 (900×1600) | SVG fallback | ~2.8 KB | ❌ expired | Near-pure black + thin warm center-line gradient (suggests time axis), strong vertical grain, edge vignette, heavy grain. Tileable vertically. |
| `S07-privileges-bg.svg`| S07 Privileges  | 16:9 (1600×900) | SVG fallback | ~2.5 KB | ❌ expired | Midnight velvet base + faint gold gradient fade from top edge + soft sheen + vignette + heavy grain. |

## How to regenerate via gflow (when auth is back)

```bash
gflow auth --status              # confirm active
gflow generate-image "Abstract deep darkness with a single subtle warm amber radial glow from upper-left corner. Heavy film grain. No symbols, no figures, no text. Aspect 16:9. Minimal luxury mood." \
  --aspect-ratio 16:9 \
  -o /Users/pro/Documents/Projects/Woloshin_club/v2/backgrounds/S02-manifesto-bg.png

gflow generate-image "Abstract dark texture suggesting ancient stone ritual space. Very dark palette with subtle warm earth undertone, hints of warm amber and umber within deep midnight. Heavy grain. No figures, no text, no symbols. Aspect 16:9." \
  --aspect-ratio 16:9 \
  -o /Users/pro/Documents/Projects/Woloshin_club/v2/backgrounds/S04-house-bg.png

gflow generate-image "Cinematic abstract darkness with subtle firelight glow from bottom-center, like embers seen through fog. Deep midnight blue-black, warm amber undertones. Ultra-wide aspect 21:9. Heavy film grain. No figures." \
  --aspect-ratio 21:9 \
  -o /Users/pro/Documents/Projects/Woloshin_club/v2/backgrounds/S05-spaces-bg.png

gflow generate-image "Abstract vertical grain texture, almost pure black with very subtle warm amber gradient along a thin vertical center line. Heavy film grain. Aspect 9:16. No text, no symbols." \
  --aspect-ratio 9:16 \
  -o /Users/pro/Documents/Projects/Woloshin_club/v2/backgrounds/S06-ritual-bg.png

gflow generate-image "Deep midnight velvet darkness with a faint warm gold gradient fade from top edge. Subtle. Heavy film grain. Aspect 16:9. No text, no symbols." \
  --aspect-ratio 16:9 \
  -o /Users/pro/Documents/Projects/Woloshin_club/v2/backgrounds/S07-privileges-bg.png
```

After re-generating, delete the matching `.svg` files (or leave both — SVG can act as a `<img>` fallback while PNG loads).

---

## Files (this batch — 3 hero/section backgrounds, 2026-09-25 subagent)

| File | Section | Aspect | Format | Size | gflow? | Notes |
|------|---------|--------|--------|------|--------|-------|
| `S01-hero-bg.svg`    | S01 Threshold (Hero)  | 16:9 (1920×1080) | SVG fallback | 4.4 KB | ❌ expired | Cinematic midnight → warm amber haze from upper-right with a soft cream-amber light point, scattered ember dots, vignette, heavy film grain. Steam-haze done via low-frequency turbulence. No figures/text. |
| `S03-number-bg.svg`  | S03 The Number ("50") | 1:1 (1024×1024)  | SVG fallback | 2.2 KB | ❌ expired | Near-pure black with a single subtle warm ember light source in the lower-right corner. Strong central vignette pushes focus to where "50" will sit. Heavy grain. |
| `S12-closing-bg.svg` | S12 The Closing       | 16:9 (1920×1080) | SVG fallback | 3.7 KB | ❌ expired | Almost solid darkness + faint gold vertical slit in the center (doorway/portal) + warm light pooling at the floor + warm vertical gradient from bottom. Heavy grain. The fog in HTML should part to reveal the slit. |

### How to apply (integration agent)

```css
/* S01 — full hero, behind text */
.bg-S01 {
  position: absolute; inset: 0;
  background: url("backgrounds/S01-hero-bg.svg") center/cover no-repeat;
  opacity: 0.85;
  z-index: 0;
}

/* S03 — fixed bg behind the giant "50" */
.bg-S03 {
  position: fixed; inset: 0;
  background: url("backgrounds/S03-number-bg.svg") center/cover no-repeat;
  z-index: -1;
}

/* S12 — full section, fog overlays this */
.bg-S12 {
  position: absolute; inset: 0;
  background: url("backgrounds/S12-closing-bg.svg") center/cover no-repeat;
  z-index: 0;
}
```

All three fall back gracefully: SVG is vector (scales to any resolution, file size in KB, no network round-trip for browser cache). When gflow is re-authenticated, replace each `.svg` with a `.png` of the same stem and update the CSS path — or keep `.svg` as the production asset (it's actually the lighter option).

### How to regenerate via gflow (when auth is back)

```bash
gflow auth --status   # confirm active

gflow generate-image "Atmospheric luxury interior. Cinematic darkness. Volumetric golden fog drifting through a vast stone room. Single soft warm light source from upper-right. No figures. Abstract. Suggesting ritual space, sacred steam, ancient banya. Hyper-detailed film grain. Muted palette of deep midnight blue, charcoal, antique gold, warm amber. No text. No logos. Aspect 16:9." \
  --aspect-ratio landscape -o /Users/pro/Documents/Projects/Woloshin_club/v2/backgrounds/S01-hero-bg.png

gflow generate-image "Abstract dark texture. Almost pure black with a single warm amber ember light source in the lower-right corner, very subtle. Faint diagonal grain. No symbols, no text. Negative space dominant. Luxury minimal. Aspect 1:1." \
  --aspect-ratio square -o /Users/pro/Documents/Projects/Woloshin_club/v2/backgrounds/S03-number-bg.png

gflow generate-image "Abstract dark portal. Nearly black background. A very faint warm gold vertical slit in the center, like light through an almost-closed ancient door. Heavy grain. Atmosphere of threshold. No text. Aspect 16:9." \
  --aspect-ratio landscape -o /Users/pro/Documents/Projects/Woloshin_club/v2/backgrounds/S12-closing-bg.png
```
