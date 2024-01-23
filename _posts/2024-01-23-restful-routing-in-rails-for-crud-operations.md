---
title: "RESTful маршрутизация в 💎 Rails для операций CRUD"
header:
 teaser: /assets/images/rest.jpg
 og_image: /assets/images/rest.jpg
category:
 - Ruby
---

Маршрутизация RESTful — это фундаментальная концепция Ruby on Rails, которая упрощает реализацию операций 
CRUD (создание, чтение, обновление, удаление) в веб-приложениях. В этой статье мы углубимся в маршрутизацию 
RESTful в Rails с практическими примерами кода, которые помогут вам понять и эффективно реализовать ее в своих
проектах.

## Понимание RESTful маршрутизации в Rails
Маршрутизация RESTful основана на идее, что веб-приложения должны следовать набору соглашений для обработки различных 
типов запросов. Эти соглашения сопоставляют глаголы HTTP (GET, POST, PUT, DELETE) с действиями контроллера и делают
поведение вашего приложения более предсказуемым и последовательным.

### 1. Создание ресурса
Начнем с создания простого ресурса, скажем, «статей».
```
rails generate scaffold Article title:string body:text
```
Эта команда создает новый ресурс, включая контроллер (ArticlesController) и представления для операций CRUD.

### 2. Индексировать и показывать действия
Действие index перечисляет все статьи, а действие show отображает конкретную статью.
```ruby
# app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
def index @articles = Article.all
end
def show
@article = Article.find(params[:id])
end
end
```
### 3. Новые и создающие действия
Новое действие отображает форму для создания новой статьи, а действие создания
обрабатывает отправку формы и создает новую запись в базе данных.

```ruby
# app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
 # …
def new
  @article = Article.new
end
def create
@article = Article.new(article_params)
if @article.save
  redirect_to @article
else
render ‘new’
 end
end
 private
def article_params
params.require(:article).permit(:title, :body)
 end
end
```
### 4. Редактировать и обновлять действия
Действие редактирования отображает форму для обновления существующей статьи,
а действие обновления обрабатывает отправку формы и обновляет запись статьи.

```ruby
# app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
  # …
  def edit
    @article = Article.find(params[:id])
  end
  def update
   @article = Article.find(params[:id])
    if @article.update(article_params)
      redirect_to @article
    else
      render ‘edit’
    end
  end
   # …
end
```
### 5. Действие «Уничтожить»
Действие уничтожить удаляет статью из базы данных.

```ruby
# app/controllers/articles_controller.rb
class ArticlesController < ApplicationController
  # …
  def destroy
    @article = Article.find(params[:id])
    @article.destroy
     redirect_to articles_path
  end
end
```
### 6. Конфигурация маршрутов
В вашем файле config/routes.rb Rails автоматически генерирует маршруты RESTful для вашего ресурса.
```ruby
# config/routes.rb
Rails.application.routes.draw do
  resources :articles
  # …
end
```

Благодаря этим маршрутам ваше приложение Rails теперь поддерживает все стандартные операции CRUD для статей.

## Заключение
Маршрутизация RESTful в Rails обеспечивает структурированный и эффективный способ обработки операций CRUD в 
ваших веб-приложениях. Следуя этим соглашениям и используя примеры кода, подобные приведенным в этой статье,
вы сможете быстро создавать мощные и удобные в обслуживании веб-приложения с помощью Ruby on Rails
