---
title: Цикли й ітерація
slug: Web/JavaScript/Guide/Loops_and_iteration
tags:
  - Guide
  - JavaScript
  - Loop
  - Syntax
  - "l10n:priority"
---

{{jsSidebar("JavaScript Guide")}}
{{PreviousNext("Web/JavaScript/Guide/Control_flow_and_error_handling",
  "Web/JavaScript/Guide/Functions")}}

Цикли пропонують швидкий і легкий спосіб зробити щось кілька разів. Цей розділ [Посібника з JavaScript](/uk/docs/Web/JavaScript/Guide) знайомить з різними інструкціями ітерації, доступними в JavaScript.

Цикл можна уявити як комп'ютеризовану версію гри, в якій комусь кажуть зробити _X_ кроків в одному напрямку, а тоді _Y_ кроків у іншому. Наприклад, ідея "зробити п'ять кроків на схід" може бути виражена в циклі отак:

```js
for (let step = 0; step < 5; step++) {
  // Спрацьовує 5 разів, причому значення step – від 0 до 4.
  console.log("Крок на схід");
}
```

Є чимало різних видів циклів, але всі вони по суті роблять одне й те ж: повторюють дію певну кількість разів. (Слід мати на увазі, що ця кількість може бути нулем!)

Різні механізми циклів пропонують різні способи визначення початкової й кінцевої точок циклу. Є різні ситуації, котрі легше обробляти за допомогою певного конкретного різновиду циклів.

Інструкції циклів, доступні в JavaScript:

- [Інструкція for](#instruktsiia-for)
- [Інструкція do...while](#instruktsiia-dowhile)
- [Інструкція while](#instruktsiia-while)
- [Інструкція з міткою](#instruktsiia-z-mitkoyu)
- [Інструкція break](#instruktsiia-break)
- [Інструкція continue](#instruktsiia-continue)
- [Інструкція for...in](#instruktsiia-forin)
- [Інструкція for...of](#instruktsiia-forof)

## Інструкція for

Цикл {{jsxref("statements/for","for")}} повторюється, поки певна умова не обчислиться в хибність. Цикл JavaScript `for` подібний до циклу `for` Java та C.

Інструкція `for` має наступний вигляд:

```js
for ([initialExpression]; [conditionExpression]; [incrementExpression])
  statement;
```

Коли виконується цикл `for`, відбувається наступне:

1. Виконується вираз ініціалізації `initialExpression`, якщо він є. Цей вираз зазвичай ініціалізує один чи більше лічильників циклу, але синтаксис дозволяє вираз будь-якої складності. Цей вираз також може оголошувати змінні.
2. Обчислюється вираз `conditionExpression`. Якщо значення `conditionExpression` – істинне, то інструкції циклу виконуються. Інакше – цикл `for` завершується. (Якщо вираз `conditionExpression` повністю упущений, то робиться припущення, що умова виконана.)
3. Виконується `statement`. Щоб виконати декілька інструкцій, для їх групування слід використовувати [блокову інструкцію](/uk/docs/Web/JavaScript/Reference/Statements/block) (`{ }`).
4. Виконується інструкція оновлення `incrementExpression`, якщо вона присутня.
5. Виконання переходить до кроку №2.

### Приклад

У прикладі нижче функція містить інструкцію `for`, котра підраховує кількість обраних варіантів у прокрутному списку (елементі [`<select>`](/uk/docs/Web/HTML/Element/select), що дозволяє вибрати декілька варіантів).

#### HTML

```html
<form name="selectForm">
  <label for="musicTypes"
    >Оберіть кілька різновидів музики, а тоді клацніть кнопку нижче:</label
  >
  <select id="musicTypes" name="musicTypes" multiple>
    <option selected>Ритм-енд-блюз</option>
    <option>Джаз</option>
    <option>Блюз</option>
    <option>Нью-ейдж</option>
    <option>Класична музика</option>
    <option>Опера</option>
  </select>
  <button id="btn" type="button">Скільки різновидів обрано?</button>
</form>
```

#### JavaScript

Тут інструкція `for` оголошує змінну `i` та ініціалізує її значенням `0`. Вона перевіряє, що `i` менша за кількість варіантів у елементі `<select>`, виконує наступну інструкцію `if` та збільшує `i` після кожного проходження тіла циклу.

```js
function howMany(selectObject) {
  let numberSelected = 0;
  for (let i = 0; i < selectObject.options.length; i++) {
    if (selectObject.options[i].selected) {
      numberSelected++;
    }
  }
  return numberSelected;
}

const btn = document.getElementById("btn");

btn.addEventListener("click", () => {
  const musicTypes = document.selectForm.musicTypes;
  console.log(`Обрано варіантів: ${howMany(musicTypes)}.`);
});
```

## Інструкція do...while

Інструкція {{jsxref("statements/do...while", "do...while")}} повторює, поки задана умова не стане хибною.

Інструкція `do...while` має наступний вигляд:

```js-nolint
do
  statement
while (condition);
```

`statement` завжди виконується принаймні один раз до перевірки умови. (Для виконання кількох інструкцій слід використовувати блокову інструкцію (`{ }`), аби їх згрупувати.)

Якщо `condition` – `true`, то інструкція виконується знову. В кінці кожного виконання перевіряється умова. Коли умова стає `false`, виконання зупиняється, і далі відбувається перехід до інструкції, що стоїть після `do...while`.

### Приклад

У наступному прикладі цикл `do` виконується принаймні раз, і повторюється, поки `i` не перестане бути меншою за `5`.

```js
let i = 0;
do {
  i += 1;
  console.log(i);
} while (i < 5);
```

## Інструкція while

Інструкція {{jsxref("statements/while","while")}} виконує інструкції свого тіла, поки задана умова обчислюється в `true`. Інструкція `while` має наступний вигляд

```js-nolint
while (condition)
  statement
```

Якщо `condition` стає `false`, то `statement` усередині циклу зупиняє виконання, далі виконується інструкція після циклу.

Перевірка умови відбувається _до_ виконання `statement` у циклі. Якщо умова повертає `true`, то `statement` виконується, і `condition` перевіряється знову. Якщо умова повертає `false`, то виконання зупиняється, і контроль виконання передається інструкції, що стоїть після `while`.

Для виконання кількох інструкцій слід використовувати блокову інструкцію (`{ }`), аби їх згрупувати.

### Приклад 1

Наступний цикл `while` ітерує, поки `n` є меншою за `3`:

```js
let n = 0;
let x = 0;
while (n < 3) {
  n++;
  x += n;
}
```

З кожною ітерацією цикл збільшує `n` на одиницю і додає нове значення до `x`. Таким чином, `x` і `n` приймають наступні значення:

- Після першого проходження: `n` = `1` і `x` = `1`
- Після другого проходження: `n` = `2` і `x` = `3`
- Після третього проходження: `n` = `3` і `x` = `6`

Після завершення третього проходження умова `n < 3` вже не `true`, тому цикл завершується.

### Приклад 2

Уникайте нескінченних циклів. Слідкуйте, аби умова циклу врешті ставала `false`: інакше цикл ніколи не завершиться! Інструкції наступного циклу `while` виконуються нескінченно, бо умова ніколи не стає `false`:

```js example-bad
// Нескінченні цикли - це погано!
while (true) {
  console.log("Привіт, світе!");
}
```

## Інструкція з міткою

{{jsxref("statements/label","Мітка")}} дає інструкції ідентифікатор, що дає змогу звертатися до неї деінде в програмі. Наприклад, можна використати мітку для ідентифікації циклу, а потім використати інструкції `break` чи `continue`, аби вказати, коли програма повинна перервати цей цикл чи продовжити його виконання.

Синтаксис інструкції з міткою має наступний вигляд:

```js-nolint
label:
  statement
```

Значення `label` може бути будь-яким ідентифікатором JavaScript, що не є зарезервованим словом. `statement`, котра ідентифікується міткою, може бути будь-якою інструкцією.

### Приклад

В цьому прикладі мітка `markLoop` ідентифікує цикл `while`.

```js
markLoop: while (theMark) {
  doSomething();
}
```

## Інструкція break

Для завершення циклу чи `switch` слід використовувати інструкцію {{jsxref("statements/break","break")}} окремо, або вкупі з інструкцією, позначеною міткою.

- Коли `break` використовується без мітки, вона негайно завершує найближчий вкладений `while`, `do-while`, `for` або
  `switch`, що її оточує, і передає контроль виконання до наступної інструкції.
- Коли `break` використовується з міткою, вона завершує вказану інструкцію з міткою.

Синтаксис інструкції `break` має такий вигляд:

```js
break;
break label;
```

1. Перша форма синтаксису завершує найглибший вкладений цикл чи `switch` навколо.
2. Друга форма синтаксису завершує названу інструкцію навколо.

### Приклад 1

Наступний приклад ітерує елементи масиву, поки не знайде індекс елемента, чиє значення – `theValue`:

```js
for (let i = 0; i < a.length; i++) {
  if (a[i] === theValue) {
    break;
  }
}
```

### Приклад 2: переривання за міткою

```js
let x = 0;
let z = 0;
labelCancelLoops: while (true) {
  console.log("Зовнішній цикл: ", x);
  x += 1;
  z = 1;
  while (true) {
    console.log("Внутрішній цикл: ", z);
    z += 1;
    if (z === 10 && x === 10) {
      break labelCancelLoops;
    } else if (z === 10) {
      break;
    }
  }
}
```

## Інструкція continue

Інструкція {{jsxref("statements/continue","continue")}} може використовуватися для перезапуску інструкції
`while`, `do-while`, `for` чи `label`.

- Коли `continue` використовується без мітки, вона завершує поточну ітерацію інструкції `while`, `do-while` чи `for` навколо, що має найглибший рівень вкладеності, й продовжує виконання циклу з наступної ітерації. На противагу інструкції `break`, `continue` не завершує виконання всього циклу. В циклі `while` вона перестрибує назад до умови. В циклі `for` вона перестрибує до `increment-expression`.
- Коли `continue` використовується з міткою, то застосовується до тієї інструкції циклу, яка ідентифікується заданою міткою.

Синтаксис інструкції `continue` має наступний вигляд:

```js
continue;
continue label;
```

### Приклад 1

Наступний приклад демонструє цикл `while` з інструкцією `continue`, що виконується, коли значення `i` – `3`. Таким чином, `n` приймає значення `1`, `3`, `7` і `12`.

```js
let i = 0;
let n = 0;
while (i < 5) {
  i++;
  if (i === 3) {
    continue;
  }
  n += i;
  console.log(n);
}
//1,3,7,12
```

Якщо закоментувати `continue;`, то цикл працюватиме до кінця й виведе `1,3,6,10,15`.

### Приклад 2

Інструкція з міткою `checkiandj` містить іншу, позначену міткою `checkj`, інструкцію. Якщо трапилась `continue`, то програма завершує поточну ітерацію `checkj`, і починає наступну. Щоразу, коли трапляється `continue`, `checkj` повторює виконання, поки її умова не поверне `false`. Коли повернено `false`, завершується решта `checkiandj`, і `checkiandj` повторює своє виконання, поки її умова не поверне `false`. Коли повернено `false`, програма продовжується з інструкції, що стоїть після `checkiandj`.

Якби `continue` мала мітку `checkiandj`, програма продовжилася б з верху інструкції `checkiandj`.

```js
let i = 0;
let j = 10;
checkiandj: while (i < 4) {
  console.log(i);
  i += 1;
  checkj: while (j > 4) {
    console.log(j);
    j -= 1;
    if (j % 2 === 0) {
      continue checkj;
    }
    console.log(j, " непарне число.");
  }
  console.log("i = ", i);
  console.log("j = ", j);
}
```

## Інструкція for...in

Інструкція {{jsxref("statements/for...in","for...in")}} ітерує заданою змінною по всіх перелічуваних властивостях об'єкта. Для кожної окремої властивості JavaScript виконує задані інструкції. Інструкція `for...in` має наступний вигляд:

```js-nolint
for (variable in object)
  statement
```

### Приклад

Наступна функція приймає аргументи з об'єкта та його імені. Потім вона ітерує по всіх властивостях цього об'єкта й повертає рядок, що перелічує імена властивостей та їх значення.

```js
function dumpProps(obj, objName) {
  let result = "";
  for (const i in obj) {
    result += `${objName}.${i} = ${obj[i]}<br>`;
  }
  result += "<hr>";
  return result;
}
```

Для об'єкта `car` з властивостями `make` і `model` `result` буде:

```
car.make = Ford
car.model = Mustang
```

### Масиви

Хоч може здаватись заманливим використати цю інструкцію як спосіб ітерації елементів {{jsxref("Array")}}, `for...in` поверне імена визначених користувачем властивостей на додачу до числових індексів.

Таким чином, краще використовувати для ітерування масивів традиційний цикл {{jsxref("statements/for","for")}} з числовим індексом, адже інструкція `for...in` також ітерує по визначених користувачем властивостях, а не лише елементах масиву, що актуально, якщо об'єкт Array був змінений (тобто якщо були додані власні властивості чи методи).

## Інструкція for...of

Інструкція {{jsxref("statements/for...of","for...of")}} утворює цикл, що ітерує [ітеровані об'єкти](/uk/docs/Web/JavaScript/Reference/Iteration_protocols) (серед яких {{jsxref("Array")}}, {{jsxref("Map")}}, {{jsxref("Set")}}, об'єкт {{jsxref("functions/arguments","arguments")}} і так далі), закликаючи особливий ітераційний гачок з інструкціями, котрі повинні бути виконані для значення кожної окремої властивості.

```js-nolint
for (variable of object)
  statement
```

Наступний приклад демонструє різницю між циклом `for...of` і циклом {{jsxref("statements/for...in","for...in")}}. Коли `for...in` ітерує імена властивостей, `for...of` ітерує значення властивостей:

```js
const arr = [3, 5, 7];
arr.foo = "привіт";

for (const i in arr) {
  console.log(i); // виводить "0", "1", "2", "foo"
}

for (const i of arr) {
  console.log(i); // виводить 3, 5, 7
}
```

{{PreviousNext("Web/JavaScript/Guide/Control_flow_and_error_handling",
  "Web/JavaScript/Guide/Functions")}}