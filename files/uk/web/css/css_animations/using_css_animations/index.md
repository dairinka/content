---
title: Застосування анімацій CSS
slug: Web/CSS/CSS_animations/Using_CSS_animations
page-type: guide
---

{{CSSRef}}

**Анімації CSS** роблять можливим анімування переходів від однієї конфігурації стилю CSS до іншої. Анімації складаються з двох деталей: стилю, що описує анімацію CSS, та набору ключових кадрів, котрі вказують на початковий і кінцевий стани стилю анімації, а також можливі проміжні точки.

Є три ключові переваги анімацій CSS над традиційними методиками анімацій, що працюють на сценаріях:

1. Їх легко застосовувати для простих анімацій; їх можна створювати навіть без знання JavaScript.
2. Такі анімації добре працюють навіть тоді, коли система перебуває під навантаженням середнього рівня. Прості анімації на JavaScript нерідко можуть мати погану швидкодію. Рушій візуалізації може застосовувати пропускання кадрів чи інші методики, аби підтримувати швидкодію настільки плавною, наскільки можливо.
3. Передача браузерові контролю над послідовністю анімації дозволяє йому оптимізувати швидкодію й ефективність шляхом, наприклад, зниження частоти оновлення анімації у вкладках, котрі наразі приховані.

## Налаштування анімації

Щоб створити послідовність анімації CSS, елемент, що анімується, оздоблюють властивістю {{cssxref("animation")}} чи її підвластивостями. Це дає змогу налаштовувати хронометраж, тривалість та інші подробиці того, як повинна перебігати анімація. Це **не** налаштовує фактичний вигляд анімації, він виконується за допомогою директиви {{cssxref("@keyframes")}} як це описано в розділі [Визначення послідовності анімації за допомогою ключових кадрів](#vyznachennia-poslidovnosti-animatsii-za-dopomohoiu-kliuchovykh-kadriv) нижче.

Підвластивості {{cssxref("animation")}} – такі:

- {{cssxref("animation-composition")}}
  - : Задає {{Glossary("Composite operation", "складену операцію")}} для використання в тих випадках, коли на одну властивість одночасно впливають кілька анімацій. Ця властивість не є частиною властивості-скорочення `animation`.
- {{cssxref("animation-delay")}}
  - : Задає затримку між завантаженням елемента і стартом послідовності анімації, а також те, чи повинна анімація початися зразу зі свого старту, чи якоїсь позиції посередині.
- {{cssxref("animation-direction")}}
  - : Задає те, чи матиме перша ітерація прямий хід, чи зворотний, і чи будуть наступні ітерації мати почергову зміну ходу або будуть скидатися на початкову точку й повторюватися.
- {{cssxref("animation-duration")}}
  - : Задає тривалість, протягом якої анімація завершує один цикл.
- {{cssxref("animation-fill-mode")}}
  - : Задає те, як анімація застосовує стилі до своєї цілі, до і після її виконання.
- {{cssxref("animation-iteration-count")}}
  - : Задає те, скільки разів повинна повторитися анімація.
- {{cssxref("animation-name")}}
  - : Задає ім'я директиви {{cssxref("@keyframes")}}, котра описує ключові кадри анімації.
- {{cssxref("animation-play-state")}}
  - : Задає паузу чи відновлення анімації.
- {{cssxref("animation-timing-function")}}
  - : Задає те, як анімація переходить між ключовими кадрами, шляхом встановлення кривих прискорення.

## Визначення послідовності анімації за допомогою ключових кадрів

Після налаштування хронометражу анімації, треба визначити її вигляд. Це виконується шляхом створення одного чи більше ключових кадрів за допомогою директиви {{cssxref("@keyframes")}}. Кожний ключовий кадр описує те, як повинен візуалізуватися анімований елемент у певну мить протягом послідовності анімації.

Оскільки хронометраж анімації визначається стилем CSS, котрий налаштовує анімацію, ключові кадри використовують {{cssxref("percentage", "відсотки")}} для вказівки на час, коли під час анімації вони спрацюють. 0% вказує на першу мить послідовності анімації, а 100% – на фінальний стан анімації. Через те, що ці дві миті такі важливі, вони мають особливі псевдоніми: `from` і `to`. Обидва – необов'язкові. Якщо `from`/`0%` чи `to`/`100%` – не задано, то браузер почне або завершить анімацію, використовуючи обчислені значення всіх атрибутів.

Можна, хоча не обов'язково, включити додаткові ключові кадри, котрі описують проміжні кроки між початком і кінцем анімації.

## Застосування скорочення animation

Скорочення {{cssxref("animation")}} – корисне для економії простору. Як приклад, частина правил, що використовуються в цій статті:

```css
p {
  animation-duration: 3s;
  animation-name: slidein;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
```

...можуть бути замінені шляхом використання скорочення `animation`.

```css
p {
  animation: 3s infinite alternate slidein;
}
```

Аби дізнатися більше про послідовність, у котрій за допомогою скорочення `animation` можуть задаватися різні значення властивостей анімації, зверніться до довідкової сторінки {{cssxref("animation")}}.

## Задання декількох значень властивостей анімації

Специфічні властивості анімації CSS можуть приймати декілька значень, розділених комами. Ця можливість може використовуватися, коли треба застосувати до одного правила декілька анімацій, встановивши для кожної з них різні тривалості, кількості ітерацій тощо. Погляньмо на кілька невеличких прикладів, котрі пояснюють різні перестановки.

У цьому першому прикладі є три тривалості й три кількості ітерацій. Тож кожна анімація отримує значення тривалості й кількості ітерацій на такій само позиції, що й ім'я анімації. Анімація `fadeInOut` отримує тривалість `2.5s` й кількість ітерацій `2`, а анімація `bounce` отримує тривалість `1s` і кількість ітерацій `5`.

```css
animation-name: fadeInOut, moveLeft300px, bounce;
animation-duration: 2.5s, 5s, 1s;
animation-iteration-count: 2, 1, 5;
```

У цьому, другому прикладі, задаються три імені анімацій, але є лише одна тривалість й одна кількість ітерацій. У такому випадку всі три анімації отримують однакові тривалість і кількість анімацій.

```css
animation-name: fadeInOut, moveLeft300px, bounce;
animation-duration: 3s;
animation-iteration-count: 1;
```

У цьому, третьому прикладі, задаються три анімації, але лише дві тривалості й дві кількості ітерацій. У таких випадках, коли в списку недостатньо значень, аби надати кожній анімації окреме, присвоєння значень йде від першого елемента до останнього в доступному списку, а потім продовжується від першого. Таким чином, `fadeInOut` отримує тривалість `2.5s`, `moveLeft300px` отримує тривалість `5s`, що є останнім значенням в списку значень тривалості. Присвоєння значень тривалості далі перестрибує на перше значення; `bounce`, таким чином, отримує тривалість `2.5s`. Значення кількості ітерацій (та інші задані значення властивостей) присвоюються так само.

```css
animation-name: fadeInOut, moveLeft300px, bounce;
animation-duration: 2.5s, 5s;
animation-iteration-count: 2, 1;
```

Якщо розбіжність числа анімацій та числа значень властивостей анімації – зворотна, скажімо, є п'ять значень `animation-duration` для трьох значень `animation-name`, то надлишкові чи невикористані значення властивості, в цьому випадку – два значення `animation-duration`, не застосовуються до жодної анімації й ігноруються.

## Приклади

> **Примітка:** Частина старих браузерів (до 2017 року) могли потребувати префіксів; живі приклади, котрі для перегляду треба клацнути, включають синтаксис із префіксом `-webkit`.

### Текст, що ковзає вікном браузера

Цей зразок так оздоблює елемент {{HTMLElement("p")}}, що текст ковзає до і від правого краю вікна браузера.

Зверніть увагу, що анімації штибу цієї можуть призвести до того, що сторінка стане ширшою за вікно браузера. Аби цього уникнути цієї проблеми, слід помістити анімований елемент у контейнер, і цьому контейнеру задати {{cssxref("overflow")}}`:hidden`.

```css
p {
  animation-duration: 3s;
  animation-name: slidein;
}

@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```

В цьому прикладі стиль елемента {{HTMLElement("p")}} задає, що виконання анімації від її початку до завершення повинно зайняти 3 секунди, за допомогою властивості {{cssxref("animation-duration")}}, і що ім'я директиви {{cssxref("@keyframes")}}, котра визначає ключові фрейми для послідовності анімації, – "slidein".

Якби ми хотіли якогось специфічного оздоблення елемента {{HTMLElement("p")}}, що з'явилось би у браузерах, котрі не підтримують анімації CSS, то включили б його і сюди; проте в цьому випадку не хочемо жодного оздоблення, крім самого ефекту анімації.

Ключові фрейми визначаються за допомогою директиви {{cssxref("@keyframes")}}. В цьому випадку є лишень два ключові фрейми. Перший трапляється на 0% (використовує псевдонім `from`). Тут ми задаємо лівий зовнішній відступ елемента 100% (тобто аж до правого краю контейнерного елемента), а ширину елемента 300% (чи втричі більшою за ширину контейнерного елемента). Це призводить до того, що перший фрейм анімації має заголовок на правому краю вікна браузера.

Другий (і фінальний) ключовий фрейм трапляється на 100% (використовує псевдонім `to`). Лівий зовнішній відступ – 0%, а ширина елемента – 100%. Це призводить до того, що заголовок закінчує свою анімацію на рівні лівого краю області вмісту.

```html
<p>
  Коли лежиш в полі лицем до неба і вслухаєшся в многоголосу тишу полів, то
  помічаєш, що в ній щось є не земне, а небесне.
</p>
```

> **Примітка:** Аби побачити анімацію – перезавантажте сторінку.

{{EmbedLiveSample("tekst-shcho-kovzaie-viknom-brauzera","100%","250")}}

### Додавання іще одного ключового фрейму

Додаймо до анімації попереднього прикладу іще один ключовий фрейм. Скажімо, хочеться, аби розмір шрифту збільшувався при русі справа наліво, а тоді зменшувався назад. Для цього достатньо додати такий ключовий фрейм:

```css
75% {
  font-size: 300%;
  margin-left: 25%;
  width: 150%;
}
```

Повний код тепер має наступний вигляд:

```css
p {
  animation-duration: 3s;
  animation-name: slidein;
}

@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  75% {
    font-size: 300%;
    margin-left: 25%;
    width: 150%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```

```html
<p>
  Коли лежиш в полі лицем до неба і вслухаєшся в многоголосу тишу полів, то
  помічаєш, що в ній щось є не земне, а небесне.
</p>
```

Такий код каже браузерові, що на 75% послідовності анімації заголовок повинен мати лівий зовнішній відступ 25%, а ширину – 150%.

> **Примітка:** Аби побачити анімацію – перезавантажте сторінку.

{{EmbedLiveSample("dodavannia-ishche-odnoho-kliuchovoho-freimu","100%","250")}}

### Повторення анімації

Щоб анімація повторювалася, треба додати властивість {{cssxref("animation-iteration-count")}}, котра вказує на те, скільки разів треба повторити анімацію. У цьому випадку використаймо `infinite`, аби анімація повторювалася нескінченно:

```css
p {
  animation-duration: 3s;
  animation-name: slidein;
  animation-iteration-count: infinite;
}
```

Додавши це до наявного коду:

```css
@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```

```html
<p>
  Коли лежиш в полі лицем до неба і вслухаєшся в многоголосу тишу полів, то
  помічаєш, що в ній щось є не земне, а небесне.
</p>
```

{{EmbedLiveSample("povtorennia-animatsii","100%","250")}}

### Анімація з рухом назад і вперед

Приклад вище змусив анімацію повторюватися, але вельми дивно, що вона щоразу скаче на початок, коли починається. Насправді хочеться, аби текст рухався текстом назад і вперед. Це легко реалізувати, задавши властивість {{cssxref("animation-direction")}} зі значенням `alternate`:

```css
p {
  animation-duration: 3s;
  animation-name: slidein;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
```

І – решта коду:

```css
@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```

```html
<p>
  Коли лежиш в полі лицем до неба і вслухаєшся в многоголосу тишу полів, то
  помічаєш, що в ній щось є не земне, а небесне.
</p>
```

{{EmbedLiveSample("animatsiia-z-rukhom-nazad-i-vpered","100%","250")}}

### Використання подій анімації

Над анімаціями можна отримати додатковий контроль – а також корисну інформацію про них – шляхом використання подій анімації. Такі події, представлені об'єктом {{domxref("AnimationEvent")}}, можуть використовуватися для відстеження того, коли анімації починаються, завершуються і коли починають нову ітерацію. Кожна подія містить час, коли вона відбулася, а також ім'я анімації, що спричинила подію.

Змінімо приклад з ковзанням тексту, аби вивести певну інформацію про кожну подію анімації, що спрацьовує, аби побачити, як ці події працюють.

#### Додавання CSS

Почнімо з CSS для анімації. Ця анімація триватиме 3 секунди, зватиметься "slidein", повториться 3 рази, щоразу зі зміною напряму. В {{cssxref("@keyframes")}} width і margin-left змінюються, аби змусити елемент ковзати екраном.

```css
.slidein {
  animation-duration: 3s;
  animation-name: slidein;
  animation-iteration-count: 3;
  animation-direction: alternate;
}

@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```

#### Додавання слухачів подій анімації

Застосуймо код JavaScript для слухання всіх трьох можливих подій анімації. Код нижче налаштовує слухачів подій; він викликається, коли документ завантажився, щоб усе приготувати.

```js
const element = document.getElementById("watchme");
element.addEventListener("animationstart", listener, false);
element.addEventListener("animationend", listener, false);
element.addEventListener("animationiteration", listener, false);

element.className = "slidein";
```

Це вельми стандартний код; подробиці про те, як він працює, можна знайти в документації {{domxref("eventTarget.addEventListener()")}}. Останнє, що робить цей код – присвоєння `class` елемента, що анімується, значення "slidein"; це робиться, щоб почати анімацію.

Чому? Бо подія `animationstart` спрацьовує, щойно почалась анімація, а в нашому випадку це відбувається до спрацювання нашого коду. Тож почнімо анімацію самі, встановивши клас елемента зі стилем, що, зрештою, анімується.

#### Отримання подій

Події передаються функції `listener()`, показаній нижче.

```js
function listener(event) {
  const l = document.createElement("li");
  switch (event.type) {
    case "animationstart":
      l.textContent = `Почалося: час, що минув – ${event.elapsedTime}`;
      break;
    case "animationend":
      l.textContent = `Скінчилося: час, що минув – ${event.elapsedTime}`;
      break;
    case "animationiteration":
      l.textContent = `Новий цикл почався після ${event.elapsedTime}`;
      break;
  }
  document.getElementById("output").appendChild(l);
}
```

Цей код також є вельми простим. Він дивиться на {{domxref("event.type")}}, аби визначити, якого роду подія анімації сталася, а потім додає відповідний запис у {{HTMLElement("ul")}} (невпорядкований список), що використовується як журнал таких подій.

Вивід після всього цього має якийсь такий вигляд:

- Почалося: час, що минув – 0
- Новий цикл почався після 3.01200008392334
- Новий цикл почався після 6.00600004196167
- Скінчилося: час, що минув – 9.234000205993652

Зверніть увагу, що миті часу дуже наближені до очікуваних згідно з заданим часом анімації, але не рівні їм. Також зверніть увагу, що після фінальної ітерації анімації подія `animationiteration` не надсилається; замість неї надсилається подія `animationend`.

Заради повноти – ось HTML, що виводить вміст сторінки, включно зі списком, до якого сценарій вставляє інформацію про отримані події:

```html
<h1 id="watchme">Дивіться, як я рухаюсь</h1>
<p>
  Цей приклад демонструє, як використовувати анімації CSS, аби елементи
  <code>H1</code> рухались по сторінці.
</p>
<p>
  На додачу – щоразу, коли спрацьовує подія анімації, виводиться певний текст,
  тож ці події помітні в дії.
</p>
<ul id="output"></ul>
```

І ось – справжній вивід.

> **Примітка:** Аби побачити анімацію – перезавантажте сторінку.

{{EmbedLiveSample('vykorystannia-podii-animatsii', '600', '300')}}

## Дивіться також

- {{domxref("AnimationEvent", "AnimationEvent")}}
- [Поради та хитрощі щодо анімацій CSS](/uk/docs/Web/CSS/CSS_animations/Tips)
- [Застосування переходів CSS](/uk/docs/Web/CSS/CSS_transitions/Using_CSS_transitions)
