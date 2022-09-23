---
title: Number
slug: Web/JavaScript/Reference/Global_Objects/Number
tags:
  - Class
  - JavaScript
  - Number
  - Reference
  - Polyfill
browser-compat: javascript.builtins.Number
---

{{JSRef}}

**`Number`** (число) – [об'єкт-обгортка примітива](/uk/docs/Glossary/Primitive#obiekty-obhortky-prymityviv-u-javascript), що застосовується для представлення й роботи з числами, як то `37` чи `-9.25`.

Конструктор `Number` містить константи й методи для роботи з числами. Значення інших типів можуть бути перетворені на числа за допомогою функції `Number()`.

## Опис

Числа найчастіше виражають у літеральних формах, як то `0b101`, `0o13`, `0x0A`. [Лексична граматика](/uk/docs/Web/JavaScript/Reference/Lexical_grammar#chyslovi-literaly) містить докладнішу довідку.

```js
123; // сто двадцять три
123.0; // те саме
123 === 123.0; // true
```

Числовий літерал, як то `37`, в коді JavaScript є значенням з рухомою комою, а не цілим. Немає загальновживаного окремого типу цілих чисел. (JavaScript тепер має тип {{jsxref("BigInt")}}, але він був розроблений не для заміни Number в повсякденному використанні. `37` – це все ж `Number`, а не BigInt.)

Бувши застосованим як функція, `Number(value)` перетворює рядок чи інше значення на Number. Якщо значення не може бути перетворено, буде повернено {{jsxref("NaN")}}.

```js
Number("123"); // повертає число 123
Number("123") === 123; // true

Number("єдиноріг"); // NaN
Number(undefined); // NaN
```

### Кодування Number

Тип JavaScript `Number` є значенням [64-бітного двійкового формату подвійної точності (IEEE 754)](https://uk.wikipedia.org/wiki/%D0%A7%D0%B8%D1%81%D0%BB%D0%BE_%D0%B7_%D1%80%D1%83%D1%85%D0%BE%D0%BC%D0%BE%D1%8E_%D0%BA%D0%BE%D0%BC%D0%BE%D1%8E), подібно до `double` в Java чи C#. Це означає, що він може представляти дробові значення, але є певні обмеження щодо величини та точності значень, котрі він може зберігати. Дуже стисло кажучи, число подвійної точності IEEE 754 використовує 64 біти для представлення 3 частин:

- 1 біт для _знаку_ (додане число чи від'ємне)
- 11 біт для _експоненти_ (від -1022 до 1023)
- 52 біти для _мантиси_ (представляє число між 0 і 1)

Мантиса – частина числа, що представляє фактичне значення (вагомі цифри). Експонента – степінь двійки, на котрий повинна бути помножена мантиса. У вигляді наукового запису:

<math display="block"><semantics><mrow><mtext>Number</mtext><mo>=</mo><mo stretchy="false">(</mo><mrow><mo>−</mo><mn>1</mn></mrow><msup><mo stretchy="false">)</mo><mtext>знак</mtext></msup><mo>⋅</mo><mo stretchy="false">(</mo><mn>1</mn><mo>+</mo><mtext>мантиса</mtext><mo stretchy="false">)</mo><mo>⋅</mo><msup><mn>2</mn><mtext>експонента</mtext></msup></mrow><annotation encoding="TeX">\text{Number} = ({-1})^{\text{знак}} \cdot (1 + \text{мантиса}) \cdot 2^{\text{експонента}}</annotation></semantics></math>

Мантиса зберігається в 52 бітах, що тлумачаться як цифри після `1.…` у двійковому дробовому числі. Таким чином, точність мантиси – 2<sup>-52</sup> (отримується за допомогою {{jsxref("Number.EPSILON")}}), або приблизно від 15 до 17 знаків після коми; арифметика понад цим рівнем точності підпадає під [округлення (англ.)](https://en.wikipedia.org/wiki/Floating-point_arithmetic#Representable_numbers,_conversion_and_rounding).

Найбільше значення, котре може утримувати число – 2<sup>1024</sup> - 1 (чия експонента 1023, а мантиса – 0.1111… за основою числення 2), його можна отримати як {{jsxref("Number.MAX_VALUE")}}. Більші значення замінюються особливою числовою сталою – {{jsxref("Infinity")}}.

Цілі числа можуть бути представлені без втрати точності лише в діапазоні від -2<sup>53</sup> + 1 до 2<sup>53</sup> - 1 включно (межі доступні як {{jsxref("Number.MIN_SAFE_INTEGER")}} і {{jsxref("Number.MAX_SAFE_INTEGER")}}), тому що мантиса може утримувати лише 53 біти (включно з 1 на початку).

Більше подробиць про це описані в [стандарті ECMAScript (англ.)](https://tc39.es/ecma262/#sec-ecmascript-language-types-number-type).

## Конструктор

- [`Number()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Number/Number)
  - : Створює нове значення `Number`.

Коли `Number` викликається як конструктор (із `new`), це породжує об'єкт {{jsxref("Number")}}, котрий **не** є примітивом. Наприклад, `typeof new Number(42) === "object"`, і `new Number(42) !== 42` (проте `new Number(42) == 42`).

> **Застереження:** Навряд вам доведеться часто застосовувати `Number` як конструктор.

## Статичні властивості

- {{jsxref("Number.EPSILON")}}
  - : Найменший інтервал між числами, котрі можна представити.
- {{jsxref("Number.MAX_SAFE_INTEGER")}}
  - : Найбільше безпечне в JavaScript ціле число (2<sup>53</sup> - 1).
- {{jsxref("Number.MAX_VALUE")}}
  - : Найбільше додатне число, котре можна представити.
- {{jsxref("Number.MIN_SAFE_INTEGER")}}
  - : Найменше безпечне в JavaScript ціле число (-(2<sup>53</sup> - 1)).
- {{jsxref("Number.MIN_VALUE")}}
  - : Найменше додатне число, котре можна представити, а отже – найближче до нуля додатне число (котре все ж не є нулем).
- {{jsxref("Number.NaN")}}
  - : Особливе значення "**N**ot **a** **N**umber" ("не число").
- {{jsxref("Number.NEGATIVE_INFINITY")}}
  - : Особливе значення, що представляє від'ємну нескінченність. Повертається при переповненні.
- {{jsxref("Number.POSITIVE_INFINITY")}}
  - : Особливе значення, що представляє нескінченність. Повертається при переповненні.
- {{jsxref("Number", "Number.prototype")}}
  - : Дає змогу додавати до об'єкта `Number` нові властивості.

## Статичні методи

- {{jsxref("Number.isNaN()")}}
  - : З'ясовує, чи є передане значення `NaN`.
- {{jsxref("Number.isFinite()")}}
  - : З'ясовує, чи є передане значення скінченним числом.
- {{jsxref("Number.isInteger()")}}
  - : З'ясовує, чи є передане значення цілим числом.
- {{jsxref("Number.isSafeInteger()")}}
  - : З'ясовує, чи є передане значення безпечним цілим (числом в діапазоні від -(2<sup>53</sup> - 1) до 2<sup>53</sup> - 1).
- {{jsxref("Number.parseFloat()")}}
  - : Те саме, що й глобальна функція {{jsxref("parseFloat", "parseFloat()")}}.
- {{jsxref("Number.parseInt()")}}
  - : Те саме, що й глобальна функція {{jsxref("parseInt", "parseInt()")}}.

## Методи примірника

- {{jsxref("Number.prototype.toExponential()")}}
  - : Повертає рядок, що представляє число в експоненціальному записі.
- {{jsxref("Number.prototype.toFixed()")}}
  - : Повертає рядок, що представляє число в записі з фіксованою комою.
- {{jsxref("Number.prototype.toLocaleString()")}}
  - : Повертає рядок представлення числа, що є чутливим до мови. Заміщає метод {{jsxref("Object.prototype.toLocaleString()")}}.
- {{jsxref("Number.prototype.toPrecision()")}}
  - : Повертає рядок, що представляє число до певної точності, в записі з фіксованою комою чи експоненціальному.
- {{jsxref("Number.prototype.toString()")}}
  - : Повертає рядок, що представляє вказаний об'єкт в указаній _основі числення_. Заміщає метод {{jsxref("Object.prototype.toString()")}}.
- {{jsxref("Number.prototype.valueOf()")}}
  - : Повертає примітивне значення вказаного об'єкта. Заміщає метод {{jsxref("Object.prototype.valueOf()")}}.

## Приклади

### Застосування об'єкта Number для присвоєння числовим змінним значень

Наступний приклад використовує властивості об'єкта `Number` для присвоєння значень декільком числовим змінним:

```js
const biggestNum = Number.MAX_VALUE;
const smallestNum = Number.MIN_VALUE;
const infiniteNum = Number.POSITIVE_INFINITY;
const negInfiniteNum = Number.NEGATIVE_INFINITY;
const notANum = Number.NaN;
```

### Діапазон цілих чисел для Number

Наступний приклад демонструє мінімальне й максимальне значення цілих чисел, що можуть бути представлені об'єктом `Number`.

```js
const biggestInt = Number.MAX_SAFE_INTEGER; //  (2**53 - 1) =>  9007199254740991
const smallestInt = Number.MIN_SAFE_INTEGER; // -(2**53 - 1) => -9007199254740991
```

При розборі даних, що були серіалізовані в JSON, від цілочислових значень, що випадають із цього діапазону, можна очікувати псування, коли розбирач JSON приводитиме їх до типу `Number`.

Це можливо обійти шляхом застосування {{jsxref("String")}}.

Більші числа можуть бути представлені за допомогою типу {{jsxref("BigInt")}}.

### Використання Number() для перетворення об'єкта Date

Наступний приклад перетворює об'єкт {{jsxref("Date")}} на числове значення, застосовуючи `Number` як функцію:

```js
const d = new Date("December 17, 1995 03:24:00");
console.log(Number(d));
```

Це виводить `819199440000`.

### Перетворення числових рядків і null на числа

```js
Number("123"); // 123
Number("123") === 123; // true
Number("12.3"); // 12.3
Number("12.00"); // 12
Number("123e-1"); // 12.3
Number(""); // 0
Number(null); // 0
Number("0x11"); // 17
Number("0b11"); // 3
Number("0o11"); // 9
Number("foo"); // NaN
Number("100a"); // NaN
Number("-Infinity"); // -Infinity
```

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

## Дивіться також

- [Поліфіл сучасної логіки `Number` (з підтримкою двійкових та вісімкових літералів) у складі `core-js`](https://github.com/zloirock/core-js#ecmascript-number)
- {{jsxref("NaN")}}
- [Арифметичні оператори](/uk/docs/Web/JavaScript/Reference/Operators#aryfmetychni-operatory)
- Глобальний об'єкт {{jsxref("Math")}}
- Цілі числа з довільною точністю: {{jsxref("BigInt")}}