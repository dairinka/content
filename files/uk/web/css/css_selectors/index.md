---
title: Селектори CSS
slug: Web/CSS/CSS_Selectors
page-type: landing-page
spec-urls: https://drafts.csswg.org/selectors/
---

{{CSSRef("Selectors")}}

**Селектори CSS** визначають патерни для вибору елементів, на котрих потім застосовується набір правил CSS.

На основі типів елементів, котрі вони можуть вибирати, селектори CSS можуть бути згруповані в наступні категорії.

## Базові селектори

- [Загальний селектор](/uk/docs/Web/CSS/Universal_selectors)

  - : Вибирає усі елементи. Крім цього, можна додати обмеження для конкретного простору імен, або всіх просторів імен.

    **Синтаксис:** `*` `ns|*` `*|*`

    **Приклад:** `*` дасть збіг з усіма елементами в документі.

- [Селектор типу](/uk/docs/Web/CSS/Type_selectors)

  - : Вибирає усі елементи, що мають задану назву вузла.

    **Синтаксис:** `elementname`

    **Приклад:** `input` дасть збіг з будь-яким елементом {{HTMLElement("input")}}.

- [Селектор класу](/uk/docs/Web/CSS/Class_selectors)

  - : Вибирає всі елементи, що мають заданий атрибут `class`.

    **Синтаксис:** `.classname`

    **Приклад:** `.index` дасть збіг з будь-яким елементом, що має `class="index"`.

- [Селектор ідентифікатора](/uk/docs/Web/CSS/ID_selectors)

  - : Вибирає елемент на основі значення його атрибута `id`. В документі повинен бути лише один елемент з таким ідентифікатором.

    **Синтаксис:** `#idname`

    **Приклад:** `#toc` дасть збіг з елементом, що має `id="toc"`.

- [Селектор атрибута](/uk/docs/Web/CSS/Attribute_selectors)

  - : Вибирає всі елементи, що мають заданий атрибут.

    **Синтаксис:** `[attr]` `[attr=value]` `[attr~=value]` `[attr|=value]` `[attr^=value]` `[attr$=value]` `[attr*=value]`

    **Приклад:** `[autoplay]` дасть збіг з усіма елементами, що мають атрибут `autoplay` (з будь-якими значеннями).

## Групування селекторів

- [Список селекторів](/uk/docs/Web/CSS/Selector_list)

  - : Селектор `,` – це метод групування, що вибирає всі вузли збігів.

    **Синтаксис:** `A, B`

    **Приклад:** `div, span` дасть збіг і з елементами {{HTMLElement("span")}}, і з елементами {{HTMLElement("div")}}.

## Комбінатори

- [Комбінатор нащадків](/uk/docs/Web/CSS/Descendant_combinator)

  - : Комбінатор " " (пробіл) вибирає вузли, що є нащадками першого елемента.

    **Синтаксис:** `A B`

    **Приклад:** `div span` дасть збіг з усіма елементами {{HTMLElement("span")}}, котрі знаходяться всередині елементів {{HTMLElement("div")}}.

- [Дочірній комбінатор](/uk/docs/Web/CSS/Child_combinator)

  - : Комбінатор `>` вибирає вузли, котрі є безпосередніми нащадками першого елемента.

    **Синтаксис:** `A > B`

    **Приклад:** `ul > li` дасть збіг з усіма елементами {{HTMLElement("li")}}, що вкладені безпосередньо в елементи {{HTMLElement("ul")}}.

- [Загальний комбінатор сестер](/uk/docs/Web/CSS/General_sibling_combinator)

  - : Комбінатор `~` вибирає сестринські елементи. Це означає, що другий елемент стоїть після першого (хоч необов'язково зразу після), і вони обидва поділяють спільний батьківський елемент.

    **Синтаксис:** `A ~ B`

    **Приклад:** `p ~ span` дасть збіг з усіма елементами {{HTMLElement("span")}}, котрі стоять після {{HTMLElement("p")}}, зразу чи опосередковано.

- [Комбінатор сусідніх сестер](/uk/docs/Web/CSS/Adjacent_sibling_combinator)

  - : Комбінатор `+` дає збіг з другим елементом лише тоді, коли він стоїть _зразу_ після першого.

    **Синтаксис:** `A + B`

    **Приклад:** `h2 + p` дасть збіг з першим елементом {{HTMLElement("p")}}, котрий стоїть _зразу_ після елемента {{HTMLElement("Heading_Elements", "h2")}}.

- [Колонковий комбінатор](/uk/docs/Web/CSS/Column_combinator) {{Experimental_Inline}}

  - : Комбінатор `||` вибирає вузли, котрі належать до колонки.

    **Синтаксис:** `A || B`

    **Приклад:** `col || td` дасть збіг з усіма елементами {{HTMLElement("td")}}, котрі належать до контексту {{HTMLElement("col")}}.

## Псевдокласи та псевдоелементи

- [Псевдокласи](/uk/docs/Web/CSS/Pseudo-classes)

  - : Псевдо `:` дає змогу вибирати елементи на основі інформації про стан, котра не вміщена в дереві документа.

    **Приклад:** `a:visited` дасть збіг з усіма елементами {{HTMLElement("a")}}, котрі були відвідані користувачем.

- [Псевдоелементи](/uk/docs/Web/CSS/Pseudo-elements)

  - : Псевдо `::` представляє сутності, котрі не включені в HTML.

    **Приклад:** `p::first-line` дасть збіг з першими рядками кожного з елементів {{HTMLElement("p")}}.

## Структура селектора

Термін "селектор" може позначати щось із наступного:

- Простий селектор

  - : Селектор з єдиної складової, як то одного селектора ідентифікатора або селектора типу, котрий не використовується в поєднанні з іншими селекторами й не містить жодних інших селекторів-складових чи комбінаторів. Про елемент кажуть, що він збігається з простим селектором, коли цей простий селектор точно описує елемент. Усі [базові селектори](#bazovi-selektory), атрибути, а також [псевдокласи та псевдоелементи](#psevdoklasy-ta-psevdoelementy) є простими селекторами.

- Складений селектор

  - : Послідовність [простих селекторів](#prostyi-selektor), не розділених [комбінаторами](#kombinatory). Складений селектор представляє набір одночасних умов для кожного елемента. Про елемент кажуть, що він дає збіг зі складовим селектором, коли елемент дає збіг з усіма простими селекторами, що є складовими цього складеного селектора.

    [Селектор типу](/uk/docs/Web/CSS/Type_selectors) або [загальний селектор](/uk/docs/Web/CSS/Universal_selectors) повинен стояти в складеному селекторі першим. У послідовності може бути лише один селектор типу або загальний селектор. Оскільки пробіл представляє [комбінатор нащадків](/uk/docs/Web/CSS/Descendant_combinator), то між простими селекторами складеного селектора не дозволені пробіли.

    **Приклад:** `a#selected {...}`

- Складний селектор

  - : Послідовність з одного або більшої кількості простих чи [складених селекторів](#skladenyi-selektor), розділених [комбінаторами](#kombinatory). Складний селектор представляє набір одночасних умов для набору елементів. Ці умови застосовуються в контексті відносин, описаних комбінаторами. Про елемент кажуть, що він дає збіг зі складним селектором, коли цей елемент дає збіг зі складеними селекторами та комбінаторами між цими складеними селекторами.

    **Приклади:** `a#selected > .icon {...}`, `.box h2 + p {...}`, `a .icon {...}`

- Відносний селектор

  - : Селектор, що представляє елемент, відносний щодо одного чи більшої кількості елементів, перед якими стоїть комбінатор. Відносні селектори, котрі не починаються з явного [комбінатора](#kombinatory), мають неявний [комбінатор нащадків](/uk/docs/Web/CSS/Descendant_combinator).

    **Приклад:** `+ div#topic > #reference {...}`, `> .icon {...}`, `dt:has(+ img) ~ dd {...}`

- [Список селекторів](/uk/docs/Web/CSS/Selector_list)

  - : Розділений комами список [простих](#prostyi-selektor), [складених](#skladenyi-selektor) чи [складних](#skladnyi-selektor) селекторів. Якщо тип списку селекторів є важливим, але не заданий, то такий список зветься _складним списком селекторів_. Про елемент кажуть, що він дає збіг зі списком селекторів, коли цей елемент дає збіг з будь-яким (щонайменше одним) з селекторів цього списку селекторів. Дізнайтесь більше про те, коли список селекторів вважається [недійсним](/uk/docs/Web/CSS/Selector_list#nediisnyi-spysok-selektoriv) і те, як сформувати [поблажливий список селекторів](/uk/docs/Web/CSS/Selector_list#poblazhlyvyi-spysok-selektoriv).

    **Приклад:** `#main, article.heading {...}`

## Специфікації

{{Specifications}}

Дивіться подробиці в таблицях специфікацій [псевдокласу](/uk/docs/Web/CSS/Pseudo-classes#specifications) та [псевдоелемента](/uk/docs/Web/CSS/Pseudo-elements#specifications).

## Дивіться також

- [Псевдоклас `:has()`](/uk/docs/Web/CSS/:has)
- [Специфічність CSS](/uk/docs/Web/CSS/Specificity)
- [Список селекторів](/uk/docs/Web/CSS/Selector_list)
