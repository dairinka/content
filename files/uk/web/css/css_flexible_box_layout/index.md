---
title: Компонування гнучкої рамки CSS
slug: Web/CSS/CSS_Flexible_Box_Layout
page-type: css-module
spec-urls: https://drafts.csswg.org/css-flexbox/
---

{{CSSRef}}

**Компонування гнучкої рамки CSS** (також відоме під назвою "флексбокс") – це модуль [CSS](/uk/docs/Web/CSS), котрий визначає рамкову модель CSS, оптимізовану для дизайну користувацьких інтерфейсів та компонування елементів в одному вимірі. При моделі гнучкого компонування, дочірні елементи гнучкого контейнера можуть бути розкладені в будь-якому напрямку, а їх розміри є "гнучкими", можуть або збільшуватися – для заповнення невикористаного простору, або зменшуватися – для запобігання переповнення батьківського елемента. Можна легко керувати і горизонтальним, і вертикальним шикуванням дочірніх елементів.

## Базовий приклад

В наступному прикладі контейнер отримує `display: flex`, що означає, що три дочірні елементи стають гнучкими елементами. Значенням `justify-content` стало `space-between`, щоб розташувати елементи рівномірно на головній осі. Однакова кількість простору розташовується між всіма елементами, а лівий і правий елементи знаходяться на краях гнучкого контейнера. Також можна спостерігати, що елементи розтягуються вздовж поперечної осі, адже значення `align-items` – `stretch`. Елементи розтягуються до висоти гнучкого контейнера, тобто кожен з них стає настільки ж високим, як найвищий елемент.

{{EmbedGHLiveSample("css-examples/flexbox/basics/simple-example.html", '100%', 600)}}

## Довідка

### Властивості

- {{cssxref("flex")}}
- {{cssxref("flex-basis")}}
- {{cssxref("flex-direction")}}
- {{cssxref("flex-flow")}}
- {{cssxref("flex-grow")}}
- {{cssxref("flex-shrink")}}
- {{cssxref("flex-wrap")}}
- {{cssxref("order")}}

### Властивості для шикування

Властивості `align-content`, `align-self`, `align-items` і `justify-content` спершу з'явилися в специфікації Флексбоксу, однак тепер – означені в Рамковому шикуванні. Специфікація Флексбоксу тепер посилається на специфікацію Рамкового шикування щодо актуальних означень. Крім цього, тепер в Рамковому шикуванні означені додаткові властивості шикування.

- {{cssxref("justify-content")}}
- {{cssxref("align-content")}}
- {{cssxref("align-items")}}
- {{cssxref("align-self")}}
- {{cssxref("place-content")}}
- {{cssxref("place-items")}}
- {{cssxref("row-gap")}}
- {{cssxref("column-gap")}}
- {{cssxref("gap")}}

## Посібники

- [Базові концепції флексбоксу](/uk/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
  - : Огляд можливостей Флексбоксу
- [Взаємини між флексбоксом та іншими способами компонування](/uk/docs/Web/CSS/CSS_Flexible_Box_Layout/Relationship_of_Flexbox_to_Other_Layout_Methods)
  - : Порівняння Флексбоксу з іншими способами компонування та іншими специфікаціями CSS
- [Шикування елементів у гнучкому контейнері](/uk/docs/Web/CSS/CSS_Flexible_Box_Layout/Aligning_Items_in_a_Flex_Container)
  - : Те, як властивості Рамкового шикування працюють зі Флексбоксом.
- [Упорядкування гнучких елементів](/uk/docs/Web/CSS/CSS_Flexible_Box_Layout/Ordering_Flex_Items)
  - : Пояснення різних способів для змінювання порядку й напряму елементів, а також роз'яснення потенційних негативних наслідків цього.
- [Контроль співвідношень гнучких елементів за головною віссю](/uk/docs/Web/CSS/CSS_Flexible_Box_Layout/Controlling_Ratios_of_Flex_Items_Along_the_Main_Ax)
  - : Пояснення властивостей flex-grow, flex-shrink і flex-basis.
- [Освоєння загортання гнучких елементів](/uk/docs/Web/CSS/CSS_Flexible_Box_Layout/Mastering_Wrapping_of_Flex_Items)
  - : Про те, як створювати гнучкі контейнери з багатьма рядами й контролювати виведення елементів на цих рядах.
- [Типові ситуації для використання флексбоксу](/uk/docs/Web/CSS/CSS_Flexible_Box_Layout/Typical_Use_Cases_of_Flexbox)
  - : Поширені патерни проєктування, котрі є типовими випадками для використання Флексбоксу.

## Специфікації

{{Specifications}}

## Дивіться також

- Терміни Глосарія:
  - {{Glossary("Flexbox", "Флексбокс")}}
  - {{Glossary("Flex Container", "Гнучкий контейнер")}}
  - {{Glossary("Flex Item", "Гнучкий елемент")}}
  - {{Glossary("Main Axis", "Головна вісь")}}
  - {{Glossary("Cross Axis", "Перехресна вісь")}}
  - {{Glossary("Flex", "Гнучкий")}}
