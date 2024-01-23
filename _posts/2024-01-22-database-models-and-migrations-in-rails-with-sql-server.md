---
title: "Модели баз данных и миграция в Rails 💎 с SQL Server"
category:
 - Ruby
tags:
 - SQL
header:
 teaser: /assets/images/r.jpg
 og_image: /assets/images/r.jpg
---
Ruby on Rails — это мощная платформа веб-приложений, предоставляющая удобный способ взаимодействия с базами данных. 
При работе с SQL Server в качестве системы управления базами данных очень важно понимать, как определять модели 
базы данных и управлять изменениями схемы с помощью миграции Rails. В этой статье мы рассмотрим процесс 
создания моделей баз данных и миграции в приложении Rails , используя SQL Server в качестве серверной 
части базы данных.

**Предварительные условия**
- Ruby on Rails установлен в вашей системе.
- Экземпляр SQL Server настроен и доступен.

### Создание нового приложения Rails
Начнем с создания нового приложения Rails. Откройте терминал и выполните следующую команду:
```
rails new sql_server_rails_app
```
Эта команда создаст новое приложение Rails с именем  sql_server_rails_app. Перейдите в каталог проекта:
```
cd sql_server_rails_app
```
Чтобы настроить SQL Server в качестве базы данных, откройте  config/database.yml файл и измените его следующим образом:
```
default: &default
  adapter: sqlserver
  host: localhost
  username: your_username
  password: your_password
  database: your_database_name
  port: 1433
```
Замените  your_username, your_password и your_database_name своими учетными данными SQL Server и желаемым именем
базы данных.

### Создание модели базы данных

Давайте создадим простую модель базы данных для приложения блога. Запустите следующую команду,
чтобы создать  Post модель с атрибутами:
```
rails generate model Post title:string body:text
```
Эта команда создаст файл миграции в  db/migrate каталоге и соответствующий файл модели в  app/models каталоге.

### Создание миграции

Откройте созданный файл миграции в  каталоге db/migrate. Он будет иметь имя типа  xxxxxx_create_posts.rb, где 
xxxxxx — временная метка. Добавьте в блок необходимые столбцы  create_table:

```ruby
class CreatePosts < ActiveRecord::Migration[6.1]
  def change
    create_table :posts do |t|
      t.string :title
      t.text :body
      t.timestamps
    end
  end
end
```
Эта миграция создает posts таблицу со столбцами title и  body .

### Запуск миграции
Чтобы применить миграцию и создать posts таблицу в базе данных SQL Server, выполните следующую команду:
```
rails db:migrate
```
Эта команда выполнит все ожидающие миграции и соответствующим образом обновит схему базы данных.

### Использование модели

Теперь, когда  Post модель и таблица созданы, вы можете использовать их в своем  приложении Rails . 
Например, вы можете создать новую запись в своем контроллере:

```ruby
class PostsController < ApplicationController
  def create
    @post = Post.new(post_params)
    if @post.save
      redirect_to @post, notice: 'Post was successfully created.'
    else
      render :new
    end
  end
  private
  def post_params
    params.require(:post).permit(:title, :body)
  end
end
```
Всё. Теперь вы можете начать создавать свое приложение, используя мощь и гибкость Rails, одновременно используя возможности SQL Server для хранения и извлечения данных.
