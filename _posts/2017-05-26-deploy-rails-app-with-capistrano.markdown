---
layout: post
title:  Deploy Rails app with Capistrano
date:   2017-05-26 15:05:55 +0300
image:  /assets/images/blog/post_1.png
author: Jacky
tags:   Rails, Deployment, Capistrano
---

There are many ways to automate deployments, from simple rsync bash scripts to complex containerized toolchains. Capistrano sits somewhere in the middle: it automates what you already know how to do manually with SSH, but in a repeatable, scalable fashion. There is no magic here!

#### Here's what makes Capistrano great:

- Strong conventions
Capistrano defines a standard deployment process that all Capistrano-enabled projects follow by default. You don't have to decide how to structure your scripts, where deployed files should be placed on the server, or how to perform common tasks: Capistrano has done this work for you.

- Multiple stages
Define your deployment once, and then easily parameterize it for multiple stages (environments), e.g. qa, staging, and production. No copy-and-paste necessary: you only need to specify what is different for each stage, like IP addresses.

- Parallel execution
Deploying to a fleet of app servers? Capistrano can run each deployment task concurrently across those servers and uses connection pooling for speed.

- Server roles
Your application may need many different types of servers: a database server, an app server, two web servers, and a job queue work server, for example. Capistrano lets you tag each server with one or more roles, so you can control what tasks are executed where.

- Community driven
Capistrano is easily extensible using the rubygems package manager. Deploying a Rails app? Wordpress? Laravel? Chances are, someone has already written Capistrano tasks for your framework of choice and has distributed it as a gem. Many Ruby projects also come with Capistrano tasks built-in.

- It's just SSH
Everything in Capistrano comes down to running SSH commands on remote servers. On the one hand, that makes Capistrano simple. On the other hand, if you aren't comfortable SSH-ing into a Linux box and doing stuff on the command-line, then Capistrano is probably not for you.

 
#### 1 - Install & setup the deployment script
To install Capistrano, all we need to add the gem to Gemfile

```ruby

  group :development do
    gem "capistrano", "~> 3.16", require: false
  end

```

Then we can run bundle to install the gem and run the install rake
```ruby

  bundle exec cap install

```

#### 2 - Essestional configs
We need to pay attention to some important configs to make sure it will run successfully for the first time deployment

```ruby

  server '<server_address>', user: "deploy", port: 22, roles: [:web, :app, :db], primary: true
  set :deploy_to, "/var/www/#{fetch(:application)}"

  set :repo_url, "git@bitbucket.org:miclabs/rails_app.git"
  set :branch, 'production'

  append :linked_files, "config/database.yml", "config/secrets.yml", 'config/application.yml', 'config/sidekiq.yml'
  append :linked_dirs, "log", "tmp/pids"

```

Next step, we can run the deploy command and wait for result

```ruby

  bundle exec cap deploy

```

Ref: [https://github.com/capistrano/capistrano](https://github.com/capistrano/capistrano)