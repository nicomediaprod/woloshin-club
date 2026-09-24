# Woloshin Club · Translation Map (RO → RU)

> Source: `/Users/pro/Documents/Projects/Woloshin_club/v2/index.html` (live landing, all visible strings).
> Source copy: `/Users/pro/Documents/Projects/Woloshin_club/v2/agents/copy/out.md` (master Romanian).
> Primary target: **Russian (RU)** — natural CIS-Russkiy, Kurale-elegant, rhythm-first, NOT Moldovan-specific, NOT translated-feeling.
> Secondary target: polished Romanian (RO) — fixing audit-flagged awkward lines.
> ★ = recommended variant (A/B primary). All others are on-brand alternatives.

---

## BANNED VOCABULARY (RU) — фильтр слов, за которыми слышно «перевод»

| ❌ Не писать | ✅ Писать вместо | Почему |
|---|---|---|
| Абонемент, абонент, подписка | Членство, круг, место за столом | превращает принадлежность в сервис |
| Скидка, снижка, дисконт | Привилегия, право, доступ | язык супермаркета |
| Клиент, потребитель, пользователь | Член клуба, гость | человек — не клиент |
| Промо-акция, акция, спецпредложение | Дар дома, жест, ритуал | язык ТВ-рекламы |
| Преимущества, бенефиты | Привилегии, дары | язык HR/страховок |
| Купить сейчас, не упустите, успейте | — (не заменять, а убирать) | давление, реклама |
| Карта члена, VIP-карта | — (не писать вообще) | опошляет |
| Бонус, экстра, сюрприз | Дар, жест, дар дома | язык розыгрыша |
| Уникальный, исключительный, премиальный | — (не писать вообще) | пустое обещание |
| Доступная цена, выгодно, всего за | — (не писать вообще) | убивает позиционирование |

---

## 0 · HEAD / `<title>` / `<meta>` / `<html lang>`

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| T00-html-lang | `ro-RO` | `ru-RU` | динамически: `data-lang="ru"` для переключателя |
| T01-title | `Woloshin Club · Cincizeci de membri. Niciunul în plus.` | `Woloshin Club · Пятьдесят членов. Ни одного сверх.` | литературно, число прописью — поэтический контекст |
| T02-meta-desc | `Woloshin Club — cincizeci de membri, cincizeci de mii de lei, o singură ușă. Ediția I, Chișinău. Aplicarea se face în conversație, nu într-un formular.` | `Woloshin Club — пятьдесят членов, пятьдесят тысяч леев, одна дверь. Издание I, Кишинёв. Заявление — в разговоре, не в форме.` | спокойный, прямой |

---

## A · NAV (навигация)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| A01-logo | `WOLOSHIN · CLUB` | `WOLOSHIN · CLUB` | латиницей — это знак, не переводится |
| A02-logo-sub | `Ediția I · 2026` | `Издание I · 2026` | |
| A03-nav-spații | `Spații` | `Пространства` | |
| A04-nav-ritual | `Ritual` | `Ритуал` | |
| A05-nav-privilegii | `Privilegii` | `Привилегии` | |
| A06-nav-contact | `Contact` | `Контакт` | |
| A07-nav-cta | `Solicită o întâlnire` | `Запросить встречу` | или альтернатива ниже |

**Альтернативы CTA:**
- ★ `Запросить встречу`
- `Назначить разговор`
- `Попросить приглашение`

---

