# Woloshin Club · Copy Critic (peer review, «редактор‑язычник»)

**File:** `v2/index.html` (RU copy on RU page; the Romanian version is identical structurally, but the Russian is what this audit reads)
**Lens (not visual, not strategic — purely linguistic):** sentences that sound translated-from-English, sentences that try to be poetic and land empty, hard ChatGPT-cliché rhythms, wrong-register words, phrases a real Moldovan/Russian person would never say.
**Tone target (Vlad):** direct, concrete, sometimes sharp. Never tries to be profound when concrete would do.
**Note:** the *Romanian* version is in many places cleaner than the Russian — the Russian reads more "translated" than "originally written in". That's a tell.

---

## Top 5 summary (the worst offenders)

| # | Location | Severity | Why it fails |
|---|---|---|---|
| 1 | **S08 headline** | CRITICAL | "Что открывает пятьдесят тысяч" — ungrammatical Russian. The headline literally asks a question a reader has to puzzle over. |
| 2 | **S04 body / S02 manifesto / S08 microcopy** | CRITICAL | Same sentence pasted into two different sections (`Woloshin Banya живёт по одному правилу — каждый жест выбран до того, как его попросят`). Page reads auto-generated. |
| 3 | **S07 subhead (line 2035)** | CRITICAL | Three AI-clichés in one sentence — `Это не X. Это Y` + `раньше, чем вы откроете рот` + `работает для вас` calque. |
| 4 | **S09 calendar (line 2291)** | CRITICAL bug | `Анти-реvelion` — Latin letters `velion` mixed into Cyrillic text inside `data-ru`. Visible artifact, fix to `Анти-ревельон` or replace entirely. |
| 5 | **"Это не X — это Y" / "Не X" rhythm** | CRITICAL (structural) | Used **4 times** across S01, S04, S07, S11. Plus `Не ваучер` (S07), `Не автоматическое письмо` (G copy). It is the page's most repeated sentence-shape — and it is the most ChatGPT-fingerprinted sentence-shape. |

---

## Per-section findings

### S01 · NAV — `nav__brand`, `nav__menu`, `nav__cta`

- **`nav__brand sub`** = `Издание I · 2026` — **MINOR**. "Издание I · 2026" reads like a book's colophon (`© Издание I · 2026`) and uses the formal Russian "издание" but as a tiny sub-label under an English-looking `WOLOSHIN · CLUB`. A Russian native would use one or the other — either the full `WOLOSHIN · CLUB · ИЗДАНИЕ I · 2026` line (as one block, tracked uppercase like the hero eyebrow does on line 1837), or nothing. Right now it's a third, half-formatted label. **Rewrite:** drop the sub entirely, OR keep it but align `text-transform: uppercase` + the same tracked Inter style the hero eyebrow uses.

---

### S01 · Hero — `hero-sub`, `hero-headline`

- **`hero-sub`** = *"Это не абонемент. Это место за столом — в Woloshin Banya, у леса. Те, кто сейчас внутри, решают, кто войдёт следующим."* — **CRITICAL**. Three AI-slop tics in one sentence:
  1. The opening **"Это не X. Это Y."** is *the* signature ChatGPT sentence-shape.
  2. "Те, кто сейчас внутри, решают, кто войдёт следующим" — bare noun phrase, no concrete subject doing a concrete verb. In Russian it would parse as "those who are currently inside decide who comes in next" — but in fact it's Woloshin who decides (the 50 members collectively), not "those who are inside". This is loose philosophical phrasing — sounds important, says nothing concrete.
  3. The whole subhead is *explaining what it isn't* before telling us what it is. Pure copywriting tech.
  
  **Rewrite:** "Место за столом. В Woloshin Banya, у леса. Пятьдесят человек, из которых вы — один. Если попросите." — shorter, more direct. Or even: "Пятьдесят имён за столом, в Woloshin Banya, у леса. Вы не заходите — вас впускают."

- **`hero-headline`** = *"Пятьдесят членов. Ни одного сверх."* — **MINOR**. "Ни одного сверх" is a calque of Romanian **"Niciunul în plus"** → literally "not a single *more*" → Russian translator's "сверху" → wrong Russian. A Russian native says either "и точка" (and that's it) or "Пятьдесят. И никого сверх." — but more naturally just "Пятьдесят. И всё." or "Пятьдесят. Точка." The current line is grammatically fine, just feels engineered, not spoken. **Rewrite:** "Пятьдесят. И ни одного сверх." — pull the period-rhythm tighter. (Note: source `copy-ru.md` ships "Ни одного сверх." exactly; the entire `copy-ru.md` file shows the Romanian Calque Syndrome — phrases lifted 1:1 from the Romanian. This is the root cause: source was written in Romanian, then "translated" word-by-word to Russian. The whole file should be re-voice-tested in Russian first.)

---

### S02 · Manifesto — `manifesto__line`

- **`manifesto__line[2]`** = *"В Woloshin каждый жест — от халата до разговора — выбран до того, как его попросят."* — **CRITICAL** (for reasons in §S04 below — same sentence appears in two places on the page).
  Plus line-internal: "от халата до разговора" is the Russian "from X to Z" framing — Russians don't usually gloss "одна вещь... до другой вещи" with this idiom; they'd write "с халата и до разговора" or break the list. "From halat to conversation" sounds like English-list idiom translated word-by-word.
- **`manifesto__line[3]`** = *"Здесь время носят иначе."* — **BAD**. "Носят время" — "time is worn". In Russian poetry "время" goes with "несут" (carried) or "проводят" (spent) or "держат" (held). "Носить" applied to time is AI-poetic but yields nonsense — maybe "так время не проводят; его держат". A native reading this tilts their head and says "what?". **Rewrite:** "Здесь время не считают." (Here time is not counted.) or "Здесь вечер не заканчивается — он догорает."

The manifesto as a block is good; the third line is the wrong note in it.

---

### S03 · The Number — `scarcity-grid__sub`, `scarcity-grid__legend`

- **`scarcity-grid__sub`** = *"Пятьдесят имён — под одной крышей."* — **MINOR**. Cute, fine. But "под одной крышей" is a tired Russian idiom (rhyme-cliché) — appears as the *warmth-fallback* of any "we're a community" copy. If the page needs the cliché, ok. If not, "Пятьдесят имён. За одним столом." mirrors the kitchen-table metaphor already in S07/S02/S10 and lands stronger.
- **`scarcity-grid__legend`** = *"Ниже — сколько осталось до пятидесяти."* — **MINOR**. "Ниже — сколько осталось" reads as instructions to the eye, not as a sentence the page is saying. The page is a place, not a kiosk UI. **Rewrite:** "Восемь пустых кресел осталось до полуночи." (eight empty chairs remain till midnight) — gives the dot-grid a tactile interpretation. Or simply remove and let the dots speak.

---

### S04 · The House — `house copy`, `house__copy p`, `italic-lead`, `house__refs`

- **`house__copy p`** *(line 1910)* = *"Woloshin Banya живёт по одному правилу — каждый жест выбран до того, как его попросят. Пар, дуб, тишина, разговор. Woloshin Club берёт этот принцип и переносит его в узкий круг из пятидесяти человек."* — **CRITICAL**.
  - The first sentence is **word-for-word identical** to S02 line 1872. Two sections of the same page literally reuse the same sentence. Reads as auto-generated.
  - "Woloshin Banya живёт по одному правилу" — metaphorical "живёт" applied to a building is fine in marketing Russian but it's been done; the actual idea is more like "Woloshin Banya работает по одному правилу" (works by one rule) — "живёт" sounds Russian as "lives" with the second sense "lives by" (живёт по...) which is acceptable. Actually OK here.
  - "Пар, дуб, тишина, разговор." — list of four nouns, period each. Tries to land like a recipe-of-the-house. Reads as if AI scanned a banya brochure and pulled the nouns. A native would say "У нас — дуб, пар, тишина, разговор." (one breath) or break differently.
  - "Woloshin Club берёт этот принцип и переносит его в узкий круг из пятидесяти человек." — *literally* "takes this principle and transfers it into a narrow circle of fifty". Office-speak. The metaphor was already strained; this clause kills it.
  
  **Rewrite:** "Woloshin Banya сначала был правилом: каждую вещь здесь подбирали до того, как о ней попросят. Пар. Дуб. Тишину. Разговор. Woloshin Club — то же правило, но в кругу пятидесяти."

