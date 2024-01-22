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

## Продвинутый парсинг веб-страниц с Ruby

Поскольку целевой веб-сайт включает в себя несколько веб-страниц, давайте просканируем все страницы целевого веб-сайта, перейдя по всем ссылкам на страницы. Для этого щелкните правой кнопкой мыши HTML-элемент номера страницы и выберите «Просмотреть»:

![Number of page](/assets/images/pnum.png)

Chrome автоматически выделит HTML-элемент, по которому вы щелкнули правой кнопкой мыши. Обратите внимание, 
что вы можете выбрать все элементы нумерации страниц с помощью  a.page-numbers селектора CSS. Продолжайте и извлеките все ссылки на страницы с помощью Nokogiri:

```ruby
# extracting the list of URLs from 
# the pagination elements 
pagination_links = document 
					.css("a.page-numbers") 
					.map{ |a| a.attribute("href") }
```
Этот фрагмент возвращает список URL-адресов, извлеченных по  href атрибуту каждого HTML-элемента нумерации страниц.

Чтобы спарсить все страницы веб-сайта, вам нужно написать некоторую логику сканирования. Вам понадобятся некоторые структуры данных, чтобы отслеживать посещенные страницы и избегать повторного парсинга страницы, а также переменную,  limit чтобы ваш парсер не посещал слишком много страниц:

```ruby
# initializing the list of pages to scrape with the 
# pagination URL associated with the first page 
pages_to_scrape = ["https://scrapeme.live/shop/page/1/"] 
 
# initializing the list of pages discovered 
# with a copy of pages_to_scrape 
pages_discovered = ["https://scrapeme.live/shop/page/1/"] 
 
# current iteration 
i = 0 
# max pages to scrape 
limit = 5 
 
# iterate until there is still a page to scrape 
# or the limit is reached 
while pages_to_scrape.length != 0 && i < limit do 
	# getting the current page to scrape and removing it from the list 
	page_to_scrape = pages_to_scrape.pop 
 
	# retrieving the current page to scrape 
	response = HTTParty.get(page_to_scrape, { 
		headers: { 
			"User-Agent" => "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36" 
		}, 
	}) 
 
	# parsing the HTML document returned by the server 
	document = Nokogiri::HTML(response.body) 
 
	# extracting the list of URLs from the pagination elements 
	pagination_links = document 
						.css("a.page-numbers") 
						.map{ |a| a.attribute("href") } 
 
	# iterating over the list of pagination links 
	pagination_links.each do |new_pagination_link| 
		# if the web page discovered is new and should be scraped 
		if !(pages_discovered.include? new_pagination_link) && !(pages_to_scrape.include? new_pagination_link) 
			pages_to_scrape.push(new_pagination_link) 
		end 
 
		# discovering new pages 
		pages_discovered.push(new_pagination_link) 
	end 
 
	# removing the duplicated elements 
	pages_discovered = pages_discovered.to_set.to_a 
 
	# scraping logic...

	# incrementing the iteration counter 
	i = i + 1 
end 

# exporting to CSV...
```
Этот парсер данных анализирует веб-страницу, ищет новые ссылки, добавляет их в очередь сканирования и собирает данные с текущей страницы. Затем он повторяет эту логику для каждой страницы.

Если вы установите для переменной limit значение 48, скрипт посетит и pages_discovered сохранит все 48 URL-страниц. В результате  output.csv будут содержаться данные обо всех 755 продуктах, с покемонами.

### Весь код
Вот как выглядит весь парсер данных Ruby:

```ruby
require "httparty" 
require "nokogiri" 
 
# defining a data structure to store the scraped data 
PokemonProduct = Struct.new(:url, :image, :name, :price) 
 
# initializing the list of objects 
# that will contain the scraped data 
pokemon_products = [] 
 
# initializing the list of pages to scrape with the 
# pagination URL associated with the first page 
pages_to_scrape = ["https://scrapeme.live/shop/page/1/"] 
 
# initializing the list of pages discovered 
# with a copy of pages_to_scrape 
pages_discovered = ["https://scrapeme.live/shop/page/1/"] 
 
# current iteration 
i = 0 
# max pages to scrape 
limit = 5 
 
# iterate until there is still a page to scrape 
# or the limit is reached 
while pages_to_scrape.length != 0 && i < limit do 
	# getting the current page to scrape and removing it from the list 
	page_to_scrape = pages_to_scrape.pop 
 
	# retrieving the current page to scrape 
	response = HTTParty.get(page_to_scrape, { 
		headers: { 
			"User-Agent" => "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36" 
		}, 
	}) 
 
	# parsing the HTML document returned by the server 
	document = Nokogiri::HTML(response.body) 
 
	# extracting the list of URLs from the pagination elements 
	pagination_links = document 
						.css("a.page-numbers") 
						.map{ |a| a.attribute("href") } 
 
	# iterating over the list of pagination links 
	pagination_links.each do |new_pagination_link| 
		# if the web page discovered is new and should be scraped 
		if !(pages_discovered.include? new_pagination_link) && !(pages_to_scrape.include? new_pagination_link) 
			pages_to_scrape.push(new_pagination_link) 
		end 
 
		# discovering new pages 
		pages_discovered.push(new_pagination_link) 
	end 
 
	# removing the duplicated elements 
	pages_discovered = pages_discovered.to_set.to_a 
 
	# selecting all HTML product elements 
	html_products = document.css("li.product") 
 
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
 
	# incrementing the iteration counter 
	i = i + 1 
end 
 
# defining the header row of the CSV file 
csv_headers = ["url", "image", "name", "price"] 
CSV.open("output.csv", "wb", write_headers: true, headers: csv_headers) do |csv| 
	# adding each pokemon_product as a new row to the output CSV file 
	pokemon_products.each do |pokemon_product| 
		csv << pokemon_product 
	end 
end
```
**Продолжим**
Давайте добавим еще один gem:
```
gem install parallel
```
И импортируйте его, добавив эту строку в ваш файл Ruby:
```
require "parallel"
```
Теперь вы можете получить доступ к нескольким служебным функциям для выполнения параллельных вычислений в Ruby.

Теперь у вас есть список веб-страниц для парсинга, хранящийся в массиве:
```ruby
pages_to_scrape = [ 
	"https://scrapeme.live/shop/page/1/", 
	"https://scrapeme.live/shop/page/2/", 
	# ... 
	"https://scrapeme.live/shop/page/48/" 
]
```
Следующим шагом будет создание параллельного веб-парсера с помощью Ruby. Для этого сначала создайте экземпляр,  Mutex чтобы реализовать семафор для координации доступа к общим данным из нескольких параллельных потоков. Он вам понадобится, потому что массивы в Ruby не являются потокобезопасными. Затем используйте  map() метод, предоставляемый  Parallelin_threads , для  одновременного  выполнения параллельного парсинга на страницах.

```ruby
# initializing a semaphore 
semaphore = Mutex.new 
 
Parallel.map(pages_to_scrape, in_threads: 4) do |page_to_scrape| 
	# retrieving the current page to scrape 
	response = HTTParty.get(page_to_scrape, { 
		headers: { 
			"User-Agent" => "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36" 
		}, 
	}) 
	 
	# parsing the HTML document returned by server 
	document = Nokogiri::HTML(response.body) 
	 
	# scraping logic... 
	 
	# since arrays are not thread-safe in Ruby 
	semaphore.synchronize { 
		# adding the PokemonProduct to the list of scraped objects 
		pokemon_products.push(pokemon_product) 
	} 
end
```
Теперь вы знаете, как сделать парсер веб-страниц на Ruby молниеносным! 

Вот весь код:
```ruby
require "httparty" 
require "nokogiri" 
require "parallel" 
 
# defining a data structure to store the scraped data 
PokemonProduct = Struct.new(:url, :image, :name, :price) 
 
# initializing the list of objects 
# that will contain the scraped data 
pokemon_products = [] 
 
# initializing the list of pages to scrape 
pages_to_scrape = [ 
	"https://scrapeme.live/shop/page/2/", 
	"https://scrapeme.live/shop/page/3/", 
	"https://scrapeme.live/shop/page/4/", 
	"https://scrapeme.live/shop/page/5/", 
	"https://scrapeme.live/shop/page/6/", 
	# ... 
	"https://scrapeme.live/shop/page/48/" 
] 
 
# initializing a semaphore 
semaphore = Mutex.new 
 
Parallel.map(pages_to_scrape, in_threads: 4) do |page_to_scrape| 
	# retrieving the current page to scrape 
	response = HTTParty.get(page_to_scrape, { 
		headers: { 
			"User-Agent" => "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36" 
		}, 
	}) 
 
	# parsing the HTML document returned by server 
	document = Nokogiri::HTML(response.body) 
 
	# selecting all HTML product elements 
	html_products = document.css("li.product") 
 
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
 
		# since arrays are not thread-safe in Ruby 
		semaphore.synchronize { 
			# adding the PokemonProduct to the list of scraped objects 
			pokemon_products.push(pokemon_product) 
		} 
	end 
end 
 
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
### Парсинг веб-сайтов с динамическим контентом

Многие веб-сайты используют JavaScript для выполнения HTTP-запросов через AJAX для асинхронного получения данных. Затем они могут использовать эти данные для соответствующего обновления DOM и, аналогичным образом, они могут использовать JavaScript для динамического управления DOM.

В этом случае HTML-документ, возвращаемый сервером, может не включать все интересующие данные. Если вы хотите парсить веб-сайты с динамическим контентом, вам нужен инструмент, который может запускать JavaScript, например, headless браузер.

Headless  браузер  — это технология, которая позволяет загружать веб-страницы в браузере без графического интерфейса. Одной из наиболее надежных библиотек Ruby, обеспечивающих функциональность headless-браузера, является  привязка  Ruby для Selenium .

Чтобы использовать его для парсинга динамической веб-страницы, установите  selenium-webdriver gem Selenium в Ruby с помощью:
```
gem install selenium-webdriver
```
После установки Selenium запустите парсер Ruby, чтобы получить данные с сайта ScrapeMe:
```ruby
require "selenium-webdriver" 
 
# defining a data structure to store the scraped data 
PokemonProduct = Struct.new(:url, :image, :name, :price) 
 
# initializing the list of objects 
# that will contain the scraped data 
pokemon_products = [] 
 
# configuring Chrome to run in headless mode 
options = Selenium::WebDriver::Chrome::Options.new 
options.add_argument("--headless") 
 
# initializing the Selenium Web Driver for Chrome 
driver = Selenium::WebDriver.for :chrome, options: options 
 
# visiting a web page in the browser opened 
# by Selenium behind the scene 
driver.navigate.to "https://scrapeme.live/shop/" 
 
# selecting all HTML product elements 
html_products = driver.find_elements(:css, "li.product") 
 
# iterating over the list of HTML products 
html_products.each do |html_product| 
	# extracting the data of interest 
	# from the current product HTML element 
	url = html_product.find_element(:css, "a").attribute("href") 
	image = html_product.find_element(:css, "img").attribute("src") 
	name = html_product.find_element(:css, "h2").text 
	price = html_product.find_element(:css, "span").text 
 
	# storing the scraped data in a PokemonProduct object 
	pokemon_product = PokemonProduct.new(url, image, name, price) 
 
	# adding the PokemonProduct to the list of scraped objects 
	pokemon_products.push(pokemon_product) 
end 
 
# closing the driver 
driver.quit 
 
# exporting logic
```
Selenium позволяет выбирать HTML-элементы с помощью метода find_elements(). При вызове  find_element() для HTML-элемента Selenium выполняется поиск HTML узлов и его дочерних элементов. Затем с помощью таких методов, как  attribute() и text(), вы можете извлекать данные из узлов HTML.

Такой подход к парсингу веб-страниц в Ruby устраняет необходимость в HTTParty и Nokogiri, поскольку Selenium использует браузер для выполнения запроса  GET и отображения результирующего HTML-документа. Таким образом, вы можете напрямую посетить новую веб-страницу в Selenium с помощью:
```ruby
# selecting a pagination element 
pagination_element = driver.find_element(:css, "a.page-numbers") 
 
# visiting to a new page 
# directy in the browser 
paginationElement.click 
 
# waiting for the web page to load... 
 
puts driver$title # prints "Products – Page 2 – ScrapeMe"
```
Когда вы вызываете метод click, Selenium откроет новую страницу в headless-браузере, позволяя вам выполнять парсинг веб-страниц, как это сделал бы человек. Это позволяет легко выполнять  парсинг веб-страниц без блокировок .
### Другие библиотеки веб-скрапинга на Ruby

Другие полезные библиотеки для парсинга веб-страниц с помощью Ruby:

- **ZenRows:** API для парсинга веб-страниц, который может легко извлекать данные с веб-страниц и автоматически обходить любую систему защиты от ботов или парсинга. ZenRows также предлагает автономные браузеры, ротацию прокси-серверов и гарантию безотказной работы в течение 99%.
- **OpenURI:** gem Ruby, который содержит библиотеки для обработки Net::HTTP  для упрощения использования. С OpenURI вы можете легко выполнять HTTP-запросы.
- **Kimurai:** современная Ruby-инфраструктура с открытым исходным кодом для парсинга данных, которая работает с headless браузерами, такими как Chromium, Headless Firefox и PhantomJS, и позволяет вам взаимодействовать с веб-сайтами, требующими JavaScript. Он также поддерживает простые HTTP-запросы для веб-сайтов со статическим контентом.
- **Watir:** библиотека Ruby с открытым исходным кодом для выполнения автоматического тестирования. Watir позволяет вам инструктировать браузер и предлагает функции headless браузера.
- **Capybara:** библиотека Ruby высокого уровня для создания тестов для веб-приложений. Capybara не зависит от веб-драйверов и поддерживает Rack::Test и Selenium.

ВСЁ! :wave:

