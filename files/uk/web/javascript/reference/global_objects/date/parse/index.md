---
title: Date.parse()
slug: Web/JavaScript/Reference/Global_Objects/Date/parse
tags:
  - Date
  - JavaScript
  - Method
  - Reference
browser-compat: javascript.builtins.Date.parse
---

{{JSRef}}

Метод **`Date.parse()`** (розібрати) розбирає рядкове представлення дати й повертає число мілісекунд, що минуло від 00:00:00 1 січня 1970 року за Всесвітнім координованим часом, або `NaN`, якщо рядок не вдалося зрозуміти або, в деяких випадках, якщо рядок містить неприпустиме значення дати (наприклад, 2015-02-31).

Лише [формат ISO 8601 (англ.)](https://tc39.es/ecma262/#sec-date-time-string-format) (`YYYY-MM-DDTHH:mm:ss.sssZ`) явно вказаний як такий, що підтримується. Інші формати залежать від реалізації й можуть не працювати на всіх браузерах. Якщо треба узгоджувати кілька різних форматів, може допомогти бібліотека.

{{EmbedInteractiveExample("pages/js/date-parse.html")}}

## Синтаксис

```js-nolint
Date.parse(dateString)
```

### Параметри

- `dateString`
  - : Рядкове представлення [спрощення розширеного формату календарної дати ISO 8601](#format-riadka-daty-i-chasu).
    (Можуть використовуватися інші формати, але результати такого використання залежать від реалізації.)

### Повернене значення

Число, що представляє мілісекунди, котрі минули від 00:00:00 1 січня 1970 року за Всесвітнім координованим часом, та дату, отриману шляхом розбору переданого представлення дати. Якщо аргумент не представляє дійсну дату, повертається {{jsxref("NaN")}}.

## Опис

Метод `parse()` приймає рядок дати (як то `"2011-10-10T14:48:00"`) і повертає число мілісекунд від 00:00:00 1 січня 1970 року за В.К.Ч..

Ця функція корисна для встановлення значень дати на основі рядкових значень, наприклад, у поєднанні з методом {{jsxref("Date.prototype.setTime()", "setTime()")}} об'єкта {{jsxref("Global_Objects/Date", "Date")}}.

### Формат рядка дати й часу

Стандартне рядкове представлення рядка дати й часу є спрощенням розширеного формату календарної дати ISO 8601. Для отримання подробиць дивіться розділ специфікації ECMAScript [Формат рядка дати й часу](https://tc39.es/ecma262/#sec-date-time-string-format).

Наприклад, `"2011-10-10"` (форма _суто дати_), `"2011-10-10T14:48:00"` (форма _дати й часу_) і `"2011-10-10T14:48:00.000+09:00"` (форма _дати й часу_ з мілісекундами й часовим поясом) можуть бути передані й будуть розібрані. Коли зміщення часового поясу відсутнє, форми суто дати тлумачаться як час за Всесвітнім координованим часом, а форми дати й часу – як місцевий час.

Хоч специфікатори часового поясу використовуються для тлумачення аргументу при розборі рядка дати, повернене значення завжди є кількістю мілісекунд між 00:00:00 1 січня 1970 року за Всесвітнім координованим часом і миттю часу, що представлена аргументом, або – `NaN`.

У зв'язку з тим, що `parse()` є статичним методом {{jsxref("Date")}}, він викликається як `Date.parse()`, а не як метод примірника {{jsxref("Date")}}.

### Залежні від реалізації формати дат як запасний варіант

> **Примітка:** Цей розділ містить залежну від реалізації логіку, котра може бути неоднаковою на різних реалізаціях.

Специфікація ECMAScript зазначає: Якщо String не відповідає стандартному форматові, функція може звернутися до будь-яких евристики чи алгоритму, специфічних для конкретної реалізації. Незрозумілі рядки чи дати, що містять неприпустимі значення елементів у рядках формату ISO, змушують `Date.parse()` повертати {{jsxref("NaN")}}.

Проте недійсні значення в рядках дати, не впізнані як спрощений формат ISO, згідно з ECMA-262 можуть повертати чи не повертати {{jsxref("NaN")}}, залежно від браузера й конкретного переданого значення, наприклад:

```js
// Не-ISO рядок з недійсними значеннями дати
new Date("23/25/2014");
```

оброблятиметься як місцева дата, 25 листопада 2015 року, у Firefox 30 і як недійсна дата в Safari 7.

Проте якщо рядок впізнаний як рядок формату ISO й містить недійсні значення, буде повернено {{jsxref("NaN")}}:

```js
// Рядок ISO з недійсними значеннями
new Date("2014-25-23").toISOString();
// викидає "RangeError: invalid date"
```

Власна евристика SpiderMonkey може бути знайдена в [`jsdate.cpp`](https://searchfox.org/mozilla-central/source/js/src/jsdate.cpp?rev=64553c483cd1#889). Рядок `"10 06 2014"` є прикладом невідповідного формату ISO, а тому змушує звертатися до власної процедури. Також читайте оцей [грубий нарис (англ.)](https://bugzilla.mozilla.org/show_bug.cgi?id=1023155#c6) про те, як працює розбір.

```js
new Date("10 06 2014");
```

оброблятиметься як місцева дата, 6 жовтня 2014 року, а не 10 червня 2014.

Інші приклади

```js
new Date("foo-bar 2014").toString();
// повертає: "Invalid Date"

Date.parse("foo-bar 2014");
// повертає: NaN
```

### Відмінності здогадів щодо часового поясу

> **Примітка:** Цей розділ містить залежну від реалізації логіку, котра може бути неоднаковою на різних реалізаціях.

Отримавши нестандартний рядок дати `"March 7, 2014"`, `parse()` припускає, що мова про місцевий часовий пояс, але отримавши спрощення розширеного формату календарної дати ISO 8601, як то `"2014-03-07"`, він вирішить, що мова про часовий пояс Всесвітнього координованого часу. Таким чином, об'єкти {{jsxref("Date")}}, створені за допомогою таких рядків, можуть представляти різні миті часу залежно від підтримуваної версії ECMAScript, якщо система не має Всесвітній координований час за місцевий часовий пояс. Це означає, що два рядки дати, котрі здаються еквівалентними, можуть призводити до двох різних значень залежно від формату рядка, котрий перетворюється.

## Приклади

### Використання Date.parse()

Усі наступні виклики повернуть `1546300800000`. Перший призведе до припущення про часовий пояс Всесвітнього координованого часу, а решта вказують цей пояс за допомогою формату дати ISO (`Z` і `+00:00`).

```js
Date.parse("2019-01-01");
Date.parse("2019-01-01T00:00:00.000Z");
Date.parse("2019-01-01T00:00:00.000+00:00");
```

Наступний виклик, котрий не вказує часовий пояс, призведе до 2019-01-01 00:00:00 в місцевому часовому поясі системи.

```js
Date.parse("2019-01-01T00:00:00");
```

### Нестандартні рядки дат

> **Примітка:** Цей розділ містить залежну від реалізації логіку, котра може бути неоднаковою на різних реалізаціях.

Якщо `ipoDate` є реальним об'єктом {{jsxref("Date)}}, то він може бути переведений на 9 серпня 1995 року (за місцевим часом) отак:

```js
ipoDate.setTime(Date.parse("Aug 9, 1995"));
```

Іще трохи прикладів розбору нестандартних рядків дати:

```js
Date.parse("Aug 9, 1995");
```

Повертає `807937200000` в часовому поясі GMT-0300 й інші значення в інших часових поясах, оскільки рядок не вказує часового поясу і не має формату ISO, а отже – часовий пояс приймається за місцевий.

```js
Date.parse("Wed, 09 Aug 1995 00:00:00 GMT");
```

Повертає `807926400000` незалежно від місцевого часового поясу, адже вказаний Гринвіцький пояс (Всесвітній координований час).

```js
Date.parse("Wed, 09 Aug 1995 00:00:00");
```

Повертає `807937200000` у часовому поясі GMT-0300 й інші значення в інших часових поясах, адже в аргументі не вказаний часовий пояс, і аргумент не має формату ISO, тому часовий пояс приймається за місцевий.

```js
Date.parse("Thu, 01 Jan 1970 00:00:00 GMT");
```

Повертає `0` незалежно від місцевого часового поясу, адже вказаний Гринвіцький пояс (Всесвітній координований час).

```js
Date.parse("Thu, 01 Jan 1970 00:00:00");
```

Повертає `14400000` у часовому поясі GMT-0400 й інші значення в інших часових поясах, адже часовий пояс не вказаний і рядок не має формату ISO, а отже – використовується місцевий часовий пояс.

```js
Date.parse("Thu, 01 Jan 1970 00:00:00 GMT-0400");
```

Повертає `14400000` незалежно від місцевого часового поясу, адже вказаний Гринвіцький пояс (Всесвітній координований час).

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

### Примітки щодо сумісності

- Firefox 49 змінив розбір двоцифрових років, аби узгодитися з браузером Google Chrome, а не Internet Explorer. Тепер двоцифрові роки, менші за `50`, розбираються як роки XXI сторіччя. Наприклад, `04/16/17`, що раніше розбиралося як 16 квітня 1917 року, тепер 16 квітня 2017 року. Для уникання будь-яких проблем взаємодії чи двозначних років рекомендовано використовувати формат ISO 8601, як то `"2017-04-16"` ([вада 1265136](https://bugzilla.mozilla.org/show_bug.cgi?id=1265136)).
- Google Chrome прийме числовий рядок як дійсний параметр `dateString`. Це означає, що, наприклад, хоч `!!Date.parse("42")` обчислюється в `false` у Firefox, цей вираз обчислюється в `true` у Google Chrome, тому що `"42"` тлумачиться як перше січня 2042 року.

## Дивіться також

- {{jsxref("Date.UTC()")}}