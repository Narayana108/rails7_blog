# Ruby on rails 7 Blog
## Stack

* ruby 3
* rails 7
* bootstrap 5
* sqlite 3

## System dependencies
Get the latest rable version of ruby with `rbenv`
* ruby 3.1.2
* Rails 7.0.2.4

## Start the blog
```ruby
rails db:migrate
rails db:seed       # Optional, populates the db with data
bundle install
rails s
```

# Blog creation tutorial
## Setup the project - Phase 1
*This is a high level overview of the steps taken to create the blog*


* Create project
```
rails new rails7_blog
```

- Install dependencies from Gemfile

```
bundle install
```

- Generate view, controller and route

```
rails g controller pages home about
```

- Run servers

```
rails s
```

- Add bootstrap 5
- Edit routes and set root_path
- Edit and link home and about page
  Use rails `link_to` instead of html's href to link pages
- Add a navbar `_navbar.html.erb` from bootstrap 5 and edit it

## Create blog posts - Phase 2
- Generate scaffold (Generates all the things)
```
rails g scaffold post title:string body:text
```

- Create tables in db
```
rails db:migrate
```

- Rails console
```
rails c
```

### Rails console commands
Create and view posts from the console
* Create a post from a variable
```ruby
irb(main):007:0> @post = Post.new(title: "Hello World", body: "This is my first post")
=> #<Post:0x00007f42c62372f0 id: nil, title: "Hello World", body: "This is my first post", created_at: nil, updated_at: nil>

irb(main):008:0> @post.save
  TRANSACTION (0.1ms)  begin transaction
  Post Create (0.2ms)  INSERT INTO "posts" ("title", "body", "created_at", "updated_at") VALUES (?, ?, ?, ?)  [["title", "Hello World"], ["body", "This is my first post"], ["created_at", "2022-05-03 06:55:43.057983"], ["updated_at", "2022-05-03 06:55:43.057983"]]
```

* Create post directly
```ruby
irb(main):006:0> Post.create(title: "My Second Post", body: "This is my second post")
  TRANSACTION (0.1ms)  begin transaction
  Post Create (0.2ms)  INSERT INTO "posts" ("title", "body", "created_at", "updated_at") VALUES (?, ?, ?, ?)  [["title", "My Second Post"], ["body", "This is my second post"], ["created_at", "2022-05-03 06:53:24.317323"], ["updated_at", "2022-05-03 06:53:24.317323"]]
```

Get post with id of 1(first post)
```ruby
irb(main):009:0> @post = Post.find(1)
  Post Load (0.1ms)  SELECT "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT ?  [["id", 1], ["LIMIT", 1]]
=> #<Post:0x00007f42c6956978 id: 1, title: "Hello World", body: "This is my first post", created_at: Tue, 03 May 2022 06:51:56.111030000 UTC +00:00, updated_at: Tue, 03 May 2022 06:51:56.111030000 UTC +00:00>

irb(main):010:0> @post.title
=> "Hello World"
```

Get first post
```ruby
irb(main):011:0> @post = Post.first
  Post Load (0.1ms)  SELECT "posts".* FROM "posts" ORDER BY "posts"."id" ASC LIMIT ?  [["LIMIT", 1]]
=> #<Post:0x00007f42c51baad0 id: 1, title: "Hello World", body: "This is my first post", created_at: Tue, 03 May 2022 06:51:56.111030000 UTC +00:00, updated_at: Tue, 03 May 2022 06:51:56.111030000 UTC +00:00>

irb(main):012:0> @post.title
=> "Hello World"
```

Get post with id of 2(second post)
```ruby
irb(main):015:0> @post = Post.last
  Post Load (0.2ms)  SELECT "posts".* FROM "posts" ORDER BY "posts"."id" DESC LIMIT ?  [["LIMIT", 1]]
=> #<Post:0x00007f42c51dd760 id: 3, title: "Hello World", body: "This is my first post", created_at: Tue, 03 May 2022 06:55:43.057983000 UTC +00:00, updated_at: Tue, 03 May 2022 06:55:43.057983000 UTC +00:00>

irb(main):016:0> @post.title
=> "Hello World"
```

Get last post
```ruby
@post = Post.last(2)
  Post Load (0.1ms)  SELECT "posts".* FROM "posts" ORDER BY "posts"."id" DESC LIMIT ?  [["LIMIT", 2]]
=> [#<Post:0x00007f42c524d718 id: 2, title: "My Second Post", body: "This is my second post", created_at: Tue, 03 May 2022 06:53:24.317323000 UTC +00:00, updated_at: Tue, 03 May 2022 06:53:24.317323000 UTC +...

irb(main):021:0> @post
=>
[#<Post:0x00007f42c524d718 id: 2, title: "My Second Post", body: "This is my second post", created_at: Tue, 03 May 2022 06:53:24.317323000 UTC +00:00, updated_at: Tue, 03 May 2022 06:53:24.317323000 UTC +00:00>,
 #<Post:0x00007f42c524d7e0 id: 3, title: "Hello World", body: "This is my first post", created_at: Tue, 03 May 2022 06:55:43.057983000 UTC +00:00, updated_at: Tue, 03 May 2022 06:55:43.057983000 UTC +00:00>]

```

* To exit the console press `ctrl + d` or type `exit`

* Link posts in the navbar
* Make posts pages and sub pages look prettier
* Add post validation in `./app/models/post.rb`

* Autogenerate Database data
Add `Post.create` in a loop and save it in `./db/seeds.rb`

```ruby
rails db:drop       # Drop/delete db
rails db:migrate    # Create database and tables
rails db:seed       # Populate db with data
```



# Otherthings to add

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions