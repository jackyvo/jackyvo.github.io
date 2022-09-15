---
layout: post
title:  Top Gems to speed up development progress
date:   2022-05-26 15:05:55 +0300
image:  /assets/images/blog/post_3.png
author: Jacky
tags:   Rails, Gems 
---

Ruby on Rails (RoR) is a server-side application framework that is written in Ruby under MIT License.  Rails is a model-view-controller (MVC) framework that provides default arrangements for a web service, database, and web service.  It reassures and simplifies the usage of web standards, such as XML or JSON for the data transfer and CSS, JavaScript, and HTML for user interfacing.

In addition to the MVC pattern, Rails accentuates the employment of other popular software engineering designs and paradigms, comprising active record pattern, don’t repeat yourself (DRY), and convention over configuration (CoC).  Shopify, GitHub, Netflix, Hulu, Airbnb, and Groupon are some of the popular companies that use Ruby on Rails. 


#### 1. Figaro 
Simple, Heroku-friendly Rails app configuration using ENV and a single YAML file.

Figaro supports loading ENV variables for each environment mode. You should add application.yml to .gitignore for private sharing

 

#### 2. Letter Opener 
Letter Opener helps to send and track the sending email in development mode. When the email is sent, it will open the window in the current browser for opening the email content. It's simple to set up with this gem as well

```ruby

  config.action_mailer.delivery_method = :letter_opener
  config.action_mailer.perform_deliveries = true

```
 

#### 3. Pry
Pry helps the developer to easily debug the working flow of the current Rails app, therefore help us to speed up the progress of debugging and find out the problem issues. We need to be familiar with this gem when working on any Rails project

This gem permits its developers to make the breakpoints and device a code debugging gradually.  Pry has an exclusive collection of traits, which comprises runtime invocation, syntax highlighting, exotic object support, command shell integration, flexible and influential command scheme

 
#### 4. Devise
Devise is the gem that you can easily meet in any Rails projects, not only small but also with large-scale system

Devise gem is one of the best ruby on rails gems of 2019.  It makes the work easy and operative.  Devise take account of 10 modules, namely, Database Authenticatable, Omniauthable, Confirmable, Registrable, Trackable, Lockable, Recoverable, Rememberable, Timeoutable, Validatable, and FriendlyId.  The resource URLs are effortlessly recognized by the main key (database ID) of every module

 

#### 5. Kaminari
It's a good gem for paginating, with simple code like .page and .per, no need to do extra setup after installing

With approximately five million downloads, Kaminari gets the top position in the list of most standard Rails Gems.  You can paginate everything by employing this gem.  Such pagination can be executed from ActiveRecord imports to simpler arrays by utilizing an easy-to-use scope-based application programming interface (API)

 

Other helpful gems from Awesome Ruby [https://awesome-ruby.com/](https://awesome-ruby.com/)

Jacky