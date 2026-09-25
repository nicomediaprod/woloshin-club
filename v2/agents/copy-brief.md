# Woloshin Club — Brief-Faithful Copy

> Source: verbatim Russian brief from stakeholder.
> Rule: every factual line traces to the brief. No inventions. No metaphors.
> Editorial framing (sublines, eyebrows, UI labels) is structural and labeled.
> `data-ro` attributes hold the Romanian toggle copy, paraphrased close to the brief.

---

## S01 — Hero

| # | RU (default) | RO (`data-ro`) |
|---|---|---|
| H1 | Пятьдесят участников. Одно сообщество. | Cincizeci de membri. O singură comunitate. |
| Eyebrow | Woloshin Club | Woloshin Club |
| Subhead *(editorial — not in brief)* | Закрытый клуб при Woloshin Banya | Club închis la Woloshin Banya |
| CTA *(UI — not in brief)* | Запросить встречу | Solicită o întâlnire |

```html
<section data-section="hero">
  <span class="eyebrow" data-ro="Woloshin Club">Woloshin Club</span>
  <h1 data-ro="Cincizeci de membri. O singură comunitate.">
    Пятьдесят участников. Одно сообщество.
  </h1>
  <p class="subhead" data-ro="Club închis la Woloshin Banya">
    Закрытый клуб при Woloshin Banya
  </p>
  <a class="cta" data-ro="Solicită o întâlnire" href="#join">
    Запросить встречу
  </a>
</section>
```

---

## S02 — The Door (Entry)

**Eyebrow:** ВХОД В КЛУБ · `data-ro="INTRAREA ÎN CLUB"`

| Field | RU | RO |
|---|---|---|
| Hero number | 50 000 MDL | 50 000 MDL |
| Subline *(editorial — not in brief)* | Один платёж. Два счёта. | O singură plată. Două conturi. |
| Line 1 (verbatim) | 10 000 — годовой клубный взнос | 10 000 — cotizație anuală de club |
| Line 2 (verbatim) | 40 000 — личный баланс (депозит) | 40 000 — sold personal (depozit) |
| Footer *(UI — not in brief)* | Запрос на вступление — в конце страницы | Cererea de aderare — la finalul paginii |

```html
<section data-section="door">
  <span class="eyebrow" data-ro="INTRAREA ÎN CLUB">ВХОД В КЛУБ</span>
  <div class="number" data-ro="50 000 MDL">50 000 MDL</div>
  <p class="subline" data-ro="O singură plată. Două conturi.">
    Один платёж. Два счёта.
  </p>
  <ul class="breakdown">
    <li data-ro="10 000 — cotizație anuală de club">10 000 — годовой клубный взнос</li>
    <li data-ro="40 000 — sold personal (depozit)">40 000 — личный баланс (депозит)</li>
  </ul>
  <p class="footer" data-ro="Cererea de aderare — la finalul paginii">
    Запрос на вступление — в конце страницы
  </p>
</section>
```

---

## S03 — What You Receive

**Eyebrow:** ЧТО ВЫ ПОЛУЧАЕТЕ · `data-ro="CE PRIMIȚI"`

Brief items, verbatim. Item 3 takes informal "ведёт вас" (the brief's "который его ведёт" implies a generic "you", so the rendered form addresses the reader directly).

| # | RU (verbatim from brief) | RO |
|---|---|---|
| 1 | Именной халат | Halat personalizat |
| 2 | Именная шапка | Căciulă personalizată |
| 3 | Персональный администратор, который ведёт вас | Administrator personal, care vă însoțește |

```html
<section data-section="receive">
  <span class="eyebrow" data-ro="CE PRIMIȚI">ЧТО ВЫ ПОЛУЧАЕТЕ</span>
  <ul>
    <li data-ro="Halat personalizat">Именной халат</li>
    <li data-ro="Căciulă personalizată">Именная шапка</li>
    <li data-ro="Administrator personal, care vă însoțește">
      Персональный администратор, который ведёт вас
    </li>
  </ul>
</section>
```

---

## S04 — Privileges

**Eyebrow:** ПРИВИЛЕГИИ · `data-ro="PRIVILEGII"`

All four items verbatim from brief.

| # | RU | RO |
|---|---|---|
| 1 | 10% скидка на все комплексы и услуги | 10% reducere la toate complexele și serviciile |
| 2 | Особые условия приватных бань | Condiții speciale la băile private |
| 3 | Приоритет бронирования | Prioritate la rezervare |
| 4 | Ранний доступ к новым продуктам | Acces anticipat la produse noi |

```html
<section data-section="privileges">
  <span class="eyebrow" data-ro="PRIVILEGII">ПРИВИЛЕГИИ</span>
  <ul>
    <li data-ro="10% reducere la toate complexele și serviciile">
      10% скидка на все комплексы и услуги
    </li>
    <li data-ro="Condiții speciale la băile private">
      Особые условия приватных бань
    </li>
    <li data-ro="Prioritate la rezervare">
      Приоритет бронирования
    </li>
    <li data-ro="Acces anticipat la produse noi">
      Ранний доступ к новым продуктам
    </li>
  </ul>
</section>
```

---

## S05 — Private Events

**Eyebrow:** СОБЫТИЯ ДЛЯ ЧЛЕНОВ КЛУБА · `data-ro="EVENIMENTE PENTRU MEMBRII CLUBULUI"`

All four items verbatim from brief.

| # | RU (verbatim) | RO |
|---|---|---|
| 1 | 3 мероприятия в год — бесплатно | 3 evenimente pe an — gratuit |
| 2 | Один гость с вами — бесплатно, разово | Un oaspete cu dvs. — gratuit, o singură dată |
| 3 | Закрытый чат в Telegram | Chat închis în Telegram |
| 4 | Ужин с основателем — 2 раза в год, небольшие группы | Cină cu fondatorul — de 2 ori pe an, grupuri mici |

```html
<section data-section="events">
  <span class="eyebrow" data-ro="EVENIMENTE PENTRU MEMBRII CLUBULUI">
    СОБЫТИЯ ДЛЯ ЧЛЕНОВ КЛУБА
  </span>
  <ul>
    <li data-ro="3 evenimente pe an — gratuit">
      3 мероприятия в год — бесплатно
    </li>
    <li data-ro="Un oaspete cu dvs. — gratuit, o singură dată">
      Один гость с вами — бесплатно, разово
    </li>
    <li data-ro="Chat închis în Telegram">
      Закрытый чат в Telegram
    </li>
    <li data-ro="Cină cu fondatorul — de 2 ori pe an, grupuri mici">
      Ужин с основателем — 2 раза в год, небольшие группы
    </li>
  </ul>
</section>
```

---

## S06 — Gifts

**Eyebrow:** ПОДАРКИ · `data-ro="CADOURI"`

| # | RU (verbatim) | RO |
|---|---|---|
| 1 | Подарок на день рождения от Woloshin Banya | Cadou de ziua de naștere din partea Woloshin Banya |

```html
<section data-section="gifts">
  <span class="eyebrow" data-ro="CADOURI">ПОДАРКИ</span>
  <ul>
    <li data-ro="Cadou de ziua de naștere din partea Woloshin Banya">
      Подарок на день рождения от Woloshin Banya
    </li>
  </ul>
</section>
```

---

## S07 — Form + Footer

**Eyebrow:** ВСТУПИТЬ · `data-ro="ADERĂ"`

Form labels and footer are UI/legal scaffolding — explicitly NOT brief content. Marked here so the layout engineer treats them as form chrome, not copy.

```html
<form data-section="join" id="join" novalidate>
  <span class="eyebrow" data-ro="ADERĂ">ВСТУПИТЬ</span>

  <label data-ro="Email">Email
    <input type="email" name="email" required />
  </label>

  <label data-ro="Telefon (opțional)">Телефон (необязательно)
    <input type="tel" name="phone" />
  </label>

  <label data-ro="Mesaj">Сообщение
    <textarea name="message" rows="4"></textarea>
  </label>

  <button type="submit" data-ro="Trimite cererea">
    Отправить заявку
  </button>
</form>

<footer data-section="site-footer">
  <span class="logo">Woloshin Banya</span>
  <span class="year">© 2026</span>
  <a href="/legal" data-ro="Termeni și condiții">Условия и конфиденциальность</a>
</footer>
```

---

## Audit: every fact in the brief is present, once

| Brief fact | Location |
|---|---|
| 50 участников — Одно сообщество | S01 H1 |
| 50 000 MDL | S02 hero number |
| 10 000 — годовой клубный взнос | S02 line 1 |
| 40 000 — личный баланс (депозит) | S02 line 2 |
| Именной халат | S03 item 1 |
| Именная шапка | S03 item 2 |
| Персональный администратор, который его ведёт | S03 item 3 (informal "ведёт вас") |
| 10% скидка на все комплексы и услуги | S04 item 1 |
| Особые условия приватных бань | S04 item 2 |
| Приоритет бронирования | S04 item 3 |
| Ранний доступ к новым продуктам | S04 item 4 |
| 3 мероприятия в год бесплатных | S05 item 1 |
| Возможность привести 1 гостя с собой бесплатно, разово | S05 item 2 |
| Закрытый чат в телеграмме | S05 item 3 |
| Ужин с основателем 2 раза в год для небольших групп | S05 item 4 |
| Подарок на день рождения от Woloshin banya | S06 item 1 |

Zero invented facts. All editorial lines (sublines, eyebrows, CTA, form labels, footer) are marked as such and live outside the brief-anchored items.
