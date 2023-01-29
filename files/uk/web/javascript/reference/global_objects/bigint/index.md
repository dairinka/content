---
title: BigInt
slug: Web/JavaScript/Reference/Global_Objects/BigInt
tags:
  - BigInt
  - Class
  - JavaScript
  - Reference
browser-compat: javascript.builtins.BigInt
---

{{JSRef}}

Значення **`BigInt`** (велике ціле) представляють числові значення, котрі [завеликі](/uk/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER) для представлення {{Glossary("Primitive", "примітивом")}} `number`.

## Опис

**Значення BigInt**, також іноді зване просто **BigInt**, є {{Glossary("Primitive", "примітивом")}} `bigint`, створеним шляхом додавання в кінець літерала цілого числа `n`, або ж викликом функції {{jsxref("Global_Objects/BigInt/BigInt", "BigInt()")}} (без оператора `new`) із передачею їй цілого числа або рядка.

```js
const previouslyMaxSafeInteger = 9007199254740991n;

const alsoHuge = BigInt(9007199254740991);
// 9007199254740991n

const hugeString = BigInt("9007199254740991");
// 9007199254740991n

const hugeHex = BigInt("0x1fffffffffffff");
// 9007199254740991n

const hugeOctal = BigInt("0o377777777777777777");
// 9007199254740991n

const hugeBin = BigInt(
  "0b11111111111111111111111111111111111111111111111111111"
);
// 9007199254740991n
```

Значення BigInt у певних аспектах подібні до значень Number, але також відрізняються в кількох ключових нюансах: значення BigInt не можуть використовуватися з методами вбудованого об'єкта [`Math`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Math) і не можуть змішуватися в операціях зі значенням Number; усі значення повинні бути зведені до одного типу. Проте слід обережно зводити значення туди-назад, адже точність значення BigInt може бути втрачена при зведенні до значення Number.

### Інформація про тип

При перевірці `typeof` значення BigInt (примітив `bigint`) дасть `"bigint"`:

```js
typeof 1n === "bigint"; // true
typeof BigInt("1") === "bigint"; // true
```

Значення BigInt також може бути загорнуто в `Object`:

```js
typeof Object(1n) === "object"; // true
```

### Оператори

Наступні оператори можуть використовуватися зі значеннями BigInt (як примітивними, так і загорнутими в об'єкти):

```
+ * - % **
```

[Побітові оператори](/uk/docs/Web/JavaScript/Reference/Operators) також підтримуються, окрім `>>>` (зсуву вправо з заповненням нулями), адже всі значення BigInt мають знак.

Також підтримується унарний оператор (`+`), [щоб не ламати asm.js](https://github.com/tc39/proposal-bigint/blob/master/ADVANCED.md#dont-break-asmjs).

```js
const previousMaxSafe = BigInt(Number.MAX_SAFE_INTEGER);
// 9007199254740991n

const maxPlusOne = previousMaxSafe + 1n;
// 9007199254740992n

const theFuture = previousMaxSafe + 2n;
// 9007199254740993n, це тепер працює!

const multi = previousMaxSafe * 2n;
// 18014398509481982n

const subtr = multi - 10n;
// 18014398509481972n

const mod = multi % 10n;
// 2n

const bigN = 2n ** 54n;
// 18014398509481984n

bigN * -1n;
// -18014398509481984n
```

Оператор `/` також працює з цілими числами як очікується – проте результати операцій з дробовими результатами обрізаються при використанні зі значеннями BigInt: не буде жодної дробової частини.

```js
const expected = 4n / 2n;
// 2n

const truncated = 5n / 2n;
// 2n, а не 2.5n
```

### Порівняння

Значення BigInt строго не дорівнює значенню Number, проте _дорівнює_ нестрого:

```js
0n === 0;
// false

0n == 0;
// true
```

Значення Number і значення BigInt можуть порівнюватися як звично:

```js
1n < 2;
// true

2n > 1;
// true

2 > 2;
// false

2n > 2;
// false

2n >= 2;
// true
```

Значення BigInt та Number можуть зустрічатися в одному масиві й сортуватися:

```js
const mixed = [4n, 6, -12n, 10, 4, 0, 0n];
// [4n, 6, -12n, 10, 4, 0, 0n]

mixed.sort(); // усталена логіка сортування
// [ -12n, 0, 0n, 10, 4n, 4, 6 ]

mixed.sort((a, b) => a - b);
// не спрацює, адже віднімання не працює з різними типами
// TypeError: can't convert BigInt value to Number value

// сортування з адекватним числовим порівнювачем
mixed.sort((a, b) => (a < b ? -1 : a > b ? 1 : 0));
// [ -12n, 0, 0n, 4n, 4, 6, 10 ]
```

Зверніть увагу, що порівняння загорнутих в `Object` значень BigInt працює як для інших об'єктів – показує рівність лише тоді, коли порівнюється з собою один і той же примірник:

```js
Object(0n) === 0n; // false
Object(0n) === Object(0n); // false

const o = Object(0n);
o === o; // true
```

### Перевірки умов

Значення BigInt відповідають тим самим правилам перетворення, що й Number, коли:

- перетворюються на [`Boolean`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Boolean) – за допомогою функції [`Boolean`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Boolean);
- використовуються з [логічними операторами](/uk/docs/Web/JavaScript/Reference/Operators) `||`, `&&` і `!`; або
- зустрічаються в перевірках умов, як то інструкціях [`if`](/uk/docs/Web/JavaScript/Reference/Statements/if...else).

А саме – лише `0n` є [хибністю](/uk/docs/Glossary/Falsy); все решта – [істинність](/uk/docs/Glossary/Truthy).

```js
if (0n) {
  console.log("Привіт з if!");
} else {
  console.log("Привіт з else!");
}

// "Привіт з else!"

0n || 12n;
// 12n

0n && 12n;
// 0n

Boolean(0n);
// false

Boolean(12n);
// true

!12n;
// false

!0n;
// true
```

### Зведення до BigInt

Чимало вбудованих операцій, котрі очікують на BigInt, спершу зводять свої аргументи до BigInt. [Ця операція](https://tc39.es/ecma262/#sec-tobigint) може бути підсумована отак:

- BigInt повертаються як є.
- [`undefined`](/uk/docs/Web/JavaScript/Reference/Global_Objects/undefined) і [`null`](/uk/docs/Web/JavaScript/Reference/Operators/null) викидають {{jsxref("TypeError")}}.
- `true` стає `1n`; `false` стає `0n`.
- Рядки перетворюються шляхом розбору їх так, ніби вони містять цілочисловий літерал. Будь-яка невдача розбору призводить до {{jsxref("SyntaxError")}}. Синтаксис є підмножиною [рядкових літералів чисел](/uk/docs/Web/JavaScript/Reference/Global_Objects/Number#zvedennia-do-chysla), у якій десятковий розділювач і експоненційний запис – заборонені.
- [Number](/uk/docs/Web/JavaScript/Reference/Global_Objects/Number) викидають {{jsxref("TypeError")}} для запобігання небажаному неявному зведенню, що призвело б до втрати точності.
- [Symbol](/uk/docs/Web/JavaScript/Reference/Global_Objects/Symbol) викидають {{jsxref("TypeError")}}.
- Об'єкти [перетворюються на примітиви](/uk/docs/Web/JavaScript/Data_structures#zvedennia-do-prymityva) шляхом виклику їх методів [`[@@toPrimitive]()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toPrimitive) (з підказкою `"number"`), `valueOf()` і `toString()` – у такому порядку. Потім результівний примітив перетворюється на BigInt.

Найкращий спосіб досягнути в JavaScript майже такого ж ефекту – функція [`BigInt()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/BigInt/BigInt): `BigInt(x)` використовує такий же алгоритм для перетворення `x`, окрім того, що [Number](/uk/docs/Web/JavaScript/Reference/Global_Objects/Number) не викидають {{jsxref("TypeError")}}, а перетворюються на BigInt, якщо є цілими числами.

Зверніть увагу, що вбудовані операції, котрі очікують на BigInt, нерідко після зведення обрізають BigInt до фіксованої ширини. Серед таких операцій – {{jsxref("BigInt.asIntN()")}}, {{jsxref("BigInt.asUintN()")}}, а також методи об'єктів {{jsxref("BigInt64Array")}} і {{jsxref("BigUint64Array")}}.

## Конструктор

- [`BigInt()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/BigInt/BigInt)
  - : Створює нове значення BigInt

## Статичні методи

- [`BigInt.asIntN()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/BigInt/asIntN)
  - : Обрізає значення BigInt до знакового цілого числа, і повертає його.
- [`BigInt.asUintN()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/BigInt/asUintN)
  - : Обрізає значення BigInt до беззнакового цілого числа, і повертає його.

## Властивості примірника

- `BigInt.prototype[@@toStringTag]`
  - : Початкове значення [`@@toStringTag`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toStringTag) – рядок `"BigInt"`. Ця властивість використовується в {{jsxref("Object.prototype.toString()")}}. Проте у зв'язку з тим, що `BigInt` також має власну реалізацію метода [`toString()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/BigInt/toString), ця властивість не використовується, якщо не викликати [`Object.prototype.toString.call()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Function/call) зі значенням BigInt як `thisArg`.

## Методи примірника

- [`BigInt.prototype.toLocaleString()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/BigInt/toLocaleString)
  - : Повертає рядок з чутливим до мови представленням цього значення BigInt. Заміщає метод [`Object.prototype.toLocaleString()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Object/toLocaleString).
- [`BigInt.prototype.toString()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/BigInt/toString)
  - : Повертає рядкове представлення цього значення BigInt за заданою основою числення. Заміщає метод [`Object.prototype.toString()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Object/toString).
- [`BigInt.prototype.valueOf()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/BigInt/valueOf)
  - : Повертає це значення BigInt. Заміщає метод [`Object.prototype.valueOf()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf).

## Рекомендації щодо застосування

### Зведення

Через те, що перетворення між значеннями Number та значеннями BigInt можуть призводити до втрати точності, рекомендовано наступне:

- Значення BigInt слід використовувати лише тоді, коли доцільно очікувати значень, більших за 2^53
- Не слід перетворювати між собою значення BigInt і Number.

### Криптографія

Операції, котрі підтримують значення BigInt, мають не сталий час виконання, а тому вразливі до [атак по часу](https://uk.wikipedia.org/wiki/%D0%90%D1%82%D0%B0%D0%BA%D0%B0_%D0%BF%D0%BE_%D1%87%D0%B0%D1%81%D1%83). Таким чином, значення BigInt у JavaScript можуть бути небезпечними для використання в криптографії, якщо не вживати застережних заходів. Як дуже узагальнений приклад – нападник може виміряти часову різницю між `101n ** 65537n` і `17n ** 9999n`, завдяки чому – оцінити потужність таємних значень, як то приватних ключів, на основі витрат часу. Якщо все ж необхідно використовувати BigInt, слід звернутися до [ЧаПів атак по часу](https://timing.attacks.cr.yp.to/programming.html) щодо загальних порад на тему цієї проблеми.

### Використання всередині JSON

Застосування [`JSON.stringify()`](/uk/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) до будь-якого значення BigInt призведе до виринання `TypeError`, адже значення BigInt усталено не серіалізуються в JSON. Проте `JSON.stringify()` залишає саме для значень BigInt запасний хід: ця функція намагається викликати метод BigInt `toJSON()`. (Вона не робить цього для будь-яких інших примітивних значень.) Таким чином, можна реалізувати власний метод `toJSON()` (це один з тих небагатьох випадків, коли внесення змін до вбудованих об'єктів явно не знеохочується):

```js
BigInt.prototype.toJSON = function () {
  return this.toString();
};
```

Замість викидання помилки, тепер `JSON.stringify()` виробляє рядок:

```js
console.log(JSON.stringify({ a: 1n }));
// {"a":"1"}
```

Коли не хочеться вносити зміни до `BigInt.prototype`, можна застосувати для серіалізації значень BigInt параметр `JSON.stringify` [`replacer`](/uk/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#parametr-replacer):

```js
const replacer = (key, value) =>
  typeof value === "bigint" ? value.toString() : value;

const data = {
  number: 1,
  big: 18014398509481982n,
};
const stringified = JSON.stringify(data, replacer);

console.log(stringified);
// {"number":1,"big":"18014398509481982"}
```

Коли є дані JSON, котрі містять значення, про котрі відомо, що там будуть великі цілі числа, то для їх обробки можна використати параметр [`reviver`](/uk/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse#zastosuvannia-parametra-reviver) методу `JSON.parse`:

```js
const reviver = (key, value) => (key === "big" ? BigInt(value) : value);

const payload = '{"number":1,"big":"18014398509481982"}';
const parsed = JSON.parse(payload, reviver);

console.log(parsed);
// { number: 1, big: 18014398509481982n }
```

> **Примітка:** Хоч замінювач для `JSON.stringify()` можна зробити узагальненим, і коректно серіалізувати значення BigInt для всіх можливих об'єктів, та відновлювач для `JSON.parse()` мусить бути конкретним для структури очікуваного корисного навантаження, тому що серіалізація відбувається _зі втратами_: неможливо відрізнити рядок, котрий представляє BigInt, від звичайного рядка.

## Приклади

### Обчислення простих чисел

```js
// Повертає true, якщо передане значення BigInt є простим числом
function isPrime(p) {
  for (let i = 2n; i * i <= p; i++) {
    if (p % i === 0n) return false;
  }
  return true;
}

// Приймає за аргумент значення BigInt, повертає n-не просте число у вигляді значення BigInt
function nthPrime(nth) {
  let maybePrime = 2n;
  let prime = 0n;

  while (nth >= 0n) {
    if (isPrime(maybePrime)) {
      nth--;
      prime = maybePrime;
    }
    maybePrime++;
  }

  return prime;
}

nthPrime(20n);
// 73n
```

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

## Дивіться також

- [`Number`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Number)
- [`Number.MAX_SAFE_INTEGER`](/uk/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)