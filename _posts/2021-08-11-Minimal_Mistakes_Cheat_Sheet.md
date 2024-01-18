---
title: "Minimal Mistakes Cheat Sheet"
category:
 - Jekyll
header:
  teaser: /assets/images/prev.jpg
  header: /assets/images/prev.jpg
  og_image: /assets/images/prev.jpg
---

В этой шпаргалке представлен краткий обзор доступных команд и опций для создания контента с помощью темы Jekyll
«Minimal Mistakes» от Майкла Роуза. 
Он не охватывает команды Markdown по умолчанию (см. руководство по Markdown ) или настройку темы
(см. веб-сайт документации по Minimal Mistakes).

### Kramdown
В теме используется kramdown, библиотека, написанная на Ruby, которая отображает Markdown для веб-сайтов Jekyll. 
kramdown позволяет использовать блочные и встроенные атрибуты, что позволяет настраивать стили для стандартных команд 
Markdown, например:
```
Right aligned text.
{: .text-right}
```
Магия kramdown : что kramdown в дополнение к стандартному рендерингу Markdown, так это, например, возможность использования классов CSS, определенных в 
фоновом режиме, с помощью удобной команды на переднем плане. Скажем, у нас где-то определен следующий класс CSS:
```css
.green {
  color: green;
}
```
Теперь этот класс можно применить через:
```
This text is rendered in green.
{: .green}
```
This text is rendered in green.
{: .green}

Команды kramdown могут включать вызовы нескольких определений стилей CSS, например:
```
This text is rendered in green and bold.
{: .green .bold}
```
This text is rendered in green and bold.
{: .green .bold}

### Посты

Добавляйте посты в папку, следуя соглашению об именах ._posts YYYY-MM-DD-name-of-post.extension

Вводная часть YAML может включать следующие метаданные даты (в соответствии с рекомендациями strftime ):
```ruby
date:               YYYY-MM-DD HH:mm:S +0000
last_modified_at:   YYYY-MM-DD HH:mm:S +0000
```
Ссылки на публикации : Для ссылки на публикации имеется дополнительный тег Liquid: post_url.

### Будущие публикации

Чтобы создать будущую публикацию, просто установите ее дату во вступительной части YAML в будущем. 
Также настройте `search: false` так, чтобы будущий пост был скрыт в поиске вашего сайта (если вы используете Lunr
в качестве поисковой системы). И не забудьте установить `future: falseв` свой `_config.yml`. 
Если вы хотите просмотреть сообщение в своей локальной сборке, используйте `--future` 
флаг для создания своего сайта.

### Font Awesome

Использование:
```
<i class="fab fa-researchgate" aria-hidden="true"></i>
```
Вывод: <i class="fab fa-researchgate" aria-hidden="true"></i>

### Изображения

Вставлять изображения можно тремя разными способами:

**Через Маркдаун**

Вы можете добавить теги kramdown к команде включения изображения lign Markdown по умолчанию :
```
![image-center](/assets/images/number0progammer.png){: .align-center}
![image-right](/assets/images/number0progammer.png){: .align-right}
![image-left](/assets/images/number0progammer.png){: .align-left} You can also place some text right after the image command, and it will nicely wrap around the image.
```
![image-center](/assets/images/number0progammer.png){: .align-center}

Вы можете дополнительно настроить стиль вашего изображения, например:
```
![styled-image](/assets/images/number0progammer.png "This is some hover text"){: .align-center style="width: 5%;"}

[![styled-image](/assets/images/number0progammer.png "This is some hover text"){: .align-center style="width: 10%;"}](/assets/images/number0progammer.png "Title shown in gallery view")
Some custom styled caption with a [_link_](#via-markdown).
{: .align-caption}
```
![styled-image](/assets/images/number0progammer.png "This is some hover text"){: .align-center style="width: 5%;"}

### Через HTML

Встраивание изображений с помощью HTML-кода позволяет настраивать дополнительные свойства изображения, 
такие как ширина изображения или подпись:
```html
<figure style="width: 80px" class="align-center">
  <a href="/assets/images/prev.jpg" title="The Pixel Tracker logo" alt="The Pixel Tracker logo">
  <img src="/assets/images/prev.jpg" alt=""></a>
  <figcaption>Image caption.</figcaption>
</figure>
```
Вы можете создавать галереи, добавляя дополнительные изображения в HTML-код.
Обратите внимание на назначения классов half, thirdкоторые управляют расположением сетки галереи:
```html
<figure class="half">
  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <figcaption>Gallery with a two image per row grid.</figcaption>
</figure>
```
<figure class="half">
  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <figcaption>Gallery with a two image per row grid.</figcaption>
</figure>

И так:

```html
<figure class="third">
  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <figcaption>Gallery with a three image per row grid.</figcaption>
</figure>
```
<figure class="third">
  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <a href="/assets/images/prev.jpg">
  <img src="/assets/images/prev.jpg"></a>

  <figcaption>Gallery with a three image per row grid.</figcaption>
</figure>


**К сведению** Подписи к рисункам по центру : добавьте строку text-align: center;в figcaption 
раздел, _base.css если вы предпочитаете подписи к рисункам по центру.{: .notice–info}


Заголовок и тизерные изображения
```
---
title: "Title of my page"
date: 2021-08-10
header:
  teaser: /assets/images/prev.jpg
  header: /assets/images/prev.jpg
  og_image: /assets/images/prev.jpg
---
```
Так называемое изображение OpenGraph, определенное в og_image переменной, будет использоваться при предварительном просмотре в социальных сетях, например, в Twitter или Facebook, если headerизображение не установлено. Если также og_image установлено значение no, сайт og_image( site.og_image), определенный в файле, _config.yml будет использоваться в качестве резервного варианта.

Основные изображения в RSS-каналах . Назначенное изображение og_image или teaser также служит тизером для постов в ваших RSS-каналах.

Вы также можете определить изображения заголовка с наложением, так называемы HERO:
```
---
title: "Post with an overlay header image"
date: 2021-08-10
header:
  overlay_image: /assets/images/mdbanner.jpg
  og_image: /assets/images/mdbanner.jpg
  caption: "Photo from the series: [**Portfolio page**](/portfolio/ginger-gulp-identity/)"
  actions:
    - label: "See More"
      url: /portfolio/ginger-gulp-identity/
excerpt: "This post has an overlay header image"
tagline: "This is a custom tagline content which overrides the *default* page excerpt."
---
```
Вы даже можете определить наложение заголовка, просто залитое сплошным цветом :
```
---
title: "Layout: Header Overlay with Background Fill"
header:
  overlay_color: "#333"
---
```
Добавление дополнительной настройки overlay_filter: o#регулирует непрозрачность наложенного изображения.
Замените заполнитель o#любым значением непрозрачности от 0 до 1 (например, overlay_filter: 0.5) 
или используйте еще более сложный параметр rgba(R#, G#, B#, o#)(например, overlay_filter: rgba(255, 0, 0, 0.25)).
```
---
title: "Post with an overlay header image and some overlay filter"
date: 2021-08-10
header:
  overlay_image: /assets/images/mdbanner.jpg
  overlay_filter: rgba(205, 239, 154, 0.30)
---
```
### Видео

Вы можете вставлять видео как в заголовок, так и в содержимое своих страниц. Для встраивания необходимы следующие параметры:

| Параметр  | Описание |
| ------------- | ------------- |
| id  | идентификатор видео  |
| provider  | 	Хостинг-провайдер видео ( youtube, vimeoили google-drive)  |

Например, видео YouTube с URL-адресом https://www.youtube.com/watch?v=XsxDH4HcOWA(короткий URL-адрес:) https://youtu.be/XsxDH4HcOWAможно встроить с помощью:
```
{% include video id="XsxDH4HcOWA" provider="youtube" %}
```
видео Vimeo , например, https://vimeo.com/212731897через:
```
{% include video id="212731897" provider="vimeo" %}
```
и видео с Google Диска , например,
```
https://drive.google.com/file/d/1u41lIbMLbV53PvMbyYc9HzvBug5lNWaO/preview
```
с помощью:
```
{% include video id="1u41lIbMLbV53PvMbyYc9HzvBug5lNWaO" provider="google-drive" %}
```
Чтобы встроить видео в заголовок страницы, добавьте следующие команды в ее заголовок YAML:
```
---
title: Post with a video header
header:
  video:
    id: 212731897
    provider: vimeo
---
```
### Выравнивание и стилизация текста
Помимо команд выравнивания текста Markdown по умолчанию , вы также можете использовать следующие теги kramdown :

```
Left aligned test.
{: style="text-align: left;"}  

Center aligned text.
{: style="text-align: center;"}

Right aligned test.
{: style="text-align: right;"}

Justified aligned test.
{: style="text-align: justify;"}
```
Left aligned test.
{: style="text-align: left;"}  

Center aligned text.
{: style="text-align: center;"}

Right aligned test.
{: style="text-align: right;"}

Justified aligned test.
{: style="text-align: justify;"}

Вы можете улучшить стиль текста, расширив тег kramdown , например:
```
**Some custom styled text with a [_link_](#text-alignment-and-styling).**
{: style="text-align: center; font-size:1.75em; color: #f78c6c;"}

This is *red*{: style="color: red"}
```
**Some custom styled text with a [_link_](#text-alignment-and-styling).**
{: style="text-align: center; font-size:1.75em; color: #f78c6c;"}

This is *red*{: style="color: red"}

### Сноски

Если ваша страница содержит сноски , они по умолчанию будут размещены в конце страницы. Чтобы разместить сноски где-нибудь еще на странице, создайте упорядоченный или неупорядоченный список и добавьте к нему тег kramdown :{:footnotes}
```
test1[^1]
[^1]: Test 1

{:footnotes}
* 

test2[^2]
[^2]: Test 2
```
test1[^1]
[^1]: Test 1

{:footnotes}
* 

test2[^2]
[^2]: Test 2

### Внутритекстовые якоря
В дополнение к синтаксису определения внутритекстовой привязки Markdown по умолчанию вы можете использовать:
```
Text with a [text anchor](#myid1).
{: #myid1}

Text with a [text anchor](#myid2) and a title. 
{:title="The blockquote title"}
{: #myid2}
```
Text with a [text anchor](#myid1).
{: #myid1}

Text with a [text anchor](#myid2) and a title. 
{:title="The blockquote title"}
{: #myid2}

### Списки определений
```
Definition term 1
: Description of term 1

Definition term 2
Definition term 3
: Description of term 3
: Another Description tio term 3
```
Definition term 1
: Description of term 1

Definition term 2
Definition term 3
: Description of term 3
: Another Description tio term 3

### Уведомления
Чтобы создать поля для уведомлений, просто прикрепите тег kramdown{: .notice} к абзацу:
```
**Notice:** This is an important info notice.
{: .notice}
```

|Доступные уведомления|
|---------------------|
|{: .notice}|
|{: .notice--primary}|
|{: .notice--info}|
|{: .notice--warning}|
|{: .notice--danger}|
|{: .notice--success}|

**Примечание:** Это важное информационное уведомление.
{: .notice}

**Основное уведомление:** Это важное информационное уведомление.
{: .notice--primary}

**Информационное уведомление:** Это важное информационное уведомление.
{: .notice--info}

**Предупреждение:** Это важное информационное уведомление.
{: .notice--warning}

**Уведомление об опасности:** Это важное информационное уведомление.
{: .notice--danger}

**Уведомление об успехе:** Это важное информационное уведомление.
{: .notice--success}

Чтобы обернуть несколько абзацев или других элементов, используйте следующие команды Liquid и HTML:
```html
{% capture notice-2 %}
**Extended notice box**:
* You can include lists
* and even fenced code blocks:

```html
<html>
  <body>Some body.<body>
</html>
```
{% endcapture %}

<div class="notice">{{ notice-2 | markdownify }}</div>
```
{% capture notice-2 %}
**Extended notice box**:
* You can include lists
* and even fenced code blocks:

```html
<html>
  <body>Some body.<body>
</html>
```
{% endcapture %}

<div class="notice">{{ notice-2 | markdownify }}</div>

Вы также можете применить следующее решение только для HTML:
```html
<div class="notice--primary" markdown="1">
**Primary Notice with code block:** Some Text...
<p>Some more text....</p>

```html
<html>
  <body>Some body.<body>
</html>
```
</div>
```

<div class="notice--primary" markdown="1">
**Primary Notice with code block:** Some Text...
<p>Some more text....</p>

```html
<html>
  <body>Some body.<body>
</html>
```
</div>

### Кнопки
Добавьте кнопки с помощью тега kramdown{: .btn} или используйте HTML-код:
```
[Button name](#link){: .btn .btn--success}
```
[Например](/services/){: .btn .btn--success}

### Оглавление

Включите оглавление, добавив следующие настройки во вступительную часть YAML вашей страницы:

```
---
toc: true
toc_label: "Unique Title" # default: Content
toc_icon: "heart"  # corresponding Font Awesome icon name without the "fa" prefix
toc_sticky: true   # enables sticky toc
---
```
Вы также можете встроить GitHub Gist:
```
<script src="https://gist.github.com/mmistakes/77c68fbb07731a456805a7b473f47841.js"></script>
```
<script src="https://gist.github.com/mmistakes/77c68fbb07731a456805a7b473f47841.js"></script>

