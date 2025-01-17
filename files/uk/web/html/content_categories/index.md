---
title: Категорії вмісту
slug: Web/HTML/Content_categories 
tags:
  - Advanced
  - Guide
  - HTML
  - NeedsUpdate
  - Web
---

{{HTMLSidebar}}

Більшість елементів [HTML](/uk/docs/Web/HTML) є членами однієї чи кількох **категорій вмісту** — ці категорії групують елементи, що поділяють спільні характеристики. Це розпливчасте групування (воно насправді не створює взаємозв'язків між елементами категорій), але допомагає визначити й описати спільну поведінку категорій та пов'язані з ними правила, особливо коли мова про заплутані подробиці. Крім цього, елемент може не бути членом _жодної_ з цих категорій.

Є три різновиди категорій вмісту:

- Головні категорії вмісту, що описують загальні правила, котрі поділяються багатьма елементами.
- Категорії вмісту форм, що описують правила, спільні для елементів, котрі стосуються форм.
- Особливі категорії вмісту, що описують рідкісні категорії, які поділяються лишень кількома елементами, іноді лише в конкретному контексті.

> **Примітка:** Більш докладне обговорення таких категорій вмісту та відповідної їм функціональності лежить поза обсягом цієї статті; на цю тему може бути доречним прочитати [відповідні частини специфікації HTML](https://html.spec.whatwg.org/multipage/dom.html#kinds-of-content).

[![Діаграма Венна, що демонструє, як взаємовідносяться різні категорії вмісту. Наступні розділи пояснюють ці взаємини у текстовий спосіб.](content_categories_venn.png)](/uk/docs/Web/Guide/HTML/Content_categories/content_categories_venn.png)

## Головні категорії вмісту

### Вміст метаданих

Елементи, що належать до категорії _вмісту метаданих_, видозмінюють представлення чи поведінку решти документа, задають посилання на інші документи чи доносять іншу _супутню_ інформацію.

Елементи, що належать до цієї категорії: {{HTMLElement("base")}}, {{HTMLElement("command")}} {{deprecated_inline}}, {{HTMLElement("link")}}, {{HTMLElement("meta")}}, {{HTMLElement("noscript")}}, {{HTMLElement("script")}}, {{HTMLElement("style")}} і {{HTMLElement("title")}}.

### Потоковий вміст

Потоковий вміст – широка категорія, що охоплює більшість елементів, котрі можуть з'явитися в елементі {{HTMLElement("body")}}, включно з елементами заголовків, розділовими, оповідальними елементами, елементами вбудування, інтерактивними та формовими елементами. Крім цього, до неї належать текстові вузли (крім тих, що містять лише пробільні символи).

Потокові елементи:

- {{HTMLElement("a")}}
- {{HTMLElement("abbr")}}
- {{HTMLElement("address")}}
- {{HTMLElement("article")}}
- {{HTMLElement("aside")}}
- {{HTMLElement("audio")}}
- {{HTMLElement("b")}}
- {{HTMLElement("bdo")}}
- {{HTMLElement("bdi")}}
- {{HTMLElement("blockquote")}}
- {{HTMLElement("br")}}
- {{HTMLElement("button")}}
- {{HTMLElement("canvas")}}
- {{HTMLElement("cite")}}
- {{HTMLElement("code")}}
- {{HTMLElement("command")}} {{deprecated_inline}}
- {{HTMLElement("data")}}
- {{HTMLElement("datalist")}}
- {{HTMLElement("del")}}
- {{HTMLElement("details")}}
- {{HTMLElement("dfn")}}
- {{HTMLElement("div")}}
- {{HTMLElement("dl")}}
- {{HTMLElement("em")}}
- {{HTMLElement("embed")}}
- {{HTMLElement("fieldset")}}
- {{HTMLElement("figure")}}
- {{HTMLElement("footer")}}
- {{HTMLElement("form")}}
- {{HTMLElement("h1")}}
- {{HTMLElement("h2")}}
- {{HTMLElement("h3")}}
- {{HTMLElement("h4")}}
- {{HTMLElement("h5")}}
- {{HTMLElement("h6")}}
- {{HTMLElement("header")}}
- {{HTMLElement("hgroup")}}
- {{HTMLElement("hr")}}
- {{HTMLElement("i")}}
- {{HTMLElement("iframe")}}
- {{HTMLElement("img")}}
- {{HTMLElement("input")}}
- {{HTMLElement("ins")}}
- {{HTMLElement("kbd")}}
- {{HTMLElement("keygen")}} {{deprecated_inline}}
- {{HTMLElement("label")}}
- {{HTMLElement("main")}}
- {{HTMLElement("map")}}
- {{HTMLElement("mark")}}
- {{MathMLElement("math")}}
- {{HTMLElement("menu")}}
- {{HTMLElement("meter")}}
- {{HTMLElement("nav")}}
- {{HTMLElement("noscript")}}
- {{HTMLElement("object")}}
- {{HTMLElement("ol")}}
- {{HTMLElement("output")}}
- {{HTMLElement("p")}}
- {{HTMLElement("picture")}}
- {{HTMLElement("pre")}}
- {{HTMLElement("progress")}}
- {{HTMLElement("q")}}
- {{HTMLElement("ruby")}}
- {{HTMLElement("s")}}
- {{HTMLElement("samp")}}
- {{HTMLElement("script")}}
- {{HTMLElement("section")}}
- {{HTMLElement("select")}}
- {{HTMLElement("small")}}
- {{HTMLElement("span")}}
- {{HTMLElement("strong")}}
- {{HTMLElement("sub")}}
- {{HTMLElement("sup")}}
- {{SVGElement("svg")}}
- {{HTMLElement("table")}}
- {{HTMLElement("template")}}
- {{HTMLElement("textarea")}}
- {{HTMLElement("time")}}
- {{HTMLElement("u")}}
- {{HTMLElement("ul")}}
- {{HTMLElement("var")}}
- {{HTMLElement("video")}}
- {{HTMLElement("wbr")}}

До цієї категорії належать іще кілька елементів, але лише за виконання певних умов:

- {{HTMLElement("area")}}, коли є нащадком елемента {{HTMLElement("map")}}
- {{HTMLElement("link")}}, коли присутній атрибут [itemprop](/uk/docs/Web/HTML/Global_attributes/itemprop)
- {{HTMLElement("meta")}}, коли присутній атрибут [itemprop](/uk/docs/Web/HTML/Global_attributes/itemprop)
- {{HTMLElement("style")}}, коли присутній атрибут `scoped` {{deprecated_inline}}

### Розділовий вміст

Розділовий вміст – підмножина потокового вмісту, тож може використовуватись усюди, де очікується потоковий вміст. Елементи, що належать до моделі розділового вмісту, утворюють [розділ у поточному плані](/uk/docs/Web/HTML/Element/Heading_Elements), котрий визначає область дії елементів {{HTMLElement("header")}}, {{HTMLElement("footer")}} і [заголовкового вмісту](#zaholovkovyi-vmist).

Елементи, що належать до цієї категорії: {{HTMLElement("article")}}, {{HTMLElement("aside")}}, {{HTMLElement("nav")}} і {{HTMLElement("section")}}.

### Заголовковий вміст

Заголовковий вміст – підмножина потокового вмісту, що визначає заголовок розділу, або позначений явним елементом [розділового вмісту](#rozdilovyi-vmist), або неявно визначений самим заголовковим вмістом. Заголовковий вміст може використовуватися всюди, де очікується потоковий вміст.

Елементи, що належать до цієї категорії: {{HTMLElement("h1")}}, {{HTMLElement("h2")}}, {{HTMLElement("h3")}}, {{HTMLElement("h4")}}, {{HTMLElement("h5")}}, {{HTMLElement("h6")}} і {{HTMLElement("hgroup")}}.

> **Примітка:** Хоч елемент {{HTMLElement("header")}} з високою ймовірністю міститиме заголовковий вміст, сам він не є заголовковим вмістом.

> **Примітка:** Елемент {{HTMLElement("hgroup")}} не рекомендується до використання, адже він не працює як слід з допоміжними технологіями. Він був прибраний зі специфікації W3C HTML до завершення HTML 5, але досі є частиною специфікації WHATWG і принаймні частково підтримується більшістю браузерів.

### Оповідальний вміст

Оповідальний вміст – підмножина потокового вмісту, що визначає текст і розмітку, котру містить, і може використовуватись всюди, де очікується потоковий вміст. Відрізки оповідального вмісту утворюють абзаци.

Елементи, що належать до цієї категорії:

- {{HTMLElement("abbr")}}
- {{HTMLElement("audio")}}
- {{HTMLElement("b")}}
- {{HTMLElement("bdo")}}
- {{HTMLElement("br")}}
- {{HTMLElement("button")}}
- {{HTMLElement("canvas")}}
- {{HTMLElement("cite")}}
- {{HTMLElement("code")}}
- {{HTMLElement("command")}} {{deprecated_inline}}
- {{HTMLElement("data")}}
- {{HTMLElement("datalist")}}
- {{HTMLElement("dfn")}}
- {{HTMLElement("em")}}
- {{HTMLElement("embed")}}
- {{HTMLElement("i")}}
- {{HTMLElement("iframe")}}
- {{HTMLElement("img")}}
- {{HTMLElement("input")}}
- {{HTMLElement("kbd")}}
- {{HTMLElement("keygen")}} {{deprecated_inline}}
- {{HTMLElement("label")}}
- {{HTMLElement("mark")}}
- {{MathMLElement("math")}}
- {{HTMLElement("meter")}}
- {{HTMLElement("noscript")}}
- {{HTMLElement("object")}}
- {{HTMLElement("output")}}
- {{HTMLElement("picture")}}
- {{HTMLElement("progress")}}
- {{HTMLElement("q")}}
- {{HTMLElement("ruby")}}
- {{HTMLElement("s")}}
- {{HTMLElement("samp")}}
- {{HTMLElement("script")}}
- {{HTMLElement("select")}}
- {{HTMLElement("small")}}
- {{HTMLElement("span")}}
- {{HTMLElement("strong")}}
- {{HTMLElement("sub")}}
- {{HTMLElement("sup")}}
- {{SVGElement("svg")}}
- {{HTMLElement("textarea")}}
- {{HTMLElement("time")}}
- {{HTMLElement("u")}}
- {{HTMLElement("var")}}
- {{HTMLElement("video")}}
- {{HTMLElement("wbr")}} і простий текст (що не складається з самих пробільних символів).

До цієї категорії належать іще кілька елементів, але лише за виконання певних умов:

- {{HTMLElement("a")}}, коли містить лише оповідальний вміст
- {{HTMLElement("area")}}, коли є нащадком елемента {{HTMLElement("map")}}
- {{HTMLElement("del")}}, коли містить лише оповідальний вміст
- {{HTMLElement("ins")}}, коли містить лише оповідальний вміст
- {{HTMLElement("link")}}, коли присутній атрибут [itemprop](/uk/docs/Web/HTML/Global_attributes/itemprop)
- {{HTMLElement("map")}}, коли містить лише оповідальний вміст
- {{HTMLElement("meta")}}, коли присутній атрибут [itemprop](/uk/docs/Web/HTML/Global_attributes/itemprop)

### Вбудований вміст

Вбудований вміст – підмножина потокового вмісту, що імпортує інші ресурси чи вставляє в документ вміст з іншої мови розмітки чи простору імен і може використовуватися всюди, де очікується потоковий вміст. Серед елементів, що належать до цієї категорії:

- {{HTMLElement("audio")}}
- {{HTMLElement("canvas")}}
- {{HTMLElement("embed")}}
- {{HTMLElement("iframe")}}
- {{HTMLElement("img")}}
- {{MathMLElement("math")}}
- {{HTMLElement("object")}}
- {{HTMLElement("picture")}}
- {{SVGElement("svg")}}
- {{HTMLElement("video")}}.

### Інтерактивний вміст

Інтерактивний вміст є підмножиною потокового вмісту, що включає елементи, котрі розроблені конкретно для взаємодії з користувачем, і можуть використовуватися всюди, де очікується потоковий вміст. Серед елементів, що належать до цієї категорії:

- {{HTMLElement("a")}}
- {{HTMLElement("button")}}
- {{HTMLElement("details")}}
- {{HTMLElement("embed")}}
- {{HTMLElement("iframe")}}
- {{HTMLElement("keygen")}} {{deprecated_inline}}
- {{HTMLElement("label")}}
- {{HTMLElement("select")}} і {{HTMLElement("textarea")}}.

Частина елементів належить до цієї категорії лише за певних умов:

- {{HTMLElement("audio")}}, коли присутній атрибут {{htmlattrxref("controls", "audio")}}
- {{HTMLElement("img")}}, коли присутній атрибут {{htmlattrxref("usemap", "img")}}
- {{HTMLElement("input")}}, коли атрибут [type](/uk/docs/Web/HTML/Element/input#type-typ) не має значення "hidden"
- {{HTMLElement("object")}}, коли присутній атрибут {{htmlattrxref("usemap", "object")}}
- {{HTMLElement("video")}}, коли присутній атрибут {{htmlattrxref("controls", "video")}}

### Відчутний вміст

Вміст є відчутним, коли він не є ані порожнім, ані прихованим; це вміст, що виводиться і є істотним. Елементи, чия модель – потоковий вміст, повинні містити принаймні один вузол, що є відчутним.

### Формовий вміст

Формовий вміст – це підмножина потокового вмісту, що складається з елементів, котрі мають форму-власника, представлену в атрибуті **form**, і може використовуватися всюди, де очікується потоковий вміст. Форма-власник може бути або контейнерним елементом {{HTMLElement("form")}}, або елементом, чий id вказаний в атрибуті **form**.

- {{HTMLElement("button")}}
- {{HTMLElement("fieldset")}}
- {{HTMLElement("input")}}
- {{HTMLElement("keygen")}} {{deprecated_inline}}
- {{HTMLElement("label")}}
- {{HTMLElement("meter")}}
- {{HTMLElement("object")}}
- {{HTMLElement("output")}}
- {{HTMLElement("progress")}}
- {{HTMLElement("select")}}
- {{HTMLElement("textarea")}}

Ця категорія містить декілька підкатегорій:

- перелічені
  - : Елементи, котрі перелічені в колекціях {{domxref("HTMLFormElement.elements", "form.elements")}} і `fieldset.elements`. Включає {{HTMLElement("button")}}, {{HTMLElement("fieldset")}}, {{HTMLElement("input")}}, {{HTMLElement("keygen")}} {{deprecated_inline}}, {{HTMLElement("object")}}, {{HTMLElement("output")}}, {{HTMLElement("select")}} і {{HTMLElement("textarea")}}.
- підписні
  - : Елементи, що можуть бути пов'язані з елементами {{HTMLElement("label")}}. Включає {{HTMLElement("button")}}, {{HTMLElement("input")}}, {{HTMLElement("keygen")}} {{deprecated_inline}}, {{HTMLElement("meter")}}, {{HTMLElement("output")}}, {{HTMLElement("progress")}}, {{HTMLElement("select")}} і {{HTMLElement("textarea")}}.
- подавальні
  - : Елементи, що можуть використовуватися для конструювання набору даних форми, коли вона подається. Включає {{HTMLElement("button")}}, {{HTMLElement("input")}}, {{HTMLElement("keygen")}} {{deprecated_inline}}, {{HTMLElement("object")}}, {{HTMLElement("select")}} і {{HTMLElement("textarea")}}.
- скидані
  - : Елементи, на котрі може повпливати скидання форми. Включає {{HTMLElement("input")}}, {{HTMLElement("keygen")}} {{deprecated_inline}}, {{HTMLElement("output")}}, {{HTMLElement("select")}} і {{HTMLElement("textarea")}}.

## Другорядні категорії

На додачу є кілька другорядних класифікацій елементів, про котрі також може бути корисно знати.

### Елементи підтримки сценаріїв

**Елементи підтримки сценаріїв** – елементи, котрі безпосередньо не докладаються до зображеного виводу документа. Натомість вони служать підтримкою сценаріям, або вміщаючи, або задаючи код сценаріїв, або вміщаючи дані, котрі будуть використані сценаріями.

Елементи підтримки сценаріїв:

- {{HTMLElement("script")}}
- {{HTMLElement("template")}}

## Модель прозорого вмісту

Коли елемент має модель прозорого вмісту, то його вміст мусить мати таку структуру, що була б дійсним HTML 5, навіть коли сам прозорий елемент був би прибраний і заміщений власними дочірніми елементами.

Наприклад, елементи {{HTMLElement("del")}} і {{HTMLElement("ins")}} – є прозорими:

```html
<p>
  Ми вважаємо ці істини <del><em>священними &amp; незаперечними</em></del>
  <ins>самоочевидними</ins>.
</p>
```

Якщо ці елементи прибрати, то такий уривок все одно буде дійсним HTML (хоч і не коректною українською).

```html
<p>
  Ми вважаємо ці істини <em>священними &amp; незаперечними</em> самоочевидними.
</p>
```
