---
title: Класи
slug: Web/JavaScript/Reference/Classes
tags:
  - Classes
  - Constructors
  - ECMAScript 2015
  - Guide
  - Inheritance
  - Intermediate
  - JavaScript
browser-compat: javascript.classes
---
{{JsSidebar("Classes")}}

Класи — це зразки, за якими створюються нові об'єкти. Вони інкапсулюють дані й код, який працює з цими даними. Класи в JS побудовані на прототипах, хоча вони містять певні синтаксичні й семантичні особливості, не властиві подібній до класів семантиці ES5.

## Описання класів

Насправді класи — це "особливі {{jsxref("Functions", "функції", "", "true")}}". Тож так само як функції оголошуються за допомогою {{jsxref("Operators/function", "функціонального виразу", "", "true")}} та {{jsxref("Statements/function", "оголошення функції", "", "true")}}, синтаксис класів також має два варіанти: {{jsxref("Operators/class", "класові вирази", "", "true")}} та {{jsxref("Statements/class", "оголошення класів", "", "true")}}.

### Оголошення класів

Одним зі способів задати клас є **оголошення класу**. Для описання класу використовується ключове слово `class` з іменем класу (в цьому випадку "Rectangle").

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

#### Підіймання

Суттєва різниця між **оголошенням функцій** та **оголошенням класів** полягає в тому, що функції можна викликати в коді до їх оголошення, тоді як клас слід спочатку оголосити, а потім вже створювати його екземпляри. Код, подібний до наведеного нижче, викине {{jsxref("ReferenceError")}}:

```js example-bad
const p = new Rectangle(); // ReferenceError

class Rectangle {}
```

Це відбувається тому, що хоча сам клас і {{Glossary("Hoisting", "підіймається")}}, його значення не ініціалізуються.

### Класові вирази

**Класові вирази** — це інший спосіб створити клас. Класові вирази можуть бути як іменовані, так і не іменовані. Ім'я, дане класовому виразові, буде локальним відносно тіла класу. Однак, це ім'я також доступне через властивість {{jsxref("Function.name", "name")}}.

```js
// неіменований клас
let Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// вивід: "Rectangle"

// іменований клас
let Rectangle = class Rectangle2 {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// вивід: "Rectangle2"
```

> **Зауваження:** Класові **вирази** повинні бути оголошені до того, як їх можна буде використовувати (вони підпорядковуються таким самим правилам підняття, які описано в розділі [Оголошення класів](#Оголошення%20класів)).

## Тіло класу і описання методів

Тілом класу називається та його частина, яка знаходиться всередині фігурних дужок `{}`. Це місце, де оголошуються члени класу, такі як методи чи конструктор.

### Суворий режим

Тіло класу виконується в {{jsxref("Strict_mode", "суворому режимі", "", "true")}}. Це означає, що код, записаний тут, має суворіші правила синтаксису для покращення швидкодії; також будуть викидатися деякі, зазвичай тихі, винятки; а певні ключові слова будуть зарезервовані для майбутніх версій ECMAScript.

### Конструктор

{{jsxref("Classes/constructor", "Конструктор", "", "true")}} — це спеціальний метод для створення та ініціалізації об'єктів, створених за допомогою класу. В класі може міститися лише один особливий метод з іменем "constructor". Якщо клас містить більше одного методу `constructor`, то буде викинуто виняток {{jsxref("SyntaxError")}}.

Конструктор може використовувати ключове слово `super`, щоб звернутись до конструктора батьківського класу.


### Блоки статичної ініціалізації

[Блоки статичної ініціалізації в класах](/en-US/docs/Web/JavaScript/Reference/Classes/Class_static_initialization_blocks) дають змогу гнучко ініціалізувати [статичні властивості класу](#static_methods_and_properties), в тому числі виконувати інструкції під час ініціалізації та надавати доступ до приватних областей.

Можна оголошувати декілька статичних блоків і перемежовувати їх з оголошеннями статичних методів та властивостей (всі статичні елементи опрацьовуються в порядку їх оголошення).


### Методи прототипу

Дивіться також {{jsxref("Functions/Method_definitions", "визначення методу", "", "true")}}.

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  // Геттер
  get area() {
    return this.calcArea();
  }
  // Метод
  calcArea() {
    return this.height * this.width;
  }
}

const square = new Rectangle(10, 10);

console.log(square.area); // 100
```

### Методи-генератори

Дивіться також [Ітератори й генератори](/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators).

```js
class Polygon {
  constructor(...sides) {
    this.sides = sides;
  }
  // Метод
  *getSides() {
    for(const side of this.sides){
      yield side;
    }
  }
}

const pentagon = new Polygon(1,2,3,4,5);

console.log([...pentagon.getSides()]); // [1,2,3,4,5]
```

### Статичні методи і властивості

Ключове слово {{jsxref("Classes/static", "static", "", "true")}} оголошує статичний метод чи властивість класу. Статичні члени (властивості та методи) викликаються без створення екземплярів їхнього класу і **не можуть** викликатись через екземпляр класу. Статичні методи часто використовуються для створення допоміжних функцій для застосунку, тоді як статичні властивості корисні для кешів, фіксованої конфігурації чи будь-яких інших даних, які не потрібно повторювати між екземплярами.

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  static displayName = "Point";
  static distance(a, b) {
    const dx = a.x - b.x;
    const dy = a.y - b.y;

    return Math.hypot(dx, dy);
  }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);
p1.displayName; // undefined
p1.distance;    // undefined
p2.displayName; // undefined
p2.distance;    // undefined

console.log(Point.displayName);      // "Point"
console.log(Point.distance(p1, p2)); // 7.0710678118654755
```

### Прив'язка `this` до прототипу і статичних методів

Коли статичний метод чи метод прототипу викликається без значення {{jsxref("Operators/this", "this")}} — наприклад, шляхом присвоєння цього методу змінній, і викликання її — значення всередині методу `this` буде дорівнювати `undefined`. Така поведінка зберігається навіть за відсутності директиви {{jsxref("Strict_mode", "\"use strict\"")}}, оскільки код всередині синтаксичних меж тіла класу завжди виконується в суворому режимі.

```js
class Animal {
  speak() {
    return this;
  }
  static eat() {
    return this;
  }
}

let obj = new Animal();
obj.speak(); // об'єкт Animal
let speak = obj.speak;
speak(); // undefined

Animal.eat() // клас Animal
let eat = Animal.eat;
eat(); // undefined
```

Якщо ми перепишемо наведений вище код у традиційному синтаксисі, за допомогою функцій у нестрогому режимі, то звертання до `this` у коді методів будуть автоматично прив'язані до первісного значення `this`, яке усталено дорівнює {{Glossary("Global_object", "глобальному об'єкту")}}. В суворому режимі автоматичне прив'язування не відбувається, а значення `this` залишається таким, яким його було передано до методу.

```js
function Animal() { }

Animal.prototype.speak = function() {
  return this;
}

Animal.eat = function() {
  return this;
}

let obj = new Animal();
let speak = obj.speak;
speak(); // глобальний об'єкт (у нестрогому режимі)

let eat = Animal.eat;
eat(); // глобальний об'єкт (у нестрогому режимі)
```

### Властивості екземпляру

Властивості екземпляру повинні задаватись всередині методів класу:

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

### Оголошення полів

#### Оголошення публічних полів

Згідно з синтаксисом JavaScript для оголошення полів, наведений вище приклад можна записати так:

```js
class Rectangle {
  height = 0;
  width;
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

Попереднє оголошення полів робить описання класу більш самодокументованим, і також гарантує наявність цих полів.

Як було показано вище, поля можуть оголошуватись як з усталеним значенням, так і без нього.

Для отримання додаткової інформації зверніть увагу на розділ {{jsxref("Classes/Public_class_fields", "публічні поля класу", "", "true")}}.

#### Оголошення приватних полів

Вищезазначений опис класу можна переробити у такий спосіб, застосувавши приватні поля:

```js
class Rectangle {
  #height = 0;
  #width;
  constructor(height, width) {
    this.#height = height;
    this.#width = width;
  }
}
```

Звертання до приватних полів класу зовні є помилкою, їх можна читати й записувати лише всередині тіла класу. Шляхом оголошення полів класу, невидимих ззовні, можна гарантувати, що користувачі класу не матимуть змоги залежати від внутрішніх деталей реалізації, які можуть змінюватися від версії до версії.

> **Зауваження:** Приватні поля можна оголошувати лише заздалегідь, під час опису полів.

Приватні поля не можна створювати пізніше шляхом присвоєння їм значень, так, як це можна робити зі звичайними властивостями.

Додаткову інформацію можна знайти в розділі {{jsxref("Classes/Private_class_fields", "приватні особливості класу", "", "true")}}.

## Створення підкласів за допомогою `extends`

Ключове слово {{jsxref("Classes/extends", "extends")}} використовується в _оголошеннях класів_ чи _класових виразах_ для створення класу, який є нащадком іншого класу.

```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} галасує.`);
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name); // виклик конструктора суперкласу і передача параметру імені в нього
  }

  speak() {
    console.log(`${this.name} гавкає.`);
  }
}

let d = new Dog('Сірко');
d.speak(); // Сірко гавкає.
```

Якщо в підкласі наявний конструктор, перед використанням "this" він повинен спершу викликати `super()`.

Також можна розширювати класи, виконані в традиційному синтаксисі, на основі функцій:

```js
function Animal (name) {
  this.name = name;
}

Animal.prototype.speak = function () {
  console.log(`${this.name} галасує.`);
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} гавкає.`);
  }
}

let d = new Dog('Сірко');
d.speak(); // Сірко гавкає.

// Якщо зустрічаються однакові методи, метод нащадка матиме перевагу над батьківським методом
```

Зауважте, що класи не можуть розширяти звичайні об'єкти (ті, що не мають конструктора). Якщо потрібно наслідувати звичайний об'єкт, можна натомість вжити {{jsxref("Object.setPrototypeOf()")}}:

```js
const Animal = {
  speak() {
    console.log(`${this.name} галасує.`);
  }
};

class Dog {
  constructor(name) {
    this.name = name;
  }
}

// Без цього рядка буде викинуто виняток TypeError під час виклику методу `speak`
Object.setPrototypeOf(Dog.prototype, Animal);

let d = new Dog('Сірко');
d.speak(); // Сірко галасує.
```

## Види

Може виникнути потреба повернути об'єкт {{jsxref("Array")}} з похідного від масиву класу `MyArray`. Патерн «види» дозволяє заміщувати усталені конструктори.

Наприклад, під час використання таких методів, як {{jsxref("Array.map", "map()")}}, які повертають усталений конструктор, може виникнути потреба повернути батьківський об'єкт `Array` замість `MyArray`. Символ {{jsxref("Symbol.species")}} дозволяє цього досягти таким чином:

```js
class MyArray extends Array {
  // Заміщуємо вид так, що він вказує на батьківський конструктор Array
  static get [Symbol.species]() { return Array; }
}

let a = new MyArray(1,2,3);
let mapped = a.map(x => x * x);

console.log(mapped instanceof MyArray); // false
console.log(mapped instanceof Array);   // true
```

## Звертання до надкласів за допомогою `super`

Ключове слово {{jsxref("Operators/super", "super")}} використовується для викликання відповідних методів надкласу. Це одна із переваг над прототипним наслідуванням.

```js
class Cat {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} галасує.`);
  }
}

class Lion extends Cat {
  speak() {
    super.speak();
    console.log(`${this.name} гарчить.`);
  }
}

let l = new Lion('Пушок');
l.speak();
// Пушок галасує.
// Пушок гарчить.
```

## Домішки

Абстрактні підкласи, або _домішки_ — це шаблони для класів. Клас в ECMAScript може мати лише один надклас, тож множинне наслідування від, наприклад, інструментальних класів, не є можливим. Така функціональність повинна надаватися надкласом.

Функція, яка приймає надклас на вхід, і розширяє цей надклас на виході, може використовуватись для реалізації домішок в ECMAScript:

```js
let calculatorMixin = Base => class extends Base {
  calc() { }
};

let randomizerMixin = Base => class extends Base {
  randomize() { }
};
```

Клас, який використовує ці домішки, можна записати таким чином:

```js
class Foo { }
class Bar extends calculatorMixin(randomizerMixin(Foo)) { }
```

## Повторне виконання опису класу

Клас не можна описати повторно. Спроба це зробити призведе до помилки `SyntaxError`.

Якщо ви експериментуєте з кодом у середовищі веббраузера, такому як «Firefox Web Console» (**Tools** > **Web Developer** > **Web Console**), і виконаєте опис класу з одним і тим самим іменем двічі, то отримаєте `SyntaxError: redeclaration of let ClassName;`. (Дивіться продовження дискусії цієї проблеми в {{Bug(1428672)}}.) Виконання подібної дії у «Chrome Developer Tools» виведе повідомлення, схоже на `Uncaught SyntaxError: Identifier 'ClassName' has already been declared at <anonymous>:1:1`.

## Специфікації

{{Specifications}}

## Сумісність із браузерами

{{Compat}}

## Дивіться також

- {{jsxref("Functions", "Функції", "", "true")}}
- {{jsxref("Statements/class", "Оголошення класів", "", "true")}}
- {{jsxref("Operators/class", "Вирази класів", "", "true")}}
- {{jsxref("Classes/Public_class_fields", "Публічні поля класів", "", "true")}}
- {{jsxref("Classes/Private_class_fields", "Приватні особливості класів", "", "true")}}
- {{jsxref("Operators/super", "super")}}
- [Допис у блозі: "ES6 In Depth: Classes"](https://hacks.mozilla.org/2015/07/es6-in-depth-classes/)
- [Fields and public/private class properties proposal (stage 3)](https://github.com/tc39/proposal-class-fields)