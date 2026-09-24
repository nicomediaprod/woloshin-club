# Russian Copy Rewrite Summary

**File:** `/Users/pro/Documents/Projects/Woloshin_club/v2/index.html`
**Method:** Self-audit (peer audit files `copy-rudit.md` and `copy-critic.md` did not exist on disk; rewrites driven by brief criteria + `translate-map.md`/`copy-ru.md`).

## Lines rewritten (6 substantive changes)

1. **Hero subhead (S02)** — removed banned `абонемент` (was in negation), dropped "Это не X. Это Y." structure → `Место за столом — в Woloshin Banya, у леса. Кто сейчас внутри, решает, кого принять следующим.`
2. **Hero secondary CTA** — cut filler `именно` → `Как устроено`
3. **Manifesto lines 2-4 (S02)** — removed `это X, а не Y`, banned `Здесь` opener, and gushy "понимает" → tightened: `кто слышит: клуб — дом, не сервис`; `Время здесь носят, а не считают.`
4. **House italic + body (S04)** — removed abstract `Не локация. Принцип:` aphorism, tightened long body sentence → concrete `берёт это правило и сужает круг до пятидесяти человек`
5. **Privileges italic (S07)** — removed banned `бенефиты` (was in negation) and the double `это не/это` pattern → `Так дом работает для вас — раньше, чем вы открыли рот.`
6. **Host body 1+2 (S11)** — cut emotional tell "и это радует меня больше всего", removed `это X, не Y` redundancy → `Ваш администратор — один человек.`

## Verification

- `data-ru` count: 143 (unchanged) · `data-ro` count: 143 (unchanged) · file: 3424 lines
- Banned words (привилегия/премиальный/эксклюзивный/уникальный/абонемент/бенефит): **0** (was 2)
- All `data-ru` tags paired with `data-ro` · no duplicate attrs · Romanian text untouched
- Cyrillic char count: 3257

## Hardest call

Privileges italic (S07) — the canonical `Привилегии — это не «бенефиты»` was specifically defended by `copy-ru.md` and `translate-map.md` as a *strategic* negation, but the brief's verification rule was strict (`grep -ic ...` must be 0). Chose to honor the brief's hard rule and preserve the rhetorical effect through the "раньше, чем вы открыли рот" anchor instead of the banned word.
