---
title: Action Cable - Quick Start
layout: post
author: alameenkhader
author_email: alameenkhader@gmail.com
date: 2017-05-02 02:44:26 +0530
title_image: action-cable-quick-start.jpg
---

We have been using ajax polling whenever we needed Real Time updates. Its time to switch to WebSockets.
Action Cable is the major feature of Rails 5, you can easily work with websockets. This article demostrates the basic usage of ActionCable.

## Prerequisites

Rails 5.0 requires Ruby 2.2.2 or newer. Make sure you have installed the compatible ruby version.

    alameen@QB-TP-201:~$ ruby -v
    ruby 2.2.2p95 (2015-04-13 revision 50295) [x86_64-linux]

## Install Bundler

    alameen@QB-TP-201:~$ gem install bundler
    Fetching: bundler-1.14.6.gem (100%)
    Successfully installed bundler-1.14.6
    Parsing documentation for bundler-1.14.6
    Installing ri documentation for bundler-1.14.6
    Done installing documentation for bundler after 9 seconds
    1 gem installed

## Install Rails

    alameen@QB-TP-201:~$ gem install rails -v 5.1.0
    Fetching: rack-2.0.1.gem (100%)
    Successfully installed rack-2.0.1
    ................................
    ............................
    .....
    Installing ri documentation for rails-5.1.0
    Done installing documentation for actionpack, railties, websocket-driver, nio4r, actioncable, activejob, actionmailer, arel, activemodel, activerecord, rails after 29 seconds
    11 gems installed

## Create new Rails 5 application

    alameen@QB-TP-201:~$ rails new quick_start_action_cable
    create
    create  README.md
    create  Rakefile
    ......................
    .......
    ..
    Installing sass-rails 5.0.6
    Bundle complete! 16 Gemfile dependencies, 69 gems now installed.
    Use `bundle show [gemname]` to see where a bundled gem is installed.
             run  bundle exec spring binstub --all
    * bin/rake: spring inserted
    * bin/rails: spring inserted

When the new rails app is created, get into the new directory

    cd quick_start_action_cable

## Generate the controller and its views

    alameen@QB-TP-201:~/quick_start_action_cable$ rails g controller notifications index
    Running via Spring preloader in process 7947
          create  app/controllers/notifications_controller.rb
           route  get 'notifications/index'
           ..................
           ........
           .....
          create      app/assets/stylesheets/notifications.scss

  Now update your template `notifications/index.html` with the following markup

    <!-- app/views/notifications/index.html.erb -->
    <h1>Notifications#index</h1>

    <div id="notifications">
    </div>

  The empty div `#notifications` will get appended with new messages when a new notification is broadcasted.

## Adding the Notification Channel

    alameen@QB-TP-201:~/quick_start_action_cable$ rails generate channel Notification
    Running via Spring preloader in process 9008
          create  app/channels/notification_channel.rb
       identical  app/assets/javascripts/cable.js
          create  app/assets/javascripts/channels/notification.coffee

## Set up the channel - Server Side

To mount Action Cable to our application, add `mount ActionCable.server => '/cable'` to `config/routes.rb`

    Rails.application.routes.draw do
      get 'notifications/index'
      mount ActionCable.server => '/cable'
    end

Add `stream_from "notifications_channel"` to the method `subscribed` of `app/channels/notification_channel.rb`

    # app/channels/notification_channel.rb
    class NotificationChannel < ApplicationCable::Channel
      def subscribed
        stream_from "notification_channel"
      end

      def unsubscribed
        # Any cleanup needed when channel is unsubscribed
      end
    end

Add a create action to the NotificationsController, broadcast the message to the channel and skip the `verify_authentication_token`

    # app/controllers/notifications_controller.rb
    class NotificationsController < ApplicationController
      skip_before_action :verify_authenticity_token

      def index
      end

      def create
        ActionCable.server.broadcast 'notification_channel', message: params[:message]
        render text: 'success'
      end
    end

Update our `config/routes.rb`

    Rails.application.routes.draw do
      resources :notifications, only: %i(index create)

      mount ActionCable.server => '/cable'
    end


## Set up the channel - Client Side

Handle the recieved event

    # app/assets/javascripts/channels/notification.coffee

    App.notification = App.cable.subscriptions.create "NotificationChannel",
      connected: ->
        console.log('connected');
        # Called when the subscription is ready for use on the server

      disconnected: ->
        # Called when the subscription has been terminated by the server

      received: (data) ->
        node = document.createElement('p')
        textnode = document.createTextNode(data.message)
        node.appendChild textnode
        document.getElementById('notifications').appendChild node

Start the server, open in your browser and navigate to `/notifications`
Now trigger a notification from your console

    curl -X POST --data "message=Hello there" http://localhost:3000/notifications

Run the curl command again with another message and see the messages gets appended in real time.
