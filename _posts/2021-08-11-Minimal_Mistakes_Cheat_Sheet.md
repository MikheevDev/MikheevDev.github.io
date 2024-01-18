---
title: "Minimal Mistakes Cheat Sheet"
category:
 - Jekyll
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

Подписи к рисункам по центру : добавьте строку text-align: center;в figcaption 
раздел, _base.css если вы предпочитаете подписи к рисункам по центру.

