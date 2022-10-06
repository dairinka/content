---
title: Array.prototype.flat()
slug: Web/JavaScript/Reference/Global_Objects/Array/flat
tags:
  - Array
  - JavaScript
  - Method
  - Prototype
  - Reference
  - flat
  - Polyfill
browser-compat: javascript.builtins.Array.flat
---

{{JSRef}}

Метод **`flat()`** (площина, плоский) створює новий масив шляхом рекурсивного зчеплення, до заданої глибини, всіх підмасивів докупи.

{{EmbedInteractiveExample("pages/js/array-flat.html")}}

## Синтаксис

```js-nolint
flat()
flat(depth)
```

### Параметри

- `depth` {{optional_inline}}
  - : Рівень глибини, що задає те, наскільки глибоко вкладена структура підмасивів повинна бути сплощена.
    Усталено – 1.

### Повернене значення

Новий масив, у котрий зчеплено елементи підмасивів.

## Опис

Метод `flat()` – [копіювальний метод](/uk/docs/Web/JavaScript/Reference/Global_Objects/Array#kopiiuvalni-ta-zminiuvalni-metody). Він не змінює `this`, а повертає [поверхневу копію](/uk/docs/Glossary/Shallow_copy), що містить ті самі елементи, що присутні у вихідному масиві.

Метод `flat()` ігнорує порожні комірки, якщо сплощуваний масив є [розрідженим](/uk/docs/Web/JavaScript/Guide/Indexed_collections#rozridzheni-masyvy). Наприклад, якщо `depth` – 1, то порожні комірки і в кореневому масиві, і в масивах першого рівня вкладеності – ігноруються, але порожні комірки в масивах глибших рівнів зберігаються вкупі з самими цими масивами.

## Альтернативи

### reduce і concat

```js
const arr = [1, 2, [3, 4]];

// Для сплощення масиву на один рівень
arr.flat();
// рівносильно щодо
arr.reduce((acc, val) => acc.concat(val), []);
// [1, 2, 3, 4]

// або – з синтаксисом розкладу
const flattened = (arr) => [].concat(...arr);
```

### reduce + concat + isArray + рекурсія

```js
const arr = [1, 2, [3, 4, [5, 6]]];

// аби реалізувати сплощення глибоких рівнів, використовується рекурсія з reduce і concat
function flatDeep(arr, d = 1) {
  if (!Array.isArray(arr)) {
    return arr;
  }
  return d > 0
    ? arr.reduce((acc, val) => acc.concat(flatDeep(val, d - 1)), [])
    : arr.slice();
}

flatDeep(arr, Infinity);
// [1, 2, 3, 4, 5, 6]
```

### Використання стека

```js
// нерекурсивне глибоке сплощення з використанням стеку
// зверніть увагу, що контролювати глибину – важко й недоцільно, адже довелось би позначити КОЖНЕ значення його глибиною
// також можливо реалізувати без розвороту, з shift й unshift, але операції масивів на кінці зазвичай швидші
function flatten(input) {
  const stack = [...input];
  const res = [];
  while (stack.length) {
    // виштовхнути значення зі стеку
    const next = stack.pop();
    if (Array.isArray(next)) {
      // заштовхати елементи масиву назад, не змінювати вихідне введення
      stack.push(...next);
    } else {
      res.push(next);
    }
  }
  // розвернути для відновлення порядку при введенні
  return res.reverse();
}

const arr = [1, 2, [3, 4, [5, 6]]];
flatten(arr);
// [1, 2, 3, 4, 5, 6]
```

### Використання генераторної функції

```js
function* flatten(array, depth) {
  if (depth === undefined) {
    depth = 1;
  }

  for (const item of array) {
    if (Array.isArray(item) && depth > 0) {
      yield* flatten(item, depth - 1);
    } else {
      yield item;
    }
  }
}

const arr = [1, 2, [3, 4, [5, 6]]];
const flattened = [...flatten(arr, Infinity)];
// [1, 2, 3, 4, 5, 6]
```

## Приклади

### Сплощення вкладених масивів

```js
const arr1 = [1, 2, [3, 4]];
arr1.flat();
// [1, 2, 3, 4]

const arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

const arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]

const arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### Використання flat() на розріджених масивах

Метод `flat()` прибирає порожні комірки масивів:

```js
const arr5 = [1, 2, , 4, 5];
console.log(arr5.flat()); // [1, 2, 4, 5]

const array = [1, , 3, ["a", , "c"]];
console.log(array.flat()); // [ 1, 3, "a", "c" ]

const array2 = [1, , 3, ["a", , ["d", , "e"]]];
console.log(array2.flat()); // [ 1, 3, "a", ["d", порожньо, "e"] ]
console.log(array2.flat(2)); // [ 1, 3, "a", "d", "e"]
```

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

## Дивіться також

- [Поліфіл `Array.prototype.flat` у складі `core-js`](https://github.com/zloirock/core-js#ecmascript-array)
- {{jsxref("Array.prototype.flatMap()")}}
- {{jsxref("Array.prototype.map()")}}
- {{jsxref("Array.prototype.reduce()")}}
- {{jsxref("Array.prototype.concat()")}}
- [Поліфіл](https://github.com/behnammodi/polyfill/blob/master/array.polyfill.js)