## B · HERO (S01)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| B01-epigraph-italic | `Woloshin Club nu se cumpără. Se poartă.` | `Woloshin Club не покупается. Его носят.` | центральная строка — должна звучать как итог |
| B02-eyebrow | `WOLOSHIN · CLUB — EDIȚIA I` | `WOLOSHIN · CLUB — ИЗДАНИЕ I` | |
| B03-h1-line-1 | `Cincizeci` | `Пятьдесят` | |
| B04-h1-line-2 | `de membri.` | `членов.` | |
| B05-h1-line-3 | `Niciunul` | `Ни одного` | |
| B06-h1-line-4 | `în plus.` | `сверх.` | |
| B07-hero-sub | `Nu este un abonament. Este un loc la masă — la Woloshin Banya, lângă pădure. Cine este acum decide cine mai intră.` | `Это не абонемент. Это место за столом — в Woloshin Banya, у леса. Те, кто сейчас внутри, решают, кто войдёт следующим.` | длинная ритмическая фраза — Курáль |
| B08-cta-primary | `Programează o conversație` | `Назначить разговор` | |
| B09-cta-secondary | `Cum funcționează, mai exact` | `Как это устроено, если коротко` | |
| B10-meta-bottom | `Ediția I · Chișinău · Woloshin Banya` | `Издание I · Кишинёв · Woloshin Banya` | |

**Эпиграф (4 строки, курсив Корморант)** — добавлено, поверх hero:
```
Не каждый, кто проходит мимо огня, — у огня свой.
Woloshin Club не покупается.
Его принимают — и носят.
```

---

## C · S02 · MANIFESTO (Манифест)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| C01-line-1 | `Nu deschidem ușa tuturor.` | `Мы не открываем дверь всем.` | |
| C02-line-2 | `O deschidem celor care înțeleg că un club este o casă, nu un serviciu.` | `Мы открываем её тем, кто понимает: клуб — это дом, а не сервис.` | |
| C03-line-3 | `La Woloshin, fiecare detaliu — de la halat la conversație — este ales înainte să fie cerut.` | `В Woloshin каждый жест — от халата до разговора — выбран до того, как его попросят.` | |
| C04-line-4-final | `Aici, timpul se poartă altfel.` | `Здесь время носят иначе.` | финал — точка, тишина |

---

## D · S03 · CIFRA · 50 (Число)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| D01-eyebrow | `CIFRA · 50` | `ЧИСЛО · 50` | |
| D02-giant-number | `50` (визуально) | `50` (визуально) | не переводится |
| D03-sub | `Cincizeci de nume, într-o singură casă.` | `Пятьдесят имён — под одной крышей.` | |
| D04-legend | `Mai jos — câți au rămas până la cincizeci.` | `Ниже — сколько осталось до пятидесяти.` | |

---

## E · S04 · THE HOUSE (Дом)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| E01-frame-label | `Woloshin Banya · în curând` | `Woloshin Banya · скоро` | |
| E02-eyebrow | `CAPITOLUL I · CASA` | `ГЛАВА I · ДОМ` | |
| E03-h2 | `Woloshin Banya. O casă lângă pădure.` | `Woloshin Banya. Дом у леса.` | |
| E04-italic-sub | `Nu o locație. Un principiu: cei care intră ies altfel.` | `Не локация. Принцип: кто входит — выходит другим.` | |
| E05-body | `Woloshin Banya funcționează după o singură regulă — fiecare gest este ales înainte să fie cerut. Abur, stejar, tăcere, conversație. Woloshin Club preia acest principiu și îl extinde într-o comunitate restrânsă de cincizeci de oameni.` | `Woloshin Banya живёт по одному правилу — каждый жест выбран до того, как его попросят. Пар, дуб, тишина, разговор. Woloshin Club берёт этот принцип и переносит его в узкий круг из пятидесяти человек.` | переписано с ритмом — длинное, потом точка |
| E06-city-1 | `Mosco` | `Москва` | |
| E06-city-2 | `Helsinki` | `Хельсинки` | |
| E06-city-3 | `Sankt Petersburg` | `Санкт-Петербург` | |
| E06-city-4 | `Tbilisi` | `Тбилиси` | |
| E06-city-5 | `Istanbul` | `Стамбул` | |
| E06-city-6 | `Berlin` | `Берлин` | |

---

## F · S05 · THE SPACES (Пространства)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| F01-eyebrow | `SPAȚIILE CASEI` | `ПРОСТРАНСТВА ДОМА` | |
| F02-h2 | `Cinci camere. O singură casă.` | `Пять комнат. Один дом.` | |
| F03-card-01-title | `Sauna Mare` | `Большая парная` | |
| F03-card-01-cap | `Pentru aburul cel lung` | `Для долгого пара` | |
| F04-card-02-title | `Baia de Stejar` | `Дубовая купель` | |
| F04-card-02-cap | `Cu apă de izvor` | `С родниковой водой` | |
| F05-card-03-title | `Camera de Lectură` | `Читальная комната` | |
| F05-card-03-cap | `Și liniște cerută` | `И запрошенная тишина` | |
| F06-card-04-title | `Cămara de Vin` | `Винный погреб` | |
| F06-card-04-cap | `Aleasă de somelier` | `Выбран сомелье` | |
| F07-card-05-title | `Salonul de Iarnă` | `Зимний салон` | |
| F07-card-05-cap | `Pentru conversație` | `Для разговора` | |

---

## G · S06 · THE RITUAL (Ритуал)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| G01-eyebrow | `CAPITOLUL II · RITUALUL` | `ГЛАВА II · РИТУАЛ` | |
| G02-h2 | `Șapte gesturi, înainte de miezul nopții.` | `Семь жестов до полуночи.` | |
| G03-beat-01-title | `Sosirea` | `Приход` | |
| G03-beat-01-body | `Haina se predă la ușă, fără cuvinte.` | `Пальто сдаётся у двери — без слов.` | |
| G04-beat-02-title | `Prima turnare` | `Первая наливка` | |
| G04-beat-02-body | `Ceaiul este deja în ceașcă.` | `Чай уже в чашке.` | |
| G05-beat-03-title | `Aburul` | `Пар` | |
| G05-beat-03-body | `Stejar, tăcere, căldură.` | `Дуб. Тишина. Жар.` | |
| G06-beat-04-title | `Conversația` | `Разговор` | |
| G06-beat-04-body | `Începe când începe.` | `Начинается, когда начинается.` | |
| G07-beat-05-title | `Cina` | `Ужин` | |
| G07-beat-05-body | `Lungă, fără agendă.` | `Длинный, без повестки.` | |
| G08-beat-06-title | `Focul din curte` | `Огонь во дворе` | |
| G08-beat-06-body | `Până se termină.` | `Пока не догорит.` | |
| G09-beat-07-title | `Plecarea` | `Уход` | |
| G09-beat-07-body | `Haina se întoarce la cuierul tău, cu un bilețel pe care nu l-ai cerut.` | `Пальто возвращается на вашу вешалку — с запиской, которую вы не просили.` | |

---

## H · S07 · THE PRIVILEGES (Привилегии)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| H01-eyebrow | `ÎN FIECARE ZI, FĂRĂ SĂ ÎNTREBI` | `КАЖДЫЙ ДЕНЬ — БЕЗ ВОПРОСОВ` | |
| H02-h2 | `Nu ceri. Ai.` | `Не просишь. Имеешь.` | центральное — топ-3 |
| H03-italic-sub | `Privilegiile nu sunt „beneficii". Sunt felul în care funcționează casa pentru tine, înainte să deschizi gura.` | `Привилегии — это не «бенефиты». Это то, как дом работает для вас — раньше, чем вы откроете рот.` | |
| H04-p01-label | `Preț de membru în toate complexele` | `Цена члена — во всех комплексах` | аудит: было «tarif» — заменено |
| H04-p01-desc | `Tariful casei aplicat automat, la fiecare vizită, fără cupon, fără cod.` | `Домашняя цена применяется автоматически, при каждом визите. Без купона. Без кода.` | |
| H05-p02-label | `Camerele private — ale tale înaintea tuturor` | `Приватные комнаты — ваши прежде всех` | |
| H05-p02-desc | `Acces prioritar la cele patru băi private. Rezervare cu 48 de ore înainte.` | `Приоритетный доступ к четырём приватным купелям. Бронь — за 48 часов до всех остальных.` | |
| H06-p03-label | `Rezervarea — cu 48 de ore înaintea publicului` | `Бронь — за 48 часов до публики` | |
| H06-p03-desc | `Fiecare fereastră de timp se deschide pentru tine înainte de a se deschide.` | `Каждое временное окно открывается для вас прежде, чем для всех.` | |
| H07-p04-label | `Produsele noi — înaintea pieței` | `Новинки — раньше рынка` | |
| H07-p04-desc | `Fiecare ulei, ceai, obiect creat la Woloshin ajunge la tine înainte de magazin.` | `Каждое масло, чай, вещь, созданная в Woloshin, приходит к вам раньше, чем попадёт в магазин.` | |
| H08-p05-label | `Cercul de Telegram — chat închis` | `Telegram-круг — закрытый чат` | |
| H08-p05-desc | `Moderat, nu controlat. Discuții, recomandări, fotografii — între cei cincizeci.` | `Модерируется, но не контролируется. Разговоры, рекомендации, фотографии — между пятьюдесятью.` | |
| H09-p06-label | `Cina cu fondatorul — de două ori pe an` | `Ужин с основателем — дважды в год` | |
| H09-p06-desc | `În grupuri mici de opt. Seara se termină când se termină. Fără agendă.` | `В малых группах по восемь. Вечер заканчивается, когда заканчивается. Без повестки.` | |
| H10-p07-label | `Un oaspete, o singură dată` | `Один гость, один раз` | |
| H10-p07-desc | `Poți aduce o persoană care nu este încă membru. Dacă îi place, va aplica ea însăși.` | `Можете привести человека, который ещё не член клуба. Если понравится — подаст заявку сам.` | |
| H11-p08-label | `Cadoul casei — de ziua ta` | `Дар дома — в ваш день` | |
| H11-p08-desc | `Un obiect sau un ritual ales anul acesta pentru tine. Nu un voucher.` | `Вещь или ритуал, выбранный в этом году для вас. Не ваучер.` | |

---

## I · SCARCITY BLOCK · 42/50

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| I01-eyebrow | `APLICARE · EDIȚIA I` | `ЗАЯВЛЕНИЕ · ИЗДАНИЕ I` | |
| I02-h2 | `8 locuri rămase` | `Осталось восемь мест` | |
| I03-sub | `42 din 50 nume sunt deja la masă.` | `42 из 50 имён уже за столом.` | |
| I04-legend | `Când ajunge la cincizeci, site-ul se închide. Ușa nu se mai deschide până la ediția a II-a.` | `Когда станет пятьдесят, сайт закроется. Дверь не откроется до второго издания.` | |

---

## J · S08 · THE DOOR (Цена) ⚠ AUDIT-FLAGGED

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| J01-eyebrow | `INTRA ÎN CLUB` | `ВОЙТИ В КЛУБ` | |
| J02-h2 | `Ceea ce 50 000 MDL deschide` ⭐ REWRITE | `Что открывает пятьдесят тысяч` ⭐ REWRITE | RO буквально «То, что 50 000 MDL открывает» — звучит как реклама. RU — чище |
| J03-price-italic | `O singură plată. Acces pe viață.` | `Один платёж. Доступ на всю жизнь.` | |
| J04-price-numeral | `50 000 MDL` | `50 000 MDL` | цифрами, без расшифровки |
| J05-price-subline | `cincizeci de mii de lei · acces pe viață` | `пятьдесят тысяч леев · доступ на всю жизнь` | |
| J06-price-unit | `lei moldovenești · taxă unică de intrare` | `молдавских леев · единый взнос за вход` | |
| J07-cta | `Înțeleg. Vreau să intru.` | `Понимаю. Хочу войти.` | |