- **`italic-lead`** *(line 1909)* = *"Не локация. Принцип: кто входит — выходит другим."* — **BAD**. The 4th instance of `Не X` rhetorical shape. Also "кто входит — выходит другим" is a known Russian-language-wisdom saying ("кто входит в реку — выходит другим"); it's *so* common the page can't claim it as fresh. **Rewrite:** either expand into a concrete verb: "Здесь не бывают дважды одинаковыми." (no one is the same after two visits) or simply "Дом, а не место." (a house, not a place).

---

### S05 · Spaces — `space-card captions`

- Mostly clean (cards are short, descriptive). One note:
- **`space-card[03]` caption** = *"И запрошенная тишина"* — **MINOR**. "Запрошенная" (past-passive participle, "asked-for") in spoken Russian is a learned-book word; in a poetic register on a card it works but most Russians would just say "Тишина — по запросу." or "Если попросите тишину." Borderline. **Rewrite:** "Если попросите тишину — будет." (If you ask for quiet — you'll get it.)

---

### S06 · Ritual — `ritual__body`

- This is the **strongest section on the page**. The seven beats read native. "Дуб. Тишина. Жар." / "Чай уже в чашке." / "Пальто возвращается на вашу вешалку — с запиской, которую вы не просили." — all clean. "Начинается, когда начинается." — strong. **Keep all seven.** No notes.

- One **MINOR** in title `Приход` (line 1982): "Приход" in Russian-marketing parlance works, but "Приход" is also slang for "доход" (revenue/earnings). On a card with no context someone glances at "Приход" and sees "Revenue". **Rewrite:** just "Вход" (entry) or "Шаг внутрь" or keep "Приход" because in context (after the page's earlier use) it's clear. Borderline.

---

### S07 · Privileges — entire `privileges__head italic-lead`, several rows

This is the section that most needs rewriting. Five issues stacked:

- **`privileges__head italic-lead`** *(line 2035)* = *"Привилегии — это не «бенефиты». Это то, как дом работает для вас — раньше, чем вы откроете рот."* — **CRITICAL**.
  - Open with a denial (rhetorical "X — это не Y" tic) — already disclaimed in section title `Не просите. Имеете.` two lines above.
  - "Как дом работает для вас" — `работает для` is English-trained Russian (`works for you`); Russian native says "устроено для вас" or "как вас здесь встречают".
  - "Раньше, чем вы откроете рот" — **the single most ChatGPT-clichéd Russian phrase** alongside `это ценно` and `в глубине души`. It's also the literal translation of English "before you open your mouth." A Russian native would say "прежде чем вы попросите" or "раньше, чем вы успеете сказать". Or remove the temporal clause entirely.
  - Net: an `Это не X. Это Y` sentence that uses a calque, an AI-cliché, and is followed directly by a section title that already said the same thing.
  
  **Rewrite:** "Дома вас встречают раньше, чем вы сами скажете, что нужно." (The house greets you before you say what's needed.) — short, concrete, with a verb doing the work.

- **`privilege-row[01] desc`** *(line 2050)* = *"Домашняя цена применяется автоматически, при каждом визите. Без купона. Без кода."* — **MINOR**. The last two short clauses are pure Hemingway-impersonation tic. Fine in English copywriting, slightly mannered in Russian. Better: "Каждый раз. Без кода." — drop the second negative (negative-stacking is itself an AI tic).

- **`privilege-row[03] desc`** *(line 2072)* = *"Каждое временное окно открывается для вас прежде, чем для всех."* — **BAD**. "Временное окно" is a calque of "time slot/time window." In Russian hospitality a native says "слот" (loan-word, common), "окно" (also ok with specialist context), or simply "Каждое время для бронирования открывается для вас за двое суток до всех остальных." Also the line restates the section title just above it ("Бронь — за 48 часов до публики"). The descriptor echoes the headline with no new info. **Rewrite:** "За двое суток до того, как слот открыт для всех, он уже ваш." or simply delete — the row's own label already says it.

- **`privilege-row[04] desc`** *(line 2083)* = *"Каждое масло, чай, вещь, созданная в Woloshin, приходит к вам раньше, чем попадёт в магазин."* — **BAD**. "Каждое масло, чай, вещь" = three bare singulars chained by commas is an AI tic (the comma-list-of-nouns). The grammar is "Each (oil, tea, thing)..." which doesn't parse in Russian singular-without-article. **Rewrite:** "Масла, чаи, вещи, сделанные в Woloshin, приходят к вам раньше, чем встают на полку в магазине."

- **`privilege-row[06]`** is the strongest item on the page and should be kept verbatim: *"В малых группах по восемь. Вечер заканчивается, когда заканчивается. Без повестки."* — This is what native Russian sounds like with Vlad's tone. (Note: same `заканчивается, когда заканчивается` phrase also appears in S09 line 2267 event #1 desc. Once is fine. Twice in adjacent sections is rhythmic over-repetition. Move `Без повестки` into one of them only and let the other vary.)

- **`privilege-row[08] desc`** *(line 2127)* = *"Вещь или ритуал, выбранный в этом году для вас. Не ваучер."* — **MINOR**. "Вещь" is the blandest possible word. The page already bans "бонус / сюрприз" in the word-choice guide; "вещь" is the same family. And "Не ваучер" is the 6th `Не X` denial in the page. **Rewrite:** "В этом году для вас приготовлено что-то одно. Не подарок и не купон." — or simpler: "Что-то — мы ещё не решили что. Скоро."

---

### Scarcity block (between S07 and S08)

- **`scarcity-block title`** = *"Осталось восемь мест"* — fine.
- **`scarcity-block__sub`** = *"42 из 50 имён уже за столом."* — fine, concrete.
- **`scarcity-grid__legend italic-lead`** *(line 2216)* = *"Когда станет пятьдесят, сайт закроется. Дверь не откроется до второго издания."* — **MINOR**. "Сайт закроется" — *literally* "the site will close" — sounds like a SaaS contract termination. The page is selling a club, and the metaphor of "site closing" breaks the spell. **Rewrite:** "Когда станет пятьдесят, страница исчезнет. До второго издания двери больше не будет."

---

### S08 · The Door — `h2`, `price-italic`, `price-numeral`, `price-subline`

- **`h2`** *(line 2227)* = *"Что открывает пятьдесят тысяч"* — **CRITICAL**. This is the section *named* "ВОЙТИ В КЛУБ" — about the price — and the headline is a Russian-language interrogative that doesn't parse. "Что открывает 50 тысяч" means "What 50k unlocks" but the Russian reader pauses: "что-что открывает? ... 50 000 чего?" because `50 000` mid-Russian-clause with no noun is unnatural. The intended reading comes only after seeing the price numeral right below. The headline fails its job.
  
  **Rewrite (Vlad tone, direct):** "Один платёж. Пятьдесят тысяч. Без рассрочки." — drops the chrome, names the number, names the key constraint. Or "50 000 MDL. Один раз. На всю жизнь." Or trust the copy-ru.md alternate **"Пятьдесят тысяч. Одна жизнь в клубе."** (which at least has a number-noun structure Russian can parse).

- **`price-italic`** *(line 2228)* = *"Один платёж. Доступ на всю жизнь."* — **CRITICAL bug**. The section's subhead and the source `copy-ru.md` both originally said `Один платёж. Две части: годовой взнос... и личный счёт...` — the page background section that explains 10K + 40K split. That whole explanatory subhead is **missing** from the page (it's absent from the screenshot and from the HTML). What's there instead is `Один платёж. Доступ на всю жизнь.` — a half-truth with no detail. **CRITICAL because it's not just bad copy, it's missing copy**: a buyer who sees `50 000 MDL · доступ на всю жизнь` and the microline `молдавских леев · единый взнос за вход` has no idea that the sum is 10K annual + 40K deposit. They will ask. Better to tell now. **Rewrite:** restore the explanation from `copy-ru.md F·f`: italic = *"Один платёж. Две части: 10 000 — годовой взнос клубу, 40 000 — ваш депозит в доме."* Or split: *"50 000 MDL. Из них 10 000 — взнос клубу. 40 000 — ваш личный счёт в доме."*

- **`price-subline`** *(line 2235)* = *"пятьдесят тысяч леев · доступ на всю жизнь"* — **MINOR**. This phrase **also repeats `доступ на всю жизнь` which appeared in the line directly above** (`price-italic`). Two adjacent lines both end on the same promise. **Rewrite:** drop `доступ на всю жизнь` from the subline; replace with the structural detail: *"50 000 леев · взнос клубу + ваш счёт"*.

- **`price-unit`** *(line 2236)* = *"молдавских леев · единый взнос за вход"* — fine but **redundant** with the line above. The reader has now seen `пятьдесят тысяч леев` AND `молдавских леев` within 30px of each other. **Drop one.** Keep `молдавских леев · один платёж` and let the money-symbol carry the rest.

---

### S09 · Calendar — `italic-lead`, event descriptions

- **`italic-lead`** *(line 2252)* = *"Три вечера в году, закрытых для публики, открытых для вас. Без телефонов. Без протокола. Без кадров."* — **MINOR**.
  - "Без кадров" is ambiguous: in Russian it can mean "without staff/extras" (ка́дры = executives/extras slang), "without footage", or "without actors". In context it has to mean "without being filmed". Russian would say **"Без съёмки."** or "Телефоны — в сторону." A reader who doesn't pick the "filming" reading on first read will re-read.
  - The Hemingway short clauses (`Без X. Без Y. Без Z.`) work in English but read slightly mannered in Russian. Acceptable here since they accumulate emotional weight. Keep, but **swap "Без кадров" → "Без съёмки"** to fix the ambiguity.

- **Event #1 desc** *(line 2267)* = *"Вино подобрано, восемь мест, общий стол. Вечер заканчивается, когда заканчивается."* — fine. But notice "Вино подобрано" — short neuter past passive — voice-passive opening is itself slightly English; Russian native would say "Вино подбирает сомелье" or "Вино подобрано заранее" or just "Подобранное вино, восемь мест, общий стол." **MINOR**.

- **Event #3 desc** *(line 2291)* = *"Анти-реvelion. Чтение в полночь, чай, тишина, три комнаты."* — **CRITICAL BUG**: the `data-ru` attribute contains **mixed Latin/Cyrillic** characters: `Анти-реvelion` (the tail `velion` is Latin). The visible inner-text uses Latin "Anti-revelion" so the live page shows the Romanian-only form. But:
  1. The `data-ru` value is broken — anyone reading the source can see the encoding corruption.
  2. The Russian reader never gets a Russian word for "celebration before New Year's" — the page just borrows "revelion" via the Romanian.
  3. The headline `Новый год, рано` already says what this is. **Rewrite data-ru** to: `Анти-ревельон. Чтение в полночь, чай, тишина, три комнаты.` — and the visible inner text becomes the same Russian text.

---

### S10 · The Numbers — `h2`, `ring__caption`, `numbers-italic`

- **`h2`** *(line 2306)* = *"Пятьдесят. Три. Два."* — fine; mirrors hero cadence.
- **`ring[01] caption`** *(line 2352)* = *"Пятьдесят имён. И всё. Больше никогда."* — fine. Strong.
- **`ring[02] caption`** *(line 2394)* = *"Три ночи, закрытые для публики, открытые для вас."* — **BAD**. This is **the fourth time** the page says "закрытые для публики, открытые для вас" or near-equivalent: S09 subhead (line 2252) says *"закрытых для публики, открытых для вас"*; S09 event #1 desc says it variantly; ring[01] caption repeats "пятьдесят имён ... больше никогда"; now ring[02] says it again. The ring caption should give **information unique to the second number**, not echo S09 subhead. **Rewrite:** "Три ночи, на которых решается год." — vague, but at least adds. Or: "Три вечера, ради которых стоит быть членом клуба."

- **`numbers-italic`** *(line 2441)* = *"Пятьдесят имён. Три вечера. Два ужина с основателем. Остальное — заслуживается."* — **BAD**. The pattern `X. Y. Z. Остальное — [abstract verb].` is an AI structural tic (parallel phrases + a meta-gloss). "Заслуживается" (passive middle, "earns itself") is a chameleon word — sounds deep, can land anywhere. A real person writes "Остальное придёт само." (the rest will come on its own). Or drop the closing clause and let the three numbers stand. **Rewrite:** "Пятьдесят имён. Три вечера. Два ужина с основателем. Остальное — дело времени." (Rest is a matter of time.) Or: "Пятьдесят. Три. Два. Третье измерение — ваше."

---

### S11 · The Host — `italic-lead` (h2), body p[1], body p[2], `placeholder-frame__label`

- **`h2 italic-lead`** *(line 2490)* = *"Добро пожаловать. Я — Рареш. Буду ждать у двери."* — fine. Establishes character. Don't touch.
- **`body p[1]`** *(line 2491)* = *"Клуб — мой дом с тех пор, как я его открыл. И каждый член клуба чувствует его своим — и это радует меня больше всего."* — **BAD**.
  - "Клуб — мой дом с тех пор, как я его открыл." — fine.
  - "И каждый член клуба чувствует его своим" — fine.
  - "— и это радует меня больше всего." — **CRITICAL** AI-flavoured closing. The classic "and that makes me most happy" is a ChatGPT-endorsement-flavoured sign-off. A real host writing to perspective members does not close his brief statement with a confession of personal happiness. **Rewrite:** remove the trailing clause entirely, OR replace with action: "— поэтому я здесь каждый вечер." (which is why I'm here every evening.) Or: "— поэтому я никуда из него не уеду." (which is why I won't leave.)  
  Full rewrite: *"Клуб — мой дом. Он открылся восемь лет назад. Я здесь каждый вечер с тех пор."*

- **`body p[2]`** *(line 2495)* = *"Ваш администратор — это один человек, не команда. Он знает, к которому часу вы приходите, что пьёте, с кем. Отвечает в тот же день — по-русски, по-румынски или по-английски."* — **CRITICAL**.
  - "Ваш администратор — это один человек, не команда" — **fifth** `Это X — не Y` denial, third **`Это не X — это Y`** denial on the page.
  - "Знает, к которому часу вы приходите" — "к которому часу" (to which hour) is grammatically correct formal Russian but **sounds translated from adjectival-Rom** ("the hour at which you arrive"). Russian native writes: "знает, во сколько вы приходите" or "знает ваше время" or "знает, к которому часу" (acceptable formal). But on the page where the rest of the S11 voice tries to be warm, "к которому часу" reads courtroom-stenographic. **Rewrite:** "Он знает, во сколько вы приходите."
  - "Отвечает в тот же день — по-русски, по-румынски или по-английски." — fine, no notes.
  - Net: the S11 body **re-establishes what S07 subhead already established**, more clumsily. S07 subhead (line 2035) says privileges are about "дом работает для вас раньше, чем откроете рот"; S11 rephrases "администратор — один человек, не команда" with the same content, plus a new "knows what you drink" beat. **Action:** cut S11 body p[2] entirely. The bit about "знает, к которому часу вы приходите" can move into S07 privilege#01 (line 2050) as a one-liner closing: "Домашняя цена применяется автоматически. Администратор знает, во сколько вы приходите, и не спрашивает."

- **`placeholder-frame__label`** *(line 2485)* = *"Рареш · хозяин клуба"* — fine, sign-off label only.

---

### S12 · Closing — `h2`, scroll-prompt, CTA

- **`h2`** = *"Дверь открывается один раз за вечер."* — fine.
- **`scroll prompt`** *(line 2519)* = *"Прокрутите, чтобы продолжить"* — **MINOR**. "Прокрутите" in Russian UI-speak is fine for software but on a luxury brand page reads as browser-default. A real Russian native would write "↓ Дальше — форма заявки" or just remove it (the section right below has the CTA). The phrase is also explaining visual UI in words — pure translation-of-English-UX-cue. **Rewrite:** remove or replace with the same direction as the page's own language.
- **`S12 closing CTA`** = `"Подать заявку"` — fine.

---

### S13 · Form — labels, submit, success, micro-meta

- **`Email label`** = `Электронная почта` — fine.
- **`Phone label`** = `Телефон · необязательно` — fine.
- **`Submit`** *(line 2558)* = *"Отправить. Потом — тишина. Мы вернёмся."* — fine, **strong**, keep.
- **`Privacy micro`** *(line 2559)* = *"Данные остаются в доме. Третьим лицам не передаются."* — fine.

- **`Heading`** *(line 2532)* = *"Расскажите о себе — несколько строк."* — fine.

- **`Italic under heading`** *(line 2533)* = *"Отвечаем за 48 часов. Или раньше."* — **INCONSISTENCY**. The success message *(line 2564)* says *"Администратор клуба свяжется с вами в течение 24 часов."* The page promises 24 hours when the user has finished filling the form, but promises 48 hours before. Same page, two different promises. **Fix:** unify. Use 24 throughout (faster, more honest) or 48 throughout (more realistic for a small club).

---

### S14 · Footer — `address__col`, legal micro

- All contact lines fine. Note:
- **`Woloshin Banya SRL. Кишинёв, Республика Молдова.`** — fine.
- **`micro-legal`** *(line 2604)* = *"Woloshin Club — программа Woloshin Banya и работает по правилам дома."* — fine.

---

## Cross-cutting structural findings

### 1. Romanization Calque Syndrome (the root cause of most issues above)

The `copy-ru.md` source document was clearly drafted with Romanian as the working language; the Russian text reads as a near-literal translation. Evidence:
- "Не X" — straight calques of Romanian "Nu este X" / "Nu X." (Nu este un abonament → Это не абонемент; Nu o locație → Не локация; etc.)
- "временное окно" → "fereastra de timp"
- "сверх" in "ни одного сверх" — direct map of "în plus" → "сверху" (not a Russian-speaking-native choice)
- "переносит в узкий круг" → "transferă în cercul restrâns" — translated phrase patterns
- "Plural-of-bare-nouns list" ("масло, чай, вещь") directly maps "ulei, ceai, obiect"
- **Data-ru** for S09 line 2291 contains `Анти-реvelion` — the corruption reveals that the original text was drafted as "Anti-revelion" in Latin charset, then not properly re-typed into Cyrillic for the Russian attribute.

**Action:** re-voice the Russian from scratch. Drop every `Это не X. Это Y.` sentence and replace with a positive single statement. Drop every sentence that begins with `Не`. Use the Russian sentence-test: read each aloud. If the rhythm feels translated from Romanian, rewrite.

### 2. The `Это не X — это Y` denial pattern

Six occurrences across the page (and one more implied "Не ваучер"):

| # | Section | Sentence | Fix |
|---|---|---|---|
| 1 | S01 hero-sub | "Это не абонемент. Это место за столом..." | → "Место за столом, в Woloshin Banya, у леса." |
| 2 | S04 italic-lead | "Не локация. Принцип..." | → "Дом, а не место." |
| 3 | S07 italic-lead | "Привилегии — это не «бенефиты». Это..." | → "Дома вас встречают раньше, чем вы сами скажете." |
| 4 | S07 #08 desc | "...Не ваучер." | → drop or replace |
| 5 | S07 #01 desc | "...Без купона. Без кода." | → "Каждый раз. Без кода." (cut one negative) |
| 6 | S11 body p[2] | "...это один человек, не команда..." | → "Один человек, а не команда. Знает, во сколько вы приходите." |

**Action (mechanical):** rewrite the page so that the count of `Это не X` / `Не X`-denial sentences ≤ **2 across the entire page**. (Possibly zero.) In its place use direct positive verbs.

### 3. `раньше, чем вы ...` anticipatory poetry (also a ChatGPT tic)

- S01 hero-sub: "решают, кто войдёт следующим" — anticipatory
- S07 italic-lead: "раньше, чем вы откроете рот" — anticipatory
- S07 #04 desc: "раньше, чем попадёт в магазин" — anticipatory
- S07 #04 row label: "раньше рынка" — anticipatory

Four hits. **Action:** keep *one* (the strongest — "раньше, чем попадёт в магазин"), rewrite the rest.

### 4. Sentence duplication across sections

| Line | First appearance | Duplicated in |
|---|---|---|
| "Woloshin Banya живёт по одному правилу — каждый жест выбран до того, как его попросят." | S02 line 1872 | S04 line 1910 (identical) |
| "Вечер заканчивается, когда заканчивается." | S09 event-1 line 2267 | S07 privilege-06 line 2105 |
| "закрытых для публики, открытых для вас" (or near) | S09 italic line 2252 | S10 ring[02] caption line 2394 |
| "Пятьдесят имён" openers | S03 line 1889, S09 line 2251, S10 ring caption 2352 | S07 implied |

**Action:** make each section earn its repetition by varying the verb/noun structure, or move to a single canonical spot.

### 5. Vertical over-stuffing

The page says each major section ~2–3 times: once in hero, once in section title, once in body, once more in the closing line. The "Admin knows you" beat appears in S07 headline (`Не просите. Имеете.`), S07 italic-lead, S11 h2 ("Буду ждать у двери"), S11 body p1, S11 body p[2] — **5 times**. A reader who finishes the page feels *told at*, not addressed.

**Action:** the admin-as-differentiator beat is the strongest single claim on the page (and `copy-ru.md` already says "если абзац нужно убрать — не убирайте этот"). **Consolidate**: keep it ONLY in S07 #01 + S11 p[1]. Cut the rest.

### 6. Words that betray translator-language register

| Word | Where | Why it's bad Russian (when on a luxury brand page) |
|---|---|---|
| сверх | S01 "ни одного сверх" | calque from "în plus"; Russian says "лишних" |
| работает для | S07 subhead | calque from "works for you"; Russian says "делается для" or "устроено для" |
| откроете рот | S07 subhead | brand-cliché; native Russian avoids |
| временное окно | S07 row #03 | calque from "time window"; native Russian says "слот" or names the slot directly |
| принцип | S04 body | meta-jargon; Russian native would say "правило" — already used earlier |
| переносит в узкий круг | S04 body | office-speak; native says "и теперь — для пятидесяти" |
| привилегии | S07 title | sounds HR/insurance; source copy words-guide *explicitly bans this*. Use "права дома" or keep title as `Не просите. Имеете.` |
| бенефиты | S07 subhead (in quotes) | English loan-word even when denied — keep quote, change the surrounding line |
| кадров | S09 subhead | ambiguous Russian; "съёмка" is clear |
| узкий круг | S04 body | cliché; "круг из пятидесяти" or "пятидесяти" sufficed already |

---

## Tone-violation examples (force-quotes from the page)

> "Не просите. Имеете."  →  **ТАК ЗВУЧИТ VЛАД.** ✔ Keep.

> "Дуб. Тишина. Жар."  →  ✔ Keep.

> "Пальто возвращается на вашу вешалку — с запиской, которую вы не просили."  →  ✔ Keep.

> "Отправить. Потом — тишина. Мы вернёмся."  →  ✔ Keep.

> "**Это не абонемент. Это место за столом** — в Woloshin Banya, у леса."  →  ❌ Replacement:  *"Место за столом. В Woloshin Banya, у леса. Пятьдесят человек, среди которых вы."*

> "**Привилегии — это не «бенефиты».** Это то, как дом работает для вас — раньше, чем вы откроете рот."  →  ❌ Replacement:  *"Что здесь — то ваше. Спросить не нужно."*

> "**Ваш администратор — это один человек, не команда.**"  →  ❌ Replacement:  *"Один человек. Знает, во сколько вы приходите, что пьёте, какой стол любите."*

> "**Остальное — заслуживается.**"  →  ❌ Replacement:  *"Остальное — дело времени."*

> "**Что открывает пятьдесят тысяч**"  →  ❌ Replacement:  *"50 000 MDL. Один платёж. Без рассрочки."*

---

## Three top fixes (the ones that move the page from "shippable" to "loved")

**The audit-file, the eye, the Russian ear.** Different lenses, same conclusion: the S07 subhead, the S08 headline, the S04 body, and the S11 body p[2] are carrying copy that no Russian-native speaker would write. Replacing those four blocks with the seven-line rewrites in this file would remove ~80% of the AI-fingerprint smell on the page. The remaining sections (S01 headline, S05 captions, S06 ritual, S09 events, S13 form, S14 footer) read native or near-native and should be left alone.

---

## Files I read while making this critique
- `/Users/pro/Documents/Projects/Woloshin_club/v2/index.html` — the page in full (extracted every Cyrillic `data-ru` attribute and every visible Russian line)
- `/Users/pro/Documents/Projects/Woloshin_club/v2/agents/copy-ru.md` — source copy
- `/Users/pro/Documents/Projects/Woloshin_club/v2/agents/final-audit.md` — visual audit (different lens, complementary)

**Critic note for the parent agent:** the source `copy-ru.md` was clearly drafted with Romanian primacy. A 30-minute pass that re-voices `copy-ru.md` from scratch in Russian (no Romanian reference) would generate better RU-on-page copy than any amount of patching the current translated version. Recommend assigning the rewrite task in that mode.
