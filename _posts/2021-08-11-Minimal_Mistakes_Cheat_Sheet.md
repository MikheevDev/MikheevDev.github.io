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
![image-center](/assets/images/pixel_tracker_logo_80p.png){: .align-center}
![image-right](/assets/images/pixel_tracker_logo_80px.png){: .align-right}
![image-left](/assets/images/pixel_tracker_logo_80px.png){: .align-left} You can also place some text right after the image command, and it will nicely wrap around the image.
```
Вы можете дополнительно настроить стиль вашего изображения, например:
```
![styled-image](/assets/images/pixel_tracker_logo_80px.png "This is some hover text"){: .align-center style="width: 5%;"}

[![styled-image](/assets/images/pixel_tracker_logo_80px.png "This is some hover text"){: .align-center style="width: 10%;"}](/assets/images/pixel_tracker_logo_80px.png "Title shown in gallery view")
Some custom styled caption with a [_link_](#via-markdown).
{: .align-caption}
```
### Через HTML

Встраивание изображений с помощью HTML-кода позволяет настраивать дополнительные свойства изображения, 
такие как ширина изображения или подпись:
```html
<figure style="width: 80px" class="align-center">
  <a href="/assets/images/pixel_tracker_logo_120px.jpg" title="The Pixel Tracker logo" alt="The Pixel Tracker logo">
  <img src="/assets/images/pixel_tracker_logo_120px.jpg" alt=""></a>
  <figcaption>Image caption.</figcaption>
</figure>
```
Вы можете создавать галереи, добавляя дополнительные изображения в HTML-код.
Обратите внимание на назначения классов half, thirdкоторые управляют расположением сетки галереи:
```html
<figure class="half">
  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg"></a>

  <figcaption>Gallery with a two image per row grid.</figcaption>
</figure>
```
<figure class="half">
  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg"></a>

  <figcaption>Gallery with a two image per row grid.</figcaption>
</figure>
И так:
```html
<figure class="third">
  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8156-1v (16. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8156-1v (16. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8161-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8161-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8164-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8164-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8175-1v (25. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8175-1v (25. Feb. 2021).jpg"></a>

  <figcaption>Gallery with a three image per row grid.</figcaption>
</figure>
```
<figure class="third">
  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8156-1v (16. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8156-1v (16. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8161-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8161-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8164-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8164-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8175-1v (25. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8175-1v (25. Feb. 2021).jpg"></a>

  <figcaption>Gallery with a three image per row grid.</figcaption>
</figure>

Подписи к рисункам по центру : добавьте строку text-align: center;в figcaption 
раздел, _base.css если вы предпочитаете подписи к рисункам по центру.

Шпаргалка по минимальным ошибкам
 12 августа 2021 г.   31 июля 2023 г.   15 минут чтения  Комментарии
↑
Содержание
Крамдаун
Сообщения
Будущие публикации
потрясающий
Изображений
Через Маркдаун
Через HTML
Через жидкость
Заголовок и тизерные изображения
Видео
Выравнивание и стилизация текста
Сноски
Внутритекстовые якоря
Списки определений
Ящики для уведомлений
Кнопки
Оглавление
Подсветка синтаксиса
Внешние плагины и решения, которые я использую
В этой шпаргалке представлен краткий обзор доступных команд и опций для создания контента с помощью темы Jekyll «Минимальные ошибки» ꜛ от Майкла Роуза ꜛ . Он не охватывает команды Markdown по умолчанию (см. руководство по Markdown ) или настройку темы (см. веб-сайт документации по минимальным ошибкам ꜛ ).

КрамдаунПостоянная ссылка
В теме используется kramdown ꜛ , библиотека, написанная на Ruby, которая отображает Markdown для веб-сайтов Jekyll ꜛ . kramdown позволяет использовать блочные ꜛ и встроенные атрибуты ꜛ , что позволяет настраивать стили для стандартных команд Markdown, например:

Right aligned text.
{: .text-right}
Магия kramdown : что kramdown в дополнение к стандартному рендерингу Markdown, так это, например, возможность использования классов CSS, определенных в фоновом режиме, с помощью удобной команды на переднем плане. Скажем, у нас где-то определен следующий класс CSS:

.green {
  color: green;
}
Теперь этот класс можно применить через:

This text is rendered in green.
{: .green}
     Этот текст отображается зеленым цветом.

Команды kramdown могут включать вызовы нескольких определений стилей CSS, например:

This text is rendered in green and bold.
{: .green .bold}
     Этот текст выделен синим цветом и жирным шрифтом.

Дополнительные примеры см., например, здесь ꜛ .

СообщенияПостоянная ссылка
Добавляйте сообщения в папку ꜛ , следуя соглашению об именах ._posts YYYY-MM-DD-name-of-post.extension

Вводная часть YAML может включать следующие метаданные даты (в соответствии с рекомендациями strftime ):

date:               YYYY-MM-DD HH:mm:S +0000
last_modified_at:   YYYY-MM-DD HH:mm:S +0000
Ссылки на публикации : Для ссылки на публикации имеется дополнительный тег Liquid: post_url.

Будущие публикацииПостоянная ссылка
Чтобы создать будущую публикацию, просто установите ее дату во вступительной части YAML в будущем. Также настройте search: falseтак, чтобы будущий пост был скрыт в поиске вашего сайта (если вы используете Lunr в качестве поисковой системы). И не забудьте установить future: falseв свой _config.yml. Если вы хотите просмотреть сообщение в своей локальной сборке, используйте --futureфлаг для создания своего сайта.

потрясающийПостоянная ссылка
Ссылка на потрясающий ꜛ . Использование:

<i class="fab fa-researchgate" aria-hidden="true"></i>
выход:      

Emojis : в качестве альтернативы Fontawesome вы также можете использовать Emojis :обнимаю: , которые включаются через плагин Jemoji . О том, как установить плагин, читайте здесь .

Юникод : Еще одна альтернатива шрифту — буквы Юникода . Прочтите здесь, как вставить, например, буквы Юникода в причудливом стиле на свой веб-сайт.

ИзображенийПостоянная ссылка
Вставлять изображения можно тремя разными способами:

Через МаркдаунПостоянная ссылка
Вы можете добавить теги kramdown к команде включения изображенияalign Markdown по умолчанию :

![image-center](/assets/images/pixel_tracker_logo_80p.png){: .align-center}
![image-right](/assets/images/pixel_tracker_logo_80px.png){: .align-right}
![image-left](/assets/images/pixel_tracker_logo_80px.png){: .align-left} You can also place some text right after the image command, and it will nicely wrap around the image.
Вы можете дополнительно настроить стиль вашего изображения, например:

![styled-image](/assets/images/pixel_tracker_logo_80px.png "This is some hover text"){: .align-center style="width: 5%;"}

[![styled-image](/assets/images/pixel_tracker_logo_80px.png "This is some hover text"){: .align-center style="width: 10%;"}](/assets/images/pixel_tracker_logo_80px.png "Title shown in gallery view")
Some custom styled caption with a [_link_](#via-markdown).
{: .align-caption}
стилизованное изображение

стилизованное изображениеНекоторая подпись в индивидуальном стиле со ссылкой .

Через HTMLПостоянная ссылка
Встраивание изображений с помощью HTML-кода позволяет настраивать дополнительные свойства изображения, такие как ширина изображения или подпись:

<figure style="width: 80px" class="align-center">
  <a href="/assets/images/pixel_tracker_logo_120px.jpg" title="The Pixel Tracker logo" alt="The Pixel Tracker logo">
  <img src="/assets/images/pixel_tracker_logo_120px.jpg" alt=""></a>
  <figcaption>Image caption.</figcaption>
</figure>

Подпись к изображению.
Вы можете создавать галереи, добавляя дополнительные изображения в HTML-код. Обратите внимание на назначения классов half, thirdкоторые управляют расположением сетки галереи:

<figure class="half">
  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg"></a>

  <figcaption>Gallery with a two image per row grid.</figcaption>
</figure>


Галерея с сеткой из двух изображений в строке.
<figure class="third">
  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8156-1v (16. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8156-1v (16. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8171-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8161-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8161-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8164-1v (21. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8164-1v (21. Feb. 2021).jpg"></a>

  <a href="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8175-1v (25. Feb. 2021).jpg">
  <img src="/weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8175-1v (25. Feb. 2021).jpg"></a>

  <figcaption>Gallery with a three image per row grid.</figcaption>
</figure>






Галерея с сеткой из трех изображений в строке.
Подписи к рисункам по центру : добавьте строку text-align: center;в figcaptionраздел, _base.cssесли вы предпочитаете подписи к рисункам по центру.

### Через Liquid

Вы также можете вставлять изображения через теги Liquid :
```ruby
---
title: "Title of my page"
date: 2021-08-10
gallery1:
  - url: /weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg
    image_path: /weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg
    alt: "placeholder image 1"
    title: "Image 1 title caption"
  - url: /weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8164-1v (21. Feb. 2021).jpg
    image_path: /weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8164-1v (21. Feb. 2021).jpg
    alt: "placeholder image 2"
    title: "Image 2 title caption"
gallery2:
  - url: /weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8175-1v (21. Feb. 2021).jpg
    image_path: /weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8175-1v (21. Feb. 2021).jpg
    alt: "placeholder image 3"
    title: "Image 3 title caption"
---
{% include gallery id="gallery1" caption="This is a sample gallery with **Markdown support**." %}

{% include gallery id="gallery2"  caption="This is a sample gallery with **Markdown support**." %}
```

### Заголовок и тизерные изображения
```ruby
---
title: "Title of my page"
date: 2021-08-10
header:
  teaser: /weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg
  header: /weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg
  og_image: /weekend_stories_pics/2021/2102_Corona_Fruehling/2102 Corona Fruehling 8170-1v (21. Feb. 2021).jpg
---
```