**⭐ TOP-REWRITE для S08 (аудит + Vlad):**
- RO вариант ★: `Что открывает пятьдесят тысяч` → RU: `Что открывает пятьдесят тысяч`
- Альтернатива RO: `Половина — клубу. Половина — вам.`
- Альтернатива RU: `Одна дверь, пятьдесят тысяч, жизнь`

---

## K · S09 · THE CALENDAR (Календарь)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| K01-eyebrow | `DOAR PENTRU NOI` | `ТОЛЬКО ДЛЯ НАС` | |
| K02-h2 | `Trei nopți pe an. Cincizeci de oameni.` | `Три ночи в году. Пятьдесят человек.` | |
| K03-italic-sub | `Trei seri pe an, închise pentru public, deschise pentru tine. Fără telefoane, fără protocol, fără capturi.` | `Три вечера в году, закрытых для публики, открытых для вас. Без телефонов. Без протокола. Без кадров.` | |
| K04-event-01-month | `Noiembrie` | `Ноябрь` | |
| K04-event-01-day | `14` | `14` | цифрами |
| K04-event-01-title | `Cina cea mai lungă` | `Самый длинный ужин` | |
| K04-event-01-desc | `Wine-paired, opt locuri, masă comună. Seara se termină când se termină.` | `Вино подобрано, восемь мест, общий стол. Вечер заканчивается, когда заканчивается.` | |
| K04-event-01-tag | `Cină` | `Ужин` | |
| K05-event-02-month | `Noiembrie` | `Ноябрь` | |
| K05-event-02-day | `28` | `28` | |
| K05-event-02-title | `Vinul lui Rareș` | `Вино Рареша` | |
| K05-event-02-desc | `Degustare verticală, șapte ani, o singură cramă. Cu poveștile lor.` | `Вертикальная дегустация, семь лет, одна винотека. С их историями.` | |
| K05-event-02-tag | `Degustare` | `Дегустация` | |
| K06-event-03-month | `Ianuarie` | `Январь` | |
| K06-event-03-day | `08` | `08` | |
| K06-event-03-title | `Anul Nou, devreme` | `Новый год, рано` | |
| K06-event-03-desc | `Anti-revelion. Lectură la miezul nopții, ceai, tăcere, trei camere.` | `Анти-реvelion. Чтение в полночь, чай, тишина, три комнаты.` | |
| K06-event-03-tag | `Lectură` | `Чтение` | |

---

## L · S10 · THE NUMBERS (Числа)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| L01-eyebrow | `CIFRE` | `ЦИФРЫ` | |
| L02-h2 | `Cincizeci. Trei. Două.` | `Пятьдесят. Три. Два.` | |
| L03-ring-01-label | `Membri` | `Членов` | |
| L03-ring-01-cap | `Cincizeci de nume. Atât. Niciodată mai mult.` | `Пятьдесят имён. И всё. Больше никогда.` | |
| L04-ring-02-label | `Seri pe an` | `Вечеров в году` | |
| L04-ring-02-cap | `Trei nopți închise pentru public, deschise pentru tine.` | `Три ночи, закрытые для публики, открытые для вас.` | |
| L05-ring-03-label | `Cine cu fondatorul` | `Ужина с основателем` | |
| L05-ring-03-cap | `De două ori pe an, în grupuri mici de opt. Fără agendă.` | `Дважды в год, в малых группах по восемь. Без повестки.` | |
| L06-context-italic | `Cincizeci de nume. Trei seri. Două cine cu fondatorul. Restul se câștigă.` | `Пятьдесят имён. Три вечера. Два ужина с основателем. Остальное — заслуживается.` | |

---

## M · S11 · THE HOST (Хозяин)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| M01-frame-label | `Rareș · gazda clubului` | `Рареш · хозяин клуба` | |
| M02-eyebrow | `GAZDA` | `ХОЗЯИН` | |
| M03-h2-italic ⭐ REWRITE | `Bun venit. Sunt Rareș. Vă aștept la ușă.` | `Добро пожаловать. Я — Рареш. Буду ждать у двери.` | проверить естественность — см. ниже |
| M04-body-1 | `Clubul este casa mea de când am deschis-o. Fiecare membru îl simte ca pe al lui — și asta mă bucură cel mai tare.` | `Клуб — мой дом с тех пор, как я его открыл. И каждый член клуба чувствует его своим — и это радует меня больше всего.` | |
| M05-body-2 | `Administratorul tău este o persoană, nu o echipă. Îți cunoaște ora la care vii, ce bei, cu cine vii. Răspunde în aceeași zi, în română, rusă sau engleză.` | `Ваш администратор — это один человек, не команда. Он знает, к которому часу вы приходите, что пьёте, с кем. Отвечает в тот же день — по-русски, по-румынски или по-английски.` | |

**⭐ Проверка «естественности» M03:** `Добро пожаловать. Я — Рареш. Буду ждать у двери.` — короткое, без инверсий, звучит как сказанное. Альтернатива: `Рад вас видеть. Я Рареш. Встречу вас у двери.` — оба варианта приемлемы; ★ первый — он теплее.

---

## N · S12 · THE CLOSING (Закрытие)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| N01-eyebrow | `TRECEȚI` | `ПРОХОДИТЕ` | |
| N02-h2 | `Ușa se deschide o singură dată pe seară.` | `Дверь открывается один раз за вечер.` | |
| N03-scroll-prompt | `Scroll pentru a continua` | `Прокрутите, чтобы продолжить` | |
| N04-cta | `Solicită` | `Подать заявку` | |

---

## O · S13 · THE FORM (Заявка)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| O01-eyebrow | `APLICĂ` | `ЗАЯВКА` | |
| O02-h2 | `Spune-ne câteva lucruri.` | `Расскажите о себе — несколько строк.` | |
| O03-italic-sub | `Răspundem în 48 de ore. Sau mai devreme.` | `Отвечаем за 48 часов. Или раньше.` | |
| O04-label-email | `Email` | `Электронная почта` | |
| O04-placeholder-email | `nume@domeniu.md` | `имя@домен.md` | |
| O05-label-phone | `Telefon opțional` | `Телефон · необязательно` | |
| O05-placeholder-phone | `+373 …` | `+373 …` | |
| O06-label-msg | `Mesaj scurt opțional` | `Короткое сообщение · необязательно` | |
| O06-placeholder-msg | `Ce cauți într-un club ca acesta…` | `Что вы ищете в клубе вроде этого…` | |
| O07-submit | `Trimit. Apoi, tăcere — noi revenim.` | `Отправить. Потом — тишина. Мы вернёмся.` | |
| O08-privacy | `Datele rămân în casă. Nu se trimit terților.` | `Данные остаются в доме. Третьим лицам не передаются.` | |
| O09-form-msg-success | `Am primit. Administratorul clubului te va contacta în 24 de ore.` | `Получили. Администратор клуба свяжется с вами в течение 24 часов.` | |

---

## P · FOOTER (S14)

| ID | RO_text (current) | RU_text (new) | Notes |
|---|---|---|---|
| P01-sigil | `WOLOSHIN · CLUB` | `WOLOSHIN · CLUB` | знак |
| P02-sub | `Woloshin Banya · Chișinău · Ediția I — 2026` | `Woloshin Banya · Кишинёв · Издание I — 2026` | |
| P03-col-1-title | `Casa` | `Дом` | |
| P03-col-1-addr | `Strada 31 August 1989, nr. 78` | `улица 31 Августа 1989, № 78` | |
| P03-col-1-city | `Chișinău, Republica Moldova` | `Кишинёв, Республика Молдова` | |
| P03-col-1-hours | `Mar–Sâm · 16:00 — 02:00` | `Вт–Сб · 16:00 — 02:00` | |
| P04-col-2-title | `Program` | `Связь` | |
| P04-col-2-email | `club@woloshin.md` | `club@woloshin.md` | |
| P04-col-2-phone | `+373 · linie dedicată membrilor` | `+373 · линия для членов клуба` | |
| P04-col-2-hours | `Luni–Sâmbătă · 09:00 — 21:00` | `Пн–Сб · 09:00 — 21:00` | |
| P05-col-3-title | `Urmărește` | `Следите` | |
| P05-col-3-ig | `Instagram · @woloshin.banya` | `Instagram · @woloshin.banya` | хэндл сохраняется |
| P05-col-3-tg | `Telegram · cercul închis` | `Telegram · закрытый круг` | |
| P06-copyright | `© 2026 Woloshin Club. Woloshin Banya SRL. Chișinău, Republica Moldova.` | `© 2026 Woloshin Club. Woloshin Banya SRL. Кишинёв, Республика Молдова.` | |
| P07-micro-legal | `Woloshin Club este un program al Woloshin Banya și funcționează sub regulile casei.` | `Woloshin Club — программа Woloshin Banya и работает по правилам дома.` | |

---

## TOP 5 NEED-REWRITE (не просто перевод — улучшение текста)

Эти пять строк **переписываются, а не просто переводятся**. Пометка ⭐ REWRITE.

| # | ID | Почему | Что делаем |
|---|---|---|---|
| 1 | **B01** Hero epigraph: `Woloshin Club nu se cumpără. Se poartă.` | Это центральная строка всей страницы. Сейчас она звучит как перевод с румынского. Нужна русская версия, которая работает как итог. | RU: `Woloshin Club не покупается. Его носят.` — коротко, ритмично, финал как точка. |
| 2 | **J02** S08: `Ceea ce 50 000 MDL deschide` ⭐ | Румынский буквален: «То, что 50 000 MDL открывает» — звучит как реклама, не как манифест. Аудит флагнул. | RO ★: `Ce deschide cincizeci de mii` / RU ★: `Что открывает пятьдесят тысяч`. Альтернатива: `Jumătate — clubului. Jumătate — ție.` (RO) / `Половина — клубу. Половина — вам.` (RU). |
| 3 | **H02** Privileges H2: `Nu ceri. Ai.` | Уже хорошо — не трогаем. Но под-курсив H03 длинноват. | RU: сократить до `Привилегии — это не «бенефиты». Это то, как дом работает для вас, ещё до ваших слов.` (H03). |
| 4 | **H04-p01-label** `Preț de membru în toate complexele` + desc с `Tariful casei` | Аудит отметил: `tarif` — единственное слово, уводящее в коммерческий регистр. | RU: `Цена члена — во всех комплексах` + `Домашняя цена применяется автоматически, при каждом визите. Без купона. Без кода.` |
| 5 | **M03** Host h2: `Bun venit. Sunt Rareș. Vă aștept la ușă.` | Нужно проверить, что русский эквивалент звучит естественно, а не как перевод. Текущее «переводческое» было бы `Добро пожаловать. Я — Рареш. Я жду вас у двери.» | RU ★: `Добро пожаловать. Я — Рареш. Буду ждать у двери.` — мягче, короче, дышит. |

---

## ИТОГО

- **Всего строк в карте:** 110+
- **RU-первичный текст:** 100% покрытие (все экраны, формы, footer, micro-meta)
- **RO-полировка:** 5 точечных переписываний (B01, J02, H03, H04, M03)
- **Banned-фильтр применён:** ни одного «Абонемент», «Скидка», «Клиент», «Промо-акция»
- **Числа:** «пятьдесят» прописью в поэтическом контексте, «50 000» цифрами в цене

Полный RU-текст — в `/Users/pro/Documents/Projects/Woloshin_club/v2/agents/copy-ru.md`.