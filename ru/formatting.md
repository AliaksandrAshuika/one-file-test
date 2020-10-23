---
"$title": Formatting guides & tutorials
"$order": '3'
description: Требования к форматированию файлов для amp.dev
formats:
- веб-сайты
- истории
- Объявления
- Эл. адрес
author: CrystalOnScript
---

Руководства и учебные пособия представлены в [Markdown](https://www.markdownguide.org/) с дополнительным форматированием внешнего вида и шорткода.

## Расположение документации

Содержимое amp.dev берется из двух репозиториев: [amp.dev](https://github.com/ampproject/amp.dev) и [AMPHTML](https://github.com/ampproject/amphtml) . Вся справочная документация по компонентам извлекается из AMPHTML либо из встроенных, либо из расширений.

- [Встроенные компоненты](https://github.com/ampproject/amphtml/tree/master/builtins)
- [Компоненты](https://github.com/ampproject/amphtml/tree/master/extensions)
- [Курсы](https://github.com/ampproject/amp.dev/tree/future/pages/content/amp-dev/documentation/courses)
- [Примеры](https://github.com/ampproject/amp.dev/tree/future/pages/content/amp-dev/documentation/examples)
- [Руководства и руководства](https://github.com/ampproject/amp.dev/tree/future/pages/content/amp-dev/documentation/guides-and-tutorials)

Есть еще несколько документов, которые импортируются в amp.dev из AMPHTML. Они [перечислены в этом файле](https://github.com/ampproject/amp.dev/blob/future/platform/config/imports/spec.json) . Не обновляйте эти документы в репозитории amp.dev - ваши изменения будут перезаписаны при последующих сборках!

## Frontmatter

Frontmatter находится в верхней части каждого руководства и учебника.

Пример:

```yaml
$title: Include Custom JavaScript in AMP Pages
$order: 7
formats:
  - websites
author: CrystalOnScript
contributors:
  - fstanis
description: For web experiences requiring a high amount of customization AMP has created amp-script, a component that allows the use of arbitrary JavaScript on your AMP page without affecting the page's overall performance.
```

<table>
  <tr>
   <td>
    <code>$title</code>
   </td>
   <td>Заголовок вашего документа, как он будет отображаться в оглавлении. Начните с заглавной буквы в первом слове, кроме «AMP» и других имен собственных. Используйте амперсанд `&` вместо слова ʻand`.</td>
  </tr>
  <tr>
   <td>
    <code>$order</code>
   </td>
   <td>Определите, где в оглавлении появится ваш документ. Возможно, вам придется отредактировать `$ order` в других документах, чтобы он отображался в правильном месте.</td>
  </tr>
  <tr>
   <td>
    <code>formats</code>
   </td>
   <td>Перечислите возможности AMP, к которым имеет отношение ваш документ. Если ваш документ имеет отношение к веб-сайтам AMP и историям AMP, но не относится к рекламе AMP или электронной почте AMP, вашему фронтмену нужно следующее: `` форматы yaml: - веб-сайты - истории ''</td>
  </tr>
  <tr>
   <td>
<code>author</code>
   </td>
   <td>Автор ты! Используйте свое имя пользователя GitHub.</td>
  </tr>
  <tr>
   <td>
<code>contributors</code>
   </td>
   <td>Перечислите всех, кто внес свой вклад в ваш документ. Это поле не является обязательным.</td>
  </tr>
  <tr>
   <td>
<code>description</code>
   </td>
   <td>Напишите краткое описание своего руководства или учебника. Это помогает с поисковой оптимизацией, передавая вашу работу в руки тех, кто в ней нуждается!</td>
  </tr>
  <tr>
   <td>
<code>tutorial</code>
   </td>
   <td>Добавьте `tutorial: true` к обложке веб-сайта, чтобы рядом с ним появился значок учебника. Учебники находятся внизу своего раздела в оглавлении.</td>
  </tr>
</table>

# Шорткоды

Список шорткодов и их использования можно найти на сайте [documentation.md на GitHub](https://github.com/ampproject/amp.dev/blob/future/contributing/documentation.md#shortcodes) .

## Изображений

amp.dev построен на AMP! Поэтому наши изображения должны соответствовать критериям [`amp-img`](../../../../documentation/components/reference/amp-img.md) . В процессе сборки используется следующий синтаксис для преобразования изображений в правильный формат `amp-img` .

<div class="ap-m-code-snippet">
<pre>{{image ('/ static / img / docs / tutorials / custom-javascript-tutorial / image1.jpg', 500, 369, layout = 'intrinsic', alt = 'Изображение начального учебного приложения по основному сценарию AMP')}}<br></pre>
</div>

## Фильтрация разделов

Некоторые документы могут иметь отношение к нескольким форматам AMP, но для некоторых форматов может потребоваться дополнительное объяснение или информация, не относящаяся к другим. Вы можете отфильтровать эти разделы, заключив их в следующий шорткод.

<div class="ap-m-code-snippet">
<pre>& lsqb; filter sizes = "веб-сайты"]<br>Это видно только для [веб-сайтов] (? Format = веб-сайты).<br>& lsqb; / filter]<br></pre>
</div>

[filter formats="websites"] Это видно только для [веб-сайтов](?format=websites) . [/filter]

[filter formats="websites, email"] Это видно для [веб-сайтов](?format=websites) и [электронной почты](?format=email) . [/filter]

[filter formats="stories"] Это видно для [историй](?format=stories) . [/filter]




## подсказки

Вы можете добавить подсказки и уточнения, заключив текст в следующий шорткод:

<div class="ap-m-code-snippet">
<pre>& lsqb; tip type = "default"]<br>Совет по умолчанию<br>[/tip]<br></pre>
</div>

[tip type="important"] Важно [/tip]

[tip type="note"] Примечание [/tip]

[tip type="read-on"] Продолжение чтения [/tip]




## Фрагменты кода

Поместите фрагменты кода в наборы из трех обратных кавычек, укажите язык в конце первого набора обратных кавычек.

<div class="ap-m-code-snippet">
<pre>`` html<br>// образец кода<br>``<br></pre>
</div>

```css
  // code sample
```

```js
  // code sample
```





Если ваш код содержит двойные фигурные скобки, что часто случается при использовании шаблонов [`amp-mustache`](../../../../documentation/components/reference/amp-mustache.md?format=websites) , вам необходимо обернуть часть кода:

<div class="ap-m-code-snippet">
<pre>`` html<br>{% raw%}<br>// код с двойными фигурными скобками<br>{% endraw%}<br>``<br></pre>
</div>

### Фрагменты кода в списках

Python-Markdown имеет некоторые ограничения. Используйте следующий синтаксис при включении фрагментов кода в списки:

<div class="ap-m-code-snippet">
<pre>1. Первое:<br>& lsqb; исходный код: html]<br><br><p>Содержимое с отступом.</p><br><br>& lsqb; / исходный код]<br>2. Второй<br>3. Третье<br></pre>
</div>

## Предварительный просмотр примеров кода

Примеры кода могут иметь предварительный просмотр и / или ссылку на версию [AMP Playground](https://playground.amp.dev/) .

<div class="ap-m-code-snippet">
  <pre>&lsqb;example preview="default: none|inline|top-frame"
          playground="default: true|false"
          imports="<custom-element-1>,<custom-element-2>,..."
          template="<custom-template>"]
  ```html
    // code sample
  ```
  &lsqb;/example]</pre>
</div>

Примечание. Предварительный просмотр будет автоматически преобразован в текущий выбранный формат при его открытии на игровой площадке 🤯!

Используйте атрибут `preview` чтобы определить, как создается предварительный просмотр:

- **none** : предварительный просмотр не будет создан

- **inline** : предварительный просмотр примера отображается над исходным кодом. Встроенный предварительный просмотр возможен только для обычных примеров веб - сайта , если код не содержит каких - либо `head` элементов. Используйте эту опцию для маленьких примеров , которые не нуждаются в каком - либо стиле или другие `head` элементах (импорт не учитывается, так как они определяются через `imports` атрибут).

- **top-frame** : предварительный просмотр примера отображается над исходным кодом внутри iframe. Ориентацию можно переключать между `portrait` и `landscape` режимами. Вы можете предварительно выбрать ориентацию, указав дополнительный атрибут:

- **ориентация** : по `default: landscape|portrait`

Если требуются настраиваемые элементы, укажите их в атрибуте `imports` в виде списка, разделенного запятыми, с именем компонента, за которым следует двоеточие и версия. Если в вашем коде используется [`amp-mustache`](../../../../documentation/components/reference/amp-mustache.md?format=websites) укажите зависимость в атрибуте `template` .

Для содержания электронной почты со ссылками на ресурсы используйте заполнитель <code>{{server_for_email}}</code> в источнике.

### Встроенный образец

Вот простой встроенный образец. Вы можете определить CSS с помощью встроенных стилей:

<div class="ap-m-code-snippet">
<pre>[example preview="inline" playground="true"]
    ```html
    <div style="background: red; width: 200px; height: 200px;">Hello World</div>
    ```
  [/example]</pre>
</div>

Вот как это выглядит:

[example preview="inline" playground="true"]
```html
<div style="background: red; width: 200px; height: 200px;">Hello World</div>
```
[/example]

Предупреждение: встроенные образцы встраиваются прямо в страницу. Это может привести к конфликтам, если компоненты уже используются на странице (например, `amp-consent` ).

### Предварительный просмотр верхнего кадра

Используйте предварительный просмотр верхнего кадра, когда вам нужно указать элементы заголовка или определить глобальные стили внутри `<style amp-custom>` .

Важно: не добавляйте в заголовок какой-либо шаблонный код AMP, так как он будет добавлен автоматически в зависимости от формата AMP. Добавляйте в голову только те элементы, которые нужны образцу!

<div class="ap-m-code-snippet">
<pre>[example preview="top-frame"
         playground="true"]
    ```html
    <head>
      <script async custom-element="amp-youtube" src="https://cdn.ampproject.org/v0/amp-youtube-0.1.js"></script>
      <style amp-custom>
        body {
          background: red;
        }
      </style>
    </head>
    <body>
      <h1>Hello AMP</h1>
      <amp-youtube width="480"
        height="270"
        layout="responsive"
        data-videoid="lBTCB7yLs8Y">
      </amp-youtube>
    </body>
    ```
  [/example]</pre>
</div>

Вот как это выглядит:

[example preview="top-frame"
         playground="true"]
```html
<head>
  <script async custom-element="amp-youtube" src="https://cdn.ampproject.org/v0/amp-youtube-0.1.js"></script>
  <style amp-custom>
    body {
      background: red;
    }
  </style>
</head>
<body>
  <h1>Hello AMP</h1>
  <amp-youtube width="480"
    height="270"
    layout="responsive"
    data-videoid="lBTCB7yLs8Y">
  </amp-youtube>
</body>
```
[/example]

### AMP-истории

Используйте `preview="top-frame"` вместе с `orientation="portrait"` для предварительного просмотра историй AMP.

<div class="ap-m-code-snippet">
<pre>[example preview="top-frame"
         orientation="portrait"
         playground="true"]
    ```html
    <head>
      <script async custom-element="amp-story"
          src="https://cdn.ampproject.org/v0/amp-story-1.0.js"></script>
      <style amp-custom>
        body {
          font-family: 'Roboto', sans-serif;
        }
        amp-story-page {
          background: white;
        }
      </style>
    </head>
    <body>
      <amp-story standalone>
        <amp-story-page id="cover">
          <amp-story-grid-layer template="vertical">
            <h1>Hello World</h1>
            <p>This is the cover page of this story.</p>
          </amp-story-grid-layer>
        </amp-story-page>
        <amp-story-page id="page-1">
          <amp-story-grid-layer template="vertical">
            <h1>First Page</h1>
            <p>This is the first page of this story.</p>
          </amp-story-grid-layer>
        </amp-story-page>
      </amp-story>
    </body>
    ```
  [/example]</pre>
</div>

Вот как это выглядит:

[example preview="top-frame"
         orientation="portrait"
         playground="true"]
```html
  <head>
    <script async custom-element="amp-story"
        src="https://cdn.ampproject.org/v0/amp-story-1.0.js"></script>
    <style amp-custom>
      body {
        font-family: 'Roboto', sans-serif;
      }
      amp-story-page {
        background: white;
      }
    </style>
  </head>
  <body>
    <amp-story standalone>
      <amp-story-page id="cover">
        <amp-story-grid-layer template="vertical">
          <h1>Hello World</h1>
          <p>This is the cover page of this story.</p>
        </amp-story-grid-layer>
      </amp-story-page>
      <amp-story-page id="page-1">
        <amp-story-grid-layer template="vertical">
          <h1>First Page</h1>
          <p>This is the first page of this story.</p>
        </amp-story-grid-layer>
      </amp-story-page>
    </amp-story>
  </body>
```
[/example]

### Абсолютные URL-адреса для электронной почты AMP

Обратите внимание, как мы используем <code>{{server_for_email}}</code> чтобы сделать URL конечной точки абсолютным, если он встроен в электронное письмо AMP.

<div class="ap-m-code-snippet">
<pre>[example preview="top-frame" playground="true"]
    ```html
    <div class="resp-img">
      <amp-img alt="flowers"
        src="{{server_for_email}}/static/inline-examples/images/flowers.jpg"
        layout="responsive"
        width="640"
        height="427"></amp-img>
    </div>
    ```
  [/example]</pre>
</div>

Вот как это выглядит:

[example preview="top-frame" playground="true"]
```html
<div class="resp-img">
  <amp-img alt="flowers"
    src="{{server_for_email}}/static/inline-examples/images/flowers.jpg"
    layout="responsive"
    width="640"
    height="427"></amp-img>
</div>
```
[/example]

### Спасение от усов tempaltes

Вот пример `top-frame` с использованием удаленной конечной точки. Шаблоны усов необходимо экранировать в образцах с помощью <code>{% raw %}</code> и <code>{% endraw %}</code> :

<div class="ap-m-code-snippet">
  <pre>[example preview="top-frame"
        playground="true"
        imports="amp-list:0.1"
        template="amp-mustache:0.2"]
    ```html
    <amp-list width="auto" height="100" layout="fixed-height"
      src="{{server_for_email}}/static/inline-examples/data/amp-list-urls.json">
      <template type="amp-mustache">{% raw %}
        <div class="url-entry">
          <a href="{{url}}">{{title}}</a>
        </div>
      {% endraw %}
      </template>
    </amp-list>
    ```
[/example]</pre>
</div>

Вот как это выглядит:

[example preview="top-frame"
         playground="true"
         imports="amp-list:0.1"
         template="amp-mustache:0.2"]
```html
<amp-list width="auto" height="100" layout="fixed-height"
  src="{{server_for_email}}/static/inline-examples/data/amp-list-urls.json">
  <template type="amp-mustache">{% raw %}
    <div class="url-entry">
      <a href="{{url}}">{{title}}</a>
    </div>
    {% endraw %}
  </template>
</amp-list>
```
[/example]

## Ссылки

Вы можете ссылаться на другие страницы со стандартным синтаксисом ссылок уценки:

```md
 [link](../../../courses/beginning-course/index.md)
```

При ссылке на другую страницу в amp.dev ссылка будет относительным путем к целевому файлу.

### Якоря

Ссылка на определенные разделы в документе с помощью якорей:

```md
[link to example section](#example-section)
```

Please create the anchor target using `<a name="#anchor-name></a>` before linking to a section with no anchor present. A good place is at the end of the section headline:

```html
## Example section <a name="example-section"></a>
```

В привязке можно использовать только буквы, цифры, тире и подчеркивание. Используйте короткие названия якорей на английском языке, которые соответствуют заголовку или описывают раздел. Убедитесь, что имя привязки уникально внутри документа.

Когда страница переводится, имена привязок не должны изменяться и оставаться на английском языке.

Когда вы создаете привязку, которая будет использоваться в ссылке с другой страницы, вы также должны создать такую же привязку во всех переводах.

### Фильтр формата AMP

Документацию по компонентам, руководства, руководства и примеры можно фильтровать по формату AMP, например веб-сайты AMP или истории AMP. При переходе по ссылке на такую страницу вы должны явно указать формат, который поддерживается целью, добавив параметр формата к ссылке:

```md
 [link](../../learn/amp-actions-and-events.md?format=websites)
```

Только если вы уверены, что цель поддерживает **все** форматы, которые поддерживает ваша страница, вы можете опустить параметр.

### Ссылки на компоненты

Ссылка на справочную документацию по компоненту автоматически укажет на последнюю версию, если в вашей ссылке отсутствует часть версии. Если вы явно хотите указать на версию, укажите полное имя:

```md
 [latest version](../../../components/reference/amp-carousel.md?format=websites)
 [explicit version](../../../components/reference/amp-carousel-v0.2.md?format=websites)
```

## Структура документа

### Заголовки, заголовки и подзаголовки

Первая буква первого слова в заголовках, заголовках и подзаголовках пишется с заглавной буквы, а все последующие строчные. Ожидания включают AMP и другие имена собственные. Заголовок не имеет заголовка `Introduction` , введение следует за названием документа.

### Именование документов

Называйте документы в соответствии с соглашением об именах тире.

<table>
  <tr>
   <td>
<strong>Делать</strong>
   </td>
   <td>
<strong>Не надо</strong>
   </td>
  </tr>
  <tr>
   <td>hello-world-tutorial.md</td>
   <td>hello_world_tutorial.md</td>
  </tr>
  <tr>
   <td>website-fundamentals.md</td>
   <td>websiteFundamentals.md</td>
  </tr>
  <tr>
   <td>actions-and-events.md</td>
   <td>actionsandevents.md</td>
  </tr>
</table>
