---
title: "Руководство по Markdown"
toc: true
toc_label: "Содержание" # default: Content
toc_icon: "file-alt"  # corresponding Font Awesome icon name without the "fa" prefix
toc_sticky: true 
tags:
 - Jekyll
header:
  teaser: /assets/images/Markdown.jpeg
  header: /assets/images/Markdown.jpeg
  og_image: /assets/images/Markdown.jpeg
---

Это руководство по Markdown предназначено для обзора синтаксиса Markdown и предоставления 
простых в использовании примеров. В нем отсутствуют подробные описания синтаксиса,и он просто показывает 
практические примеры, которые вы можете напрямую применить к своему документу Markdown.

### Заголовки
```
# First level headline
## Second level headline
### Third level headline
```
### Форматирование текста

| Команда | Отображение |
| :----------- | -----------: | 
|  `This is **bold**.`       |      This is **bold**.   |
|  `This is __bold__.`  |      This is __bold__.  |
|  `This is *italicized*.`  |      This is *italicized*.   |
|  `This is _italicized_.`  |      This is _italicized_.  |
|  `This is ***bold and italicized***.`  |      This is ***bold and italicized***.   |
|  `This is ___bold and italicized___.`  |      This is ___bold and italicized___.   |
|  `This is ~~strikethrough~~.`  |      This is ~~strikethrough~~.   |
|  `This is a <sup>superscript</sup>.`  |      This is a <sup>superscript</sup>.   |
|  `This is a <sub>subscript</sub>.`  |      This is a <sub>subscript</sub>.   |

<div class="notice--info">
  Подчеркивание текста : для подчеркивания текста не существует команды Markdown, поскольку это 
  форматирование зарезервировано для обозначения гиперссылок. Тем не менее, подчеркивание возможно с 
  помощью HTML-тега <u>your text</u>, который преобразуется в: ваш текст .
</div>

### Цвет шрифта
Вы можете изменить цвет шрифта, вставив следующий HTML-код:
```
This is <span style="color:blue">my *blue*</span> text.<br>
This is <span style="color:#FF33AB">my **custom** _colored_</span> text, using a hex color code.
```
This is <span style="color:blue">my *blue*</span> text.<br>
This is <span style="color:#FF33AB">my **custom** _colored_</span> text, using a hex color code.

<div class="notice--info">
Цвета HTML : вы можете выбрать один из следующих предопределенных цветов: белый , серый , черный , 
красный , зеленый , синий , голубой , пурпурный или желтый . Вы также можете использовать онлайн-палитры 
цветов HTML, такие как htmlcolorcodes.com ꜛ , чтобы найти шестнадцатеричный код цвета нужного цвета.
</div>

### Выравнивание текста
Вы можете принудительно выровнять текст, вставив следующий HTML-код:
```html
<center>
  My centered text.
</center>

<div align="center">
  My centered text.
</div>

<div align="right">
  My right aligned text.
</div>

<div align="left">
  My left aligned text.
</div>
```

<center>
  My centered text.
</center>

<div align="center">
  My centered text.
</div>

<div align="right">
  My right aligned text.
</div>

<div align="left">
  My left aligned text.
</div>

### Вставка дополнительных пробелов
Вы можете заставить процессор Markdown вставлять дополнительные пробелы,
вставив следующие HTML-теги &nbsp;(1x), &ensp;(2x) и &emsp;(4x):

```html
&nbsp; Here we insert one extra space.<br>
&ensp; Here we insert two extra spaces.<br>
&emsp; Here we insert four extra spaces.<br>
&nbsp;&nbsp;&nbsp;&nbsp; Here we insert indent-type extra spaces.<br>
... because inserting just extra standard spaces          has no effect.
```
&nbsp; Here we insert one extra space.<br>
&ensp; Here we insert two extra spaces.<br>
&emsp; Here we insert four extra spaces.<br>
&nbsp;&nbsp;&nbsp;&nbsp; Here we insert indent-type extra spaces.<br>
... because inserting just extra standard spaces          has no effect.

<div class="notice--info">
Сохранение слов вместе . Чтобы слова или отдельные символы оставались вместе, т. е. чтобы предотвратить 
автоматический перенос строки между ними, просто соедините их с помощью HTML-тега &nbsp;, 
например: Пожалуйста, &nbsp;держите эти &nbsp;слова вместе &nbsp;. 
Конечно, это работает и в HTML.
</div>

### Разрывы строк
Вы можете заставить процессор Markdown вставить дополнительный разрыв строки, вставив тег HTML <br>:
```html
This is my text, <br> with two extra line<br>breaks.


This is another line...
<br>

...with an extra empty line to the next line.
```

This is my text, <br> with two extra line<br>breaks.


This is another line...
<br>

...with an extra empty line to the next line.

### Горизонтальные линии
```
***

---
```
### Списки
```
* entry 1
* entry 2
  * sub-entry 1
      * sub-sub-entry 1
* entry 3
```
* entry 1
* entry 2
  * sub-entry 1
      * sub-sub-entry 1
* entry 3

### Нумерованные списки
```
1. numbered entry 1
2. numbered entry 2
  - a sub entry
3. numbered entry 3
```
1. numbered entry 1
2. numbered entry 2
  - a sub entry
3. numbered entry 3

*Инициализация списка элементов с номером :*
```
* 2019\. ...That was a great year!
* I think that 2019 was a great year.
```
* 2019\. ...That was a great year!
* I think that 2019 was a great year.

### Добавление элементов в список
Вы можете добавлять в список другие элементы, сохраняя его непрерывность:
```
* entry 1

  This is an extra elemente

* entry 2

  > a quote

```
* entry 1

  This is an extra elemente

* entry 2

  > a quote


### Списки задач
```
- [x] taks 1
- [ ] taks 2
- [ ] taks 3
```
- [x] taks 1
- [ ] taks 2
- [ ] taks 3

### Ссылки
```ruby
Link to [Python](https://www.python.org).
```
Вы также можете добавить заголовок:

```ruby
Link to [Python](https://www.python.org "Link to the Python website").
```
Вы можете добавлять ссылки также в ссылочном стиле:
```html
Link to [Python][1] via referencing.<br>
You can even re-use the [link-reference][1] as many times as you want to.

[1]: <https://www.python.org>
```
<div class="notice--info">
Примечание . Вы можете разместить определение ссылки ( [#]: link) в 
любом месте документа. Например, вы можете поместить все определения 
ссылок внизу документа, чтобы иметь обзор доступных ссылок в документе.
</div>

### Отображение URL-адресов и адресов электронной почты
Вы можете связать и отобразить полный URL-адрес веб-адреса одной командой:
```ruby
<https://www.python.org>
<email@example.com>
```
<div class="notice--info">
Автоматическая интерпретация URL-адресов . Некоторые процессоры Markdown автоматически преобразуют 
URL-адреса в ссылки даже без скобок. Если вы хотите обойти эту автоматизацию, поместите обратные 
кавычки (`) вокруг соответствующего URL-адреса, например `https://www.python.org`.
</div>

### Ссылки на почту
Вы можете вставить адреса электронной почты таким образом, чтобы они открывали окно
почтовой программы по умолчанию на вашем компьютере, когда вы нажимаете на предоставленную ссылку:
```ruby
[email@example.com](mailto:email@example.com)
```
### Изображени
Ссылка на изображение на вашем сервере:
```
![my_img](/assets/images/prev.jpg)
```
![my_img](/assets/images/prev.jpg)

Ссылка на изображение из сети:
```
![my_img](https://mddev.ru/assets/images/mikheevsergey.jpg)
```
![my_img](https://mddev.ru/assets/images/mikheevsergey.jpg)

Ссылка на изображение с альтернативным текстом:
```
![my_img](/assets/images/mikheevsergey.jpg) "I'm")
```
![my_img](/assets/images/mikheevsergey.jpg) "I'm")


Прикрепите подпись к изображению:
```
![my_img](/assets/images/prev.jpg) "I'm")This **is** *my caption* with a [link](https://www.python.org).
```
![my_img](/assets/images/prev.jpg) "I'm")This **is** *my caption* with a [link](https://www.python.org).

<div class="notice--info">
Информация : Описание в квадратных скобках ( [my_img]) — это всего лишь смысловое описание изображения.
Вы можете вставить любое описание (например, [My website logo]).
</div>

### Перекрестные ссылки
```ruby
Place an _anchor_ <a name="anchor"></a> here.
Clicking on this  [anchor](#anchor)-link will jump to our _anchor_.
```
Place an _anchor_ <a name="anchor"></a> here.
Clicking on this  [anchor](#anchor)-link will jump to our _anchor_.

### Ссылки на заголовки
Вы также можете ссылаться на заголовки напрямую, не размещая привязку :
```ruby
## My headline
Click on this  [link](#my-headline) to jump to "My headline".
```
## My headline
Click on this  [link](#my-headline) to jump to "My headline".

<div class="notice--info">
Привязки заголовков автоматически генерируются по следующему шаблону: ### My precious headline 1доступен 
через #-my-precious-headline-1. 
Вы также можете присвоить заголовкам собственную привязку , например:### My precious headline 1 {#my_id}
</div>

### Таблицы
```
| First Column | Second Column | Third Column         |  
| :----------- | :-----------: | -------------------: |  
|  row 1       |      data 1   | **propety 1**       |  
|  row 2       |      data 2   |  *property 2*        |
```

| First Column | Second Column | Third Column         |  
| :----------- | :-----------: | -------------------: |  
|  row 1       |      data 1   | **propety 1**       |  
|  row 2       |      data 2   |  *property 2*        |  


<div class="notice--info">
Ширина ячеек : хотя ширина ячеек может различаться в вашем документе 
Markdown, они будут автоматически отображаться с соответствующим интервалом между ячейками.
</div>

Выравнивание : поместив двоеточие :слева, справа или на обоих дефисах в строке заголовка, 
вы можете установить выравнивание текста каждого столбца по левому, правому или центру.

Описание таблицы : В некоторых процессорах Markdown вы можете добавить  `[table description]` право 
под таблицей. Вы даже можете ссылаться на таблицу через `[table description][table_reference]`(затем 
вы можете использовать внутритекстовую привязку `[#table_reference]` ).

Несколько строк : вы можете добавить несколько строк в ячейку, вставив тег HTML <br>, чтобы вызвать 
дополнительный разрыв строки.

Онлайн-генераторы таблиц , такие как tablegenerator.com, — это полезные инструменты, которые помогают создавать
(особенно огромные) таблицы.

### Использование HTML в ячейках Kramdown
С помощью kramdown ꜛ (например, используемого темой веб-сайтов Jekyll ) можно применять к ячейкам HTML-код, что 
обеспечивает дальнейшее форматирование внутри ячеек. Единственное, что вам нужно сделать, 
это обернуть HTML-код в это выражение: {::nomarkdown} HTML code... {:/}например:
```ruby
| First Column | Second Column | Third Column         |  
| :----------- | :-----------: | -------------------: |  
|  row 1       |      data 1   | {::nomarkdown}<ul><li>property 1.1</li><li>property 1.2</li></ul>{:/} |  
|  row 2       |      data 2   |  {::nomarkdown}<ul><li>property 2.1</li><li>property 2.2</li></ul>{:/} |
```

| First Column | Second Column | Third Column         |  
| :----------- | :-----------: | -------------------: |  
|  row 1       |      data 1   | {::nomarkdown}<ul><li>property 1.1</li><li>property 1.2</li></ul>{:/} |  
|  row 2       |      data 2   |  {::nomarkdown}<ul><li>property 2.1</li><li>property 2.2</li></ul>{:/} |   

### Отображение кода

Встроенный и однострочный код
```
\`This is some code\`
```
`This is some code`

**Сегменты многострочного кода**
Просто сделайте отступ для текста/кода на четыре пробела:
```
    This is a multi-line
    code segment.
```
    This is a multi-line
    code segment.

Подсветка синтаксиса

Вы также можете применить подсветку синтаксиса к изолированным блокам кода. Используйте ` вместо ':
```
'''python
import numpy as np
a=np.arange(5)
print(a+a)
'''
```
```python
import numpy as np
a=np.arange(5)
print(a+a)
```
### Цитаты
Следующие команды работают только в процессорах Markdown, поддерживающих MultiMarkdown:
```ruby
Let's cite a book[p. 99][#doebook] with some additional reference info.
Let's simply cite a book[][#doebook]. There is also a follow-up edition of that book[][#doebook2].

[#doebook]: Jane Doe, _My life as a placeholder_. Doe Press, 1898.
[#doebook2]: Jane Doe, _My life as a placeholder, Part 2_. Doe Press, 1902.
```

Let's cite a book[p. 99][#doebook] with some additional reference info.
Let's simply cite a book[][#doebook]. There is also a follow-up edition of that book[][#doebook2].


[#doebook]: Jane Doe, _My life as a placeholder_. Doe Press, 1898.
[#doebook2]: Jane Doe, _My life as a placeholder, Part 2_. Doe Press, 1902.


### Сноски
```ruby
Let's place a footnote here[^1].
[^1]: Some explanation text at the end of your document.
```

Let's place a footnote here[^1].
[^1]: Some explanation text at the end of your document.

### Глоссарий
```ruby
Let's place a link to a _glossary term_[^glossary] here.
[^glossary]:glossary: Glossary    Some explanation text at the end of your document to explain the _glossary term_.
```

Let's place a link to a _glossary term_[^glossary] here.
[^glossary]:glossary: Glossary    Some explanation text at the end of your document to explain the _glossary term_.


Некоторые процессоры Markdown также принимают следующий синтаксис:
```
This [?term1] has a glossary entry, as well as this this [?term2].

[?term1]: Definition of term 1.
[?term2]: Definition of term 2.
```

This [?term1] has a glossary entry, as well as this this [?term2].

[?term1]: Definition of term 1.
[?term2]: Definition of term 2.


<div class="notice--info">
Примечание.Функция глоссария может работать не во всех процессорах Markdown.
</div>

### Определения

Простые определения:
```
Lorem ipsum
:   Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```
Lorem ipsum
:   Lorem ipsum dolor sit amet, consectetur adipiscing elit.

Списки определений:
```
Lorem ipsum
:   1. Lorem ipsum dolor sit amet, consectetur adipiscing elit.
    2. Fusce et erat eget mauris semper aliquam in non nulla.
```
Lorem ipsum
:   1. Lorem ipsum dolor sit amet, consectetur adipiscing elit.
    2. Fusce et erat eget mauris semper aliquam in non nulla.

### Блоки цитат
```
> This is my first level quoting.
>> This is my second level quoting.

> This is my first level quoting with a citation.
<cite>Joan Doe</cite>
```
> This is my first level quoting.
>> This is my second level quoting.

> This is my first level quoting with a citation.
<cite>Joan Doe</cite>

<div class="notice--info">
Примечание. Эта <cite>команда может работать не для каждого процессора Markdown.
</cite>
</div>


### Экранирование
Если вы хотите использовать знак, который по умолчанию интерпретируется вашим процессором Markdown как синтаксис 
Markdown, поместите `\` перед ним обратную косую черту. 
Следующие знаки зарезервированы в качестве разметки Markdown по умолчанию:

```
\* - _ () . ! {} [] # `\
```
### Переменные
В некоторых процессорах Markdown вы можете определять 
переменные и использовать их как шаблонизатор повсюду в тексте:

```
my_var_1: dog
my_var_2: cat

My _[%my_var_2]_ is in love with my **[%my_var_1]**.
```
my_var_1: dog
my_var_2: cat

My _[%my_var_2]_ is in love with my **[%my_var_1]**.

### Споллеры
```
This is some visible text.
<details>
<summary>Toggle hidden text</summary>

<br>

This is some hidden text.

'''python
# you can even use it for code folding:
import matplotlib.pyplot as plt
import numpy as np
plt.plot(np.arange(5), np.arange(5))
'''
</details>
```

This is some visible text.
<details>
<summary>Toggle hidden text</summary>

<br>

This is some hidden text.

```python
# you can even use it for code folding:
import matplotlib.pyplot as plt
import numpy as np
plt.plot(np.arange(5), np.arange(5))
```
</details>


<div class="notice--info">
Примечание. Поместите пустую строку после закрывающего
</summary>тега, иначе текст Markdown будет отображаться неправильно. 
Также поместите пустую строку после закрывающего </details>тега.
</div>

Всё!:v:

