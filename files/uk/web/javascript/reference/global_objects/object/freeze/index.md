---
title: Object.freeze()
slug: Web/JavaScript/Reference/Global_Objects/Object/freeze
browser-compat: javascript.builtins.Object.freeze
---

{{JSRef}}

Метод **`Object.freeze()`** _заморожує_ об'єкт. Замороження об'єкта [перешкоджає його розширенню](/uk/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions), і робить наявні властивості незаписуваними та неналаштовними. Заморожені об'єкти більше не можна змінювати: неможливо додати нові властивості, наявні властивості неможливо видалити, їхні перелічуваність, налаштовність, записуваність чи значення не можна змінити, і не можна повторно присвоїти прототип об'єкта. Виклик `freeze()` повертає той самий об'єкт, який було передано до нього.

Замороження об'єкта — це найвищий рівень цілісності, який може надати JavaScript.

{{EmbedInteractiveExample("pages/js/object-freeze.html")}}

## Синтаксис

```js
Object.freeze(obj)
```

### Параметри

- `obj`
  - : Об'єкт до замороження.

### Повернене значення

Об'єкт, який було передано до функції.

## Опис

Замороження об'єкта рівносильне [перешкоджанню його розширення](/uk/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions), і далі заміні атрибута `configurable` в [дескрипторах](/uk/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty#opys) всіх наявних властивостей на `false`, а для властивостей даних — атрибут `writable` також заміняється на `false`. До переліку властивостей замороженого об'єкта не можна ні додати властивості, ні прибрати наявні. Будь-яка спроба це зробити провалиться: або тихо, або з викиданням винятку {{jsxref("TypeError")}} (найчастіше у {{jsxref("Strict_mode", "суворому режимі", "", 1)}}, хоча й не завжди).

Стосовно властивостей даних у заморожених об'єктів — їхні значення неможливо змінити, адже значенням їхніх атрибутів записуваності та налаштовності встановлюється `false`. Аксесорні властивості (гетери й сетери) працюють як і раніше — значення, повернене гетером, все ще може змінюватися, а сетер і далі зможе викликатися без викидання помилки, під час встановлення значень властивості. Слід зауважити, що ті значення властивостей, які є об'єктами, можна буде й далі змінювати, якщо вони також не заморожені. Як і об'єкт, масив також можна заморозити. Після цього його елементи неможливо буде змінити, і жодного елемента не можна буде додати чи видалити з масиву.

Виклик `freeze()` повертає той самий об'єкт, який було передано до функції. Він _не_ створює замороженої копії.

Примірник {{jsxref("TypedArray")}} чи {{jsxref("DataView")}} з елементами призведе до помилки {{jsxref("TypeError")}}, оскільки такі об'єкти є проєкціями на область пам'яті, і, авжеж, призведуть до інших можливих проблем:

```js
Object.freeze(new Uint8Array(0)) // Без елементів
// Uint8Array []

Object.freeze(new Uint8Array(1)) // З елементами
// TypeError: Cannot freeze array buffer views with elements

Object.freeze(new DataView(new ArrayBuffer(32))) // Без елементів
// DataView {}

Object.freeze(new Float64Array(new ArrayBuffer(64), 63, 0)) // Без елементів
// Float64Array []

Object.freeze(new Float64Array(new ArrayBuffer(64), 32, 2)) // З елементами
// TypeError: Cannot freeze array buffer views with elements
```

Слід зазначити, що, оскільки три стандартні властивості (`buf.byteLength`, `buf.byteOffset` та `buf.buffer`) доступні лише для читання (так само як і аналогічні властивості примірників {{jsxref("ArrayBuffer")}} чи {{jsxref("SharedArrayBuffer")}}), — немає потреби намагатися заморозити ці властивості.

На відміну від {{jsxref("Object.seal()")}}, наявні в об'єктах, заморожених за допомогою `Object.freeze()`, властивості стають імутабельними, а властивості даних — недоступними для повторного присвоєння.

## Приклади

### Замороження об'єктів

```js
const obj = {
  prop() {},
  foo: 'bar'
};

// До заморожування — можна додавати нові властивості,
// а наявні властивості можуть бути змінені чи видалені
obj.foo = 'baz';
obj.lumpy = 'woof';
delete obj.prop;

// Замороження.
const o = Object.freeze(obj);

// Результівне значення — той самий об'єкт, який було передано до функції.
o === obj; // true

// Об'єкт став замороженим.
Object.isFrozen(obj); // === true

// Тепер будь-які зміни зазнають невдачі
obj.foo = 'quux'; // мовчки не робить нічого
// мовчки не додає властивість
obj.quaxxor = 'the friendly duck';

// В суворому режимі такі спроби викидатимуть помилки TypeError
function fail() {
  'use strict';
  obj.foo = 'sparky'; // викидає TypeError
  delete obj.foo; // викидає TypeError
  delete obj.quaxxor; // повертає true, адже атрибут 'quaxxor' не було додано
  obj.sparky = 'arf'; // викидає TypeError
}

fail();

// Спроби внести зміни за допомогою Object.defineProperty.
// Обидві наведені нижче інструкції викинуть TypeError.
Object.defineProperty(obj, 'ohai', { value: 17 });
Object.defineProperty(obj, 'foo', { value: 'eit' });

// Також неможливо змінити прототип,
// обидві наведені нижче інструкції викинуть TypeError.
Object.setPrototypeOf(obj, { x: 20 })
obj.__proto__ = { x: 20 }
```

### Заморожування масивів

```js
const a = [0];
Object.freeze(a); // Тепер масив не можна змінити.

a[0] = 1; // завершується тихою відмовою

// В суворому режимі такі спроби викидатимуть TypeError
function fail() {
  "use strict";
  a[0] = 1;
}

fail();

// Спроба вставити значення за допомогою методу push
a.push(2); // викидає помилку TypeError
```

Заморожений об'єкт стає _імутабельним_. Проте це не обов'язково означає, що він буде _сталим_. Наступний приклад ілюструє, що заморожений об'єкт не є сталим (тобто, замороження є поверхневим).

```js
const obj1 = {
  internal: {}
};

Object.freeze(obj1);
obj1.internal.a = 'якесь значення';

obj1.internal.a // 'якесь значення'
```

Аби стати сталим об'єктом, весь граф посилань (прямі та непрямі посилання на інші об'єкти) повинен посилатися виключно на імутабельні заморожені об'єкти. Заморожений об'єкт називається імутабельним через те, що _стан_ всього об'єкта (значення та посилання на інші об'єкти) всередині цілого об'єкта зафіксовано. Варто зазначити, що рядки, числа, та булеві значення завжди імутабельні, а функції та масиви — це об'єкти.

#### Що означає "поверхневе заморожування"?

Результат виклику `Object.freeze(object)` застосовується лише до безпосередніх властивостей об'єкта `object`, і запобігає майбутнім додаванням нових властивостей, операціям видалення чи повторного присвоєння _лише_ на цьому об'єкті. В разі, якщо ті властивості самі є об'єктами, ті об'єкти не заморожуються, і можуть бути ціллю операцій додавання або видалення властивостей, чи повторного присвоєння значення.

```js
const employee = {
  name: "Маянк",
  designation: "Розробник",
  address: {
    street: "Рогіні",
    city: "Делі"
  }
};

Object.freeze(employee);

employee.name = "Кінь в пальто"; // мовчки завершується невдачею в несуворому режимі
employee.address.city = "Нойда"; // атрибути дочірніх об'єктів можна модифікувати

console.log(employee.address.city); // "Нойда"
```

Аби зробити весь об'єкт незмінним — слід рекурсивно заморозити кожну з тих його властивостей, які мають об'єктний тип (глибоке замороження). Можна застосовувати цей патерн в архітектурі, залежно від конкретного випадку — якщо відомо, що об'єкт не містить [зациклень](<https://uk.wikipedia.org/wiki/%D0%A6%D0%B8%D0%BA%D0%BB_(%D1%82%D0%B5%D0%BE%D1%80%D1%96%D1%8F_%D0%B3%D1%80%D0%B0%D1%84%D1%96%D0%B2)>) у графі залежностей, бо інакше це спричинить нескінченний цикл. Певним вдосконаленням функції `deepFreeze()` було б додати внутрішню функцію, яка б отримувала аргумент (наприклад, масив Array) зі шляхом до об'єкта, щоб можна було заблокувати рекурсивний виклик `deepFreeze()` в разі, якщо об'єкт вже в процесі замороження. Проте залишиться ризик заморозити об'єкт, який заморожуватися не повинен, наприклад — \[window].

```js
function deepFreeze(object) {
  // Отримання назв означених на об'єкті властивостей
  const propNames = Object.getOwnPropertyNames(object);

  // Заморожування властивостей, перед заморожуванням самого себе
  for (const name of propNames) {
    const value = object[name];

    if (value && typeof value === "object") {
      deepFreeze(value);
    }
  }

  return Object.freeze(object);
}

const obj2 = {
  internal: {
    a: null
  }
};

deepFreeze(obj2);

obj2.internal.a = 'якесьІншеЗначення'; // мовчки завершується невдачею в несуворому режимі
obj2.internal.a; // null
```

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

## Дивіться також

- {{jsxref("Object.isFrozen()")}}
- {{jsxref("Object.preventExtensions()")}}
- {{jsxref("Object.isExtensible()")}}
- {{jsxref("Object.seal()")}}
- {{jsxref("Object.isSealed()")}}
