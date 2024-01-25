---
title: "Как создать адаптивную галерею для интернет-магазина"
category:
 - Ruby
tags:
 - Ruby on Rails
---

В этой статье вы узнаете, как создать адаптивную галерею с помощью простенького JavaScript-фреймворка Stimulus 
для HTML-страницы вашего будущего интернет-магазина. Stimulus — это мощная альтернатива SPA, которая позволяет 
разработчикам воплощать в жизнь их задумки по созданию веб-приложений.

Stimulus Components — это проект с открытым исходным кодом, в котором размещена коллекция настраиваемых компонентов
для типичного поведения JavaScript. Один компонент поможет создать в вашем будущем интернет-магазине
многофункциональную адаптивную галерею. Причем никакого пользовательского JavaScript писать вообще не нужно. 
Загляните на lightgallery.js за вдохновением: быть может, у вас появятся новые идеи для собственной галереи.

Stimulus не имеет привязки к каким-либо платформам для создания бэкенда приложений. Поэтому смело используйте
его со своим любимым бэкенд-фреймворком. Для этого руководства был выбран Ruby on Rails.

## Что мы будем создавать?
Адаптивную галерею для интернет-магазина по продаже подушек.

### Прежде чем начинать…
Убедитесь, что Stimulus у вас установлен. Приготовьте файл package.json или запустите yarn why stimulus. 
Если Stimulus пока не установлен, следуйте инструкциям в документации.

Пользователям Rails рекомендую посмотреть GoRails episode. А если у вас есть webpack, просто запустите 
```
rails webpacker:install:stimulus.
```
### Создаем свою адаптивную галерею
1. Установим пакет
Запустите `yarn add stimulus-lightbox` в терминале.

2. Добавим библиотеку Lightbox от Stimulus
```
// app/javascript/controllers/index.js
import { Application } from "stimulus"
import Lightbox from "stimulus-lightbox"
const application = Application.start()
application.register("lightbox", Lightbox)
```
3. Импортируем таблицы стилей
```
// В application.js (например)
import "lightgallery.js/dist/css/lightgallery.min.css"
  
// Или в файле application.scss
@import "lightgallery.js/src/sass/lightgallery"
```
4. Добавим базовый HTML-шаблон
Библиотеке lightgallery.js нужен атрибут data-scr. Он не предоставляется image tag (тегом изображения)
rails по умолчанию. Поэтому добавьте атрибут data-src в HTML вручную.
```html
<div data-controller="lightbox" class="images">
 <%= image_tag "pillow1",  data: { src: "../assets/pillow1.jpg" } %>
 <%= image_tag "pillow2",  data: { src: "../assets/pillow2.jpg" } %>
 <%= image_tag "pillow3",  data: { src: "../assets/pillow3.jpg" } %>
 <%= image_tag "pillow4",  data: { src: "../assets/pillow4.jpg" } %>
</div>
```
5. Добавим изображениям базовое стилевое оформление
```css
<style>
 .images {
 display: flex;
 justify-content: center;
 margin-top: 25px;
 }
img {
 height: 200px;
 width: 200px;
 margin: 10px;
 cursor: pointer;
 }
</style>
```
6. Добавим текст
Сделайте адаптивную галерею более информативной,
добавив в нижней части каждого изображения небольшое текстовое описание.
```html
<div data-controller="lightbox" class="images">
 <%= image_tag "pillow1", data: { src: "../assets/pillow1.jpg", 
          sub_html: "A companion for other pillows." } %>
 <%= image_tag "pillow2", data: { src: "../assets/pillow2.jpg", 
          sub_html: "Always on duty." } %>
 <%= image_tag "pillow3", data: { src: "../assets/pillow3.jpg", 
          sub_html: "Easy to hold with 2 hands."} %>
 <%= image_tag "pillow4", data: { src: "../assets/pillow4.jpg", 
          sub_html: "Or twist when you feel like."} %>
</div
```
7. Добавим дополнительные опции
Подключите дополнительные функции. Полный список параметров для адаптивной галереи доступен по [ссылке](https://sachinchoolur.github.io/lightgallery.js/docs/api.html#lg-thumbnail).

Среди них выделяются:

1) параметры визуальной навигации;
2) бесконечный цикл.
```html
<div data-controller="lightbox" 
     class="images" 
     data-lightbox-options-value='{"controls": true, "loop":true}'>
 
 ...
</div>
```
Если вы не хотите прописывать параметры data-lightbox-options в HTML, расширьте библиотеку функциональности
и добавьте свои опции адаптивной галереи по умолчанию.

Вот и все, адаптивная галерея готова. 
