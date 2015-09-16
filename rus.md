# Центрирование в CSS: полное руководство

Центрирование элементов — самая популярная причина для жалоб на CSS. 
*«Ну почему нельзя было сделать всё попроще?»* — возмущаются все кому не лень. 
Думаю, проблема не в том, что это сложно сделать, а в том, что способов 
центрирования элементов такое множество, что бывает 
трудно выбрать подходящий.

Давайте построим древовидную схему для принятия решения и будем надеяться, что 
это всё немного упростит.

Мне нужно отцентрировать элемент...

## По горизонтали

### Является ли элемент строчным или строчно-* (как текст или ссылки)?

Строчные элементы внутри родительского блочного можно центрировать так:

    .center-children {
      text-align: center;
    }

<iframe id="cp_embed_HulzB" src="//codepen.io/chriscoyier/embed/HulzB?default-tab=result&amp;slug-hash=HulzB&amp;theme-id=1&amp;height=184&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="184" frameborder="0"></iframe>

Это сработает для элементов с типом отображения `inline`, `inline-block`, 
`inline-table`, `inline-flex` и т.д.

### Является ли элемент блочным?

Блочный элемент можно центрировать, указав для `margin-left` и 
`margin-right` значение `auto` (а также прописав для него конкретный 
`width`, иначе он займёт всю ширину родительского контейнера и не будет 
нуждаться в центрировании). Для этого часто используют сокращённую запись:

    .center-me {
      margin: 0 auto;
    }

<iframe id="cp_embed_eszon" src="//codepen.io/chriscoyier/embed/eszon?default-tab=result&amp;slug-hash=eszon&amp;theme-id=1&amp;height=200&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="200" frameborder="0"></iframe>

Способ работает независимо от ширины центрируемого блочного элемента и его 
родителя. 

Обратите внимание, что заставить элемент плавать по центру с помощью `float` 
нельзя. [Хотя есть одна хитрость.][1]

### Вам нужно центрировать несколько блочных элементов?

Если вы имеете дело с двумя и больше блочными элементами, размещёнными *в ряд*, 
которые нужно центрировать по горизонтали, возможно, вам потребуется 
изменить тип `display`. Вот что произойдёт, если указать для 
них тип отображения `inline-block` или применить flexbox:

<iframe id="cp_embed_ebing" src="//codepen.io/chriscoyier/embed/ebing?default-tab=result&amp;slug-hash=ebing&amp;theme-id=1&amp;height=438&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="438" frameborder="0"></iframe>

В том же случае, если у вас несколько блочных элементов размещены друг над 
другом, вполне сработает приём с автоматическими отступами:

<iframe id="cp_embed_haCGt" src="//codepen.io/chriscoyier/embed/haCGt?default-tab=result&amp;slug-hash=haCGt&amp;theme-id=1&amp;height=352&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="352" frameborder="0"></iframe>

## По вертикали

С вертикальным центрированием в CSS все немного сложнее:

### Это элемент строчного типа или строчно-* (как текст или гиперссылки)?

#### Он помещается в одну строку?

Иногда строчные/текстовые элементы могут выглядеть отцентрированными по 
вертикали только потому, что у них одинаковые верхнее и нижнее поля (`padding`).

    .link {
      padding-top: 30px;
      padding-bottom: 30px;
    }

<iframe id="cp_embed_ldcwq" src="//codepen.io/chriscoyier/embed/ldcwq?default-tab=result&amp;slug-hash=ldcwq&amp;theme-id=1&amp;height=180&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="180" frameborder="0"></iframe>

Если использование полей по какой-либо причине невозможно, а вы хотите 
отцентрировать текст, который точно не будет переноситься в следующую строку, 
можно использовать хитрость с установкой `line-height` равной высоте элемента, 
это отцентрирует текст:

    .center-text-trick {
      height: 100px;
      line-height: 100px;
      white-space: nowrap;
    }

<iframe id="cp_embed_LxHmK" src="//codepen.io/chriscoyier/embed/LxHmK?default-tab=result&amp;slug-hash=LxHmK&amp;theme-id=1&amp;height=305&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="305" frameborder="0"></iframe>

#### Элемент занимает несколько строк?

Центрирование нескольких строчек текста также можно сделать с помощью 
установки одинаковых верхнего и нижнего полей, однако, если этот вариант вам не 
подходит, можно сделать элемент, в который помещён текст, ячейкой таблицы — 
буквально или же просто её имитацией на CSS. За центрирование в этом 
случае отвечает свойство [`vertical-align`][2], несмотря на то, что обычно 
он просто выравниванивает по горизонтали элементы в ряду. ([Более подробно об этом.][3])

<iframe id="cp_embed_ekoFx" src="//codepen.io/chriscoyier/embed/ekoFx?default-tab=result&amp;slug-hash=ekoFx&amp;theme-id=1&amp;height=426&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="426" frameborder="0"></iframe>

Если вы имеете дело с некоей имитацией таблицы, может быть, стоит использовать 
flexbox? Один дочерний flex-элемент можно довольно легко отцентрировать во 
flex-родителе. 

    .flex-center-vertically {
      display: flex;
      justify-content: center;
      flex-direction: column;
      height: 400px;
    }

<iframe id="cp_embed_uHygv" src="//codepen.io/chriscoyier/embed/uHygv?default-tab=result&amp;slug-hash=uHygv&amp;theme-id=1&amp;height=380&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="380" frameborder="0"></iframe>

Помните, что этот способ подходит только если у родительского контейнера указана 
конкретная ширина (px, % и т.д.), поэтому здесь у контейнера есть высота.

Если оба этих способа не подходят, можно использовать приём «элемент-призрак», при 
котором в контейнер помещается псевдоэлемент с максимальной высотой, и текст 
выравнивается по горизонтали по этому элементу: 

    .ghost-center {
      position: relative;
    }
    .ghost-center::before {
      content: " ";
      display: inline-block;
      height: 100%;
      width: 1%;
      vertical-align: middle;
    }
    .ghost-center p {
      display: inline-block;
      vertical-align: middle;
    }

<iframe id="cp_embed_ofwgD" src="//codepen.io/chriscoyier/embed/ofwgD?default-tab=result&amp;slug-hash=ofwgD&amp;theme-id=1&amp;height=392&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="392" frameborder="0"></iframe>

### Это блочный элемент?

#### Вам известна высота элемента?

Обычно, когда речь идёт о веб-странице, высота может быть неизвестна 
по многим причинам: если изменяется ширина элемента, перераспределение текста 
может изменить высоту. Вариации в стилизации текста могут 
изменить высоту. Изменение количества текста может 
изменить высоту элемента. Элементы с фиксированным соотношением сторон, например, 
изображения, могут изменить высоту при масштабировании — и так далее.

Но, если вам известна высота, вертикальное центрирование можно сделать так:

    .parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;
      height: 100px;
      margin-top: -50px; /* учитывайте поля и границы, если не используете box-sizing: border-box; */
    }

<iframe id="cp_embed_HiydJ" src="//codepen.io/chriscoyier/embed/HiydJ?default-tab=result&amp;slug-hash=HiydJ&amp;theme-id=1&amp;height=457&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="457" frameborder="0"></iframe>

#### Вам неизвестна высота элемента?

Его все-таки можно центрировать, подняв вверх на половину его высоты после 
того, как сдвинули его наполовину вниз:

    .parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
    }

<iframe id="cp_embed_lpema" src="//codepen.io/chriscoyier/embed/lpema?default-tab=result&amp;slug-hash=lpema&amp;theme-id=1&amp;height=469&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="469" frameborder="0"></iframe>

#### Вы можете использовать flexbox?

Не удивительно, что всё это можно сделать значительно проще с помощью [flexbox][4].

    .parent {
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

<iframe id="cp_embed_FqDyi" src="//codepen.io/chriscoyier/embed/FqDyi?default-tab=result&amp;slug-hash=FqDyi&amp;theme-id=1&amp;height=471&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="471" frameborder="0"></iframe>

## И по горизонтали, и по вертикали

Описанные выше приёмы можно комбинировать как угодно, чтобы получить идеально 
отцентрированные элементы. Но, по моему опыту, обычно всё сводится к трём 
вариантам:

### У элемента фиксированная высота и ширина?

Использование отступов с отрицательными значениями, равными половине высоты и 
ширины элемента после того, как для него было прописано абсолютное 
позиционирование в точке 50%/50%, отцентрирует элемент внутри родителя. 
Кроме того, способ хорошо поддерживается браузерами:


    .parent {
      position: relative;
    }

    .child {
      width: 300px;
      height: 100px;
      padding: 20px;

      position: absolute;
      top: 50%;
      left: 50%;

      margin: -70px 0 0 -170px;
    }

<iframe id="cp_embed_JGofm" src="//codepen.io/chriscoyier/embed/JGofm?default-tab=result&amp;slug-hash=JGofm&amp;theme-id=1&amp;height=386&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="386" frameborder="0"></iframe>

### Высота и ширина элемента неизвестны?

Если вам не известны ширина или высота, для центрирования можно использовать 
свойство `transform` и отрицательное значение `translate` по 50% в обоих 
направлениях (оно вычисляется от текущей ширины/высоты элемента):

    .parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

<iframe id="cp_embed_lgFiq" src="//codepen.io/chriscoyier/embed/lgFiq?default-tab=result&amp;slug-hash=lgFiq&amp;theme-id=1&amp;height=412&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="412" frameborder="0"></iframe>

### Вы можете использовать flexbox?

Чтобы выполнить центрирование в обоих направлениях с помощью flexbox, нужно 
использовать два центрирующих свойства:

    .parent {
      display: flex;
      justify-content: center;
      align-items: center;
    }

<iframe id="cp_embed_msItD" src="//codepen.io/chriscoyier/embed/msItD?default-tab=result&amp;slug-hash=msItD&amp;theme-id=1&amp;height=404&amp;user=chriscoyier" scrolling="no" allowtransparency="true" allowfullscreen="true" class="cp_embed_iframe" style="width: 100%; overflow: hidden;" height="404" frameborder="0"></iframe>

## Заключение

С помощью CSS вы можете отцентрировать всё что угодно.

[1]: http://css-tricks.com/float-center/
[2]: http://css-tricks.com/almanac/properties/v/vertical-align/
[3]: http://css-tricks.com/what-is-vertical-align/
[4]: http://css-tricks.com/snippets/css/a-guide-to-flexbox/
