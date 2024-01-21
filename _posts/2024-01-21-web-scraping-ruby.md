---
title: Парсинг веб-страниц с помощью Ruby
header:
  teaser: /assets/images/parse.jpg
  og_image: /assets/images/parse.jpg
category:
 - Ruby
tags:
 - Scraping
toc: true
toc_label: "Содержание"
toc_icon: "file-alt"
toc_sticky: true
---

Потребность в сборе данных со стороны компаний и частных лиц в последние годы возросла, и Ruby является одним из 
лучших языков программирования для этой цели. Парсинг веб-страниц в Ruby — это просто создание сценария, который 
может автоматически извлекать данные из Интернета, а затем вы можете использовать извлеченные данные по своему 
усмотрению.

В этом пошаговом руководстве вы узнаете, как выполнять парсинг веб-страниц с помощью Ruby, используя такие 
библиотеки, как Nokogiri и Selenium.

### Инициализация Ruby-проекта веб-скрапинга

Создайте папку для своего проекта Ruby, а затем войдите в нее с помощью команд ниже:
```bush
mkdir simple-web-scraper-ruby 
cd simple-web-scraper-ruby
```
Теперь создайте  scraper.rb файл и инициализируйте его следующим образом:
```bush
puts "Hello, World!"
```
В терминале выполните команду  ruby scraper.rb для запуска скрипта. Это должно напечатать:
```
"Hello, World!"
```
Обратите внимание, что он  scraper.rb будет содержать логику парсинга. Импортируйте  simple-web-scraper-ruby папку в свою Ruby IDE,
и теперь вы готовы применить на практике основы скрапинга веб данных с помощью Ruby!

### Как парсить сайт на Ruby
Давайте используем  ScrapeMe  в качестве целевого веб-сайта, а также нашего Ruby-паука для посещения каждой
страницы и получения данных о продукте. Целевой веб-сайт содержит только список элементов,
с покемонами, разбитых на несколько страниц.

![ScrapeMe](/assets/images/Products-–-ScrapeMe.png)

> Давайте установим несколько gem'ов "драгоценных камней" Ruby и начнем.

### Шаг 1. Установите HTTParty и Nokogiry.
Библиотека Net::HTTP  — это стандартный API-интерфейс HTTP-клиента для Ruby, и вы можете использовать его 
для выполнения HTTP-запросов. Но он не обеспечивает лучший синтаксис и может быть не лучшим вариантом для новичков. 
Поэтому лучшим выбором будет более удобный HTTP-клиент, например  HTTPParty .

HTTParty — это интуитивно понятный HTTP-клиент, который пытается сделать HTTP запросы более привлекательным занятием.
А учитывая, насколько важны эти запросы при скрапинге веб-страниц, HTTParty вам пригодится.

Установите HTTParty через gem httparty с помощью:
```
gem install httparty
```
Теперь вы можете легко выполнять HTTP-запросы для получения HTML-документов. Вам нужен только парсер HTML!
Nokogiri  упрощает работу с документами XML и HTML в Ruby.
Он предлагает мощный и простой в использовании API, который позволяет анализировать HTML-страницы, 
выбирать HTML-элементы и извлекать их данные.

Другими словами, Nokogiri помогает вам выполнять парсинг веб-страниц в Ruby. 

Вы можете установить его через gem nokogiri:
```
gem install nokogiri
```
Добавьте следующие строки в заголовок вашего scraper.rb файла:

```ruby
require "httparty" 
require "nokogiri"
```
Давайте продолжим и посмотрим, как использовать HTTParty и Nokogiri!

### Шаг 2. Загрузите целевую веб-страницу
Используйте HTTParty для выполнения HTTP  GET запроса для загрузки веб-страницы, которую вы хотите спарсить:

```ruby
# downloading the target web page 
response = HTTParty.get("https://scrapeme.live/shop/")
```

Метод HTTParty  get() выполняет запрос GET к URL-адресу, переданному в качестве параметра, и содержит
response.body HTML-документа, возвращаемый сервером в качестве ответа.

Ничего страшного, если на этом этапе вы получите ошибку, поскольку ошибка связана с тем, 
что некоторые веб-сайты блокируют HTTP-запросы в соответствии со своими заголовками. В частности, 
они запрещают запросы, которые не имеют допустимого  User-Agent заголовка, в рамках своих  технологий 
защиты от парсинга . Вы можете установить  User-Agent в HTTParty следующим образом:

```ruby
response = HTTParty.get("https://scrapeme.live/shop/", { 
	headers: { 
		"User-Agent" => "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36" 
	}, 
})
```
### Шаг 3. Анализ HTML-документа
Используйте Nokogiri для анализа HTML-документа, содержащегося в ответе response.body.

```ruby
# parsing the HTML document returned by the server 
document = Nokogiri::HTML(response.body)
```
Метод  `Nokogiri:HTML()` принимает строку HTML и возвращает документ Nokogiri, который имеет множество методов, 
которые предоставляют вам доступ ко всем функциям парсинга веб-страниц. Давайте посмотрим,
как использовать их для выбора элементов HTML на целевой странице.

### Шаг 4. Определите наиболее важные элементы HTML
Откройте DevTools F12 или наведите курсор на интересующий элемент и нажав правую кнопку мыши выбирете
исследовать элемент:

![DevTools](/assets/images/devtools.png)

Здесь вы можете заметить, что  li.product элемент HTML содержит:

HTML -  a элемент, содержащий URL-адрес продукта.
HTML -  img элемент, содержащий изображение продукта.
HTML  h2 -элемент, который содержит название продукта.
HTML -  span элемент, в котором хранится цена продукта.
Давайте спарсим данные из HTML-элементов продукта с помощью Ruby.

### Шаг 5. Извлеките данные из этих HTML-элементов.
Вам понадобится объект Ruby, в котором вы сначала сохраните спарсенные данные, и вы можете сделать это, 
создав класс PokemonProduct:
```ruby
# defining a data structure to store the scraped data 
PokemonProduct = Struct.new(:url, :image, :name, :price)
```
Struct позволяет объединить несколько атрибутов в одну структуру данных без написания нового класса с нуля. 
PokemonProduct имеет четыре атрибута, соответствующие данным, которые необходимо извлечь из каждого HTML-элемента
продукта.

Теперь продолжим и получим список всех элементов li.product:

```ruby
# selecting all HTML product elements 
html_products = document.css("li.product")
```
Благодаря  css() методу, представленному Нокогири, вы можете выбирать элементы HTML на основе селектора CSS. 
Здесь  css() применяется для получения всех HTML-элементов продукта.

Переберите список продуктов HTML и извлеките интересующие данные из каждого продукта следующим образом:

```ruby
# initializing the list of objects 
# that will contain the scraped data 
pokemon_products = [] 
 
# iterating over the list of HTML products 
html_products.each do |html_product| 
	# extracting the data of interest 
	# from the current product HTML element 
	url = html_product.css("a").first.attribute("href").value 
	image = html_product.css("img").first.attribute("src").value 
	name = html_product.css("h2").first.text 
	price = html_product.css("span").first.text 
 
	# storing the scraped data in a PokemonProduct object 
	pokemon_product = PokemonProduct.new(url, image, name, price) 
 
	# adding the PokemonProduct to the list of scraped objects 
	pokemon_products.push(pokemon_product) 
end
```
Вы только что узнали, как выполнять парсинг данных в Ruby. В приведенном выше фрагменте используется API 
веб-скрапинга Nokogiri, для извлечения интересующих данных из каждого HTML-элемента продукта. 
Затем он создает экзэмпляр класса PokemonProduct с этими данными и сохраняет его в списке продуктов.

< Пришло время преобразовать очищенные данные в более удобный формат.

### Шаг 6. Преобразование данных в CSV
Вы можете легко извлечь данные в CSV-файл следующим образом:

```ruby
# defining the header row of the CSV file 
csv_headers = ["url", "image", "name", "price"] 
CSV.open("output.csv", "wb", write_headers: true, headers: csv_headers) do |csv| 
	# adding each pokemon_product as a new row 
	# to the output CSV file 
	pokemon_products.each do |pokemon_product| 
		csv << pokemon_product 
	end 
end
```
<div class="notice--info">
Примечание
Библиотека  CSV является частью пакета ruby по умолчанию. Таким образом, вы можете работать
с CSV-файлами в Ruby без дополнительной библиотеки. Фрагмент кода инициализирует  output.csv файл со
строкой заголовка, затем заполняет CSV-файл данными, содержащимися в списке спарсенных продуктов.
</div>

Запустите scraper.rb скрипт Ruby для получения данных в своей IDE или с помощью команды ниже:
```
ruby scraper.rb
```
Когда сценарий завершится, вы найдете  output.csv файл в корневой папке вашего проекта Ruby.
Откройте его и вы увидите следующие данные:

![Result](/assets/images/result1.png)

Так держать :+1: Вы только что спарсили веб-страницу с помощью Ruby! :sunglasses:
