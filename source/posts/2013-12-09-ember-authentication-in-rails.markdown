---
title: Ember Authentication in Rails
layout: post
---

There are a bunch of examples out there for doing authentication. If you are looking for the ember side of authentication check out: http://jsbin.com/eQOZoGe/1/edit. The server code is the same as any other implementation except you will be using REST JSON API rather than rendering pages.

One thing that can be tricky is that most of the examples use a local storage variable to check whether the user is logged in. The problem is that the local storage variables last forever but the server side session lasts for a finite amount of time so when the user trys to perform an action, they are logged in on the client side but logged out on the server side.

## Authenticated Controller

Having an authenticated controller that renders a json response with a status of unauthorized (401) is a good way to communicate back to the ember app that the user needs to login again.

```ruby
class AuthenticatedController < ApplicationController
  before_filter :verify_user

  helper_method :current_user

  def current_user
    @current_user
  end

  protected

  def verify_user
    @current_user = User.find session[:user_id]
    unless @current_user
      render :json => {}, :status => :unauthorized
      false
    end
  end
end
```

## Make Ember redirect to Login

When the ember app sees any unauthorized request it needs to redirect to a login page. I put this code __app/assets/javascripts/appname.js.coffee__.

```coffeescript
Ember.$(document).ajaxError (event, jqxhr, settings, exception) ->
  if jqxhr.status is 401
    document.location.hash = "/login"
```

This code will be triggered whenever there is an ajax request that errors with an unauthorized response code and redirect the user back to /login. A fancier implementation would store the current browser location and then do the login and redirect back to that location when the user logs in successfully.
