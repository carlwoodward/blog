---
title: Multiple Backends
layout: post
---

There are many new languages and frameworks that are getting popular in the web app arena. Now that it is becoming easier to separate the backend from the frontend (using backbone, angular or ember), I thought it was time to evaluate the backend technologies from the basis of "which language do I prefer to use" to make API driven backend systems?

To figure this out I've decided to work on a project before christmas that is simple enough to be finished quickly but has enough depth to help influence my choices for upcoming projects. I came up with doing a simple moodtracker. Checkout the project at https://github.com/carlwoodward/moodtracker.

## Moodtracker

Is an app designed to be a test for different backend languages/frameworks.

The moodtracker is a simple web application that:

- Allows a user to sign up.
- Lets the user log in.
- Gives the user the ability to track their mood on a daily basis.
- Presents the user with a graph and activity timeline of their moods.

The front end is using Ember js handlebars for templating.

The user interface is using grunt as the build system.

## Multiple Backends

The main goal of the project is to see how developing backend application differs between the following languages/frameworks:

- Ruby/Sinatra
- Clojure/Compojure
- Go/Martini
- Elixir/Dynamo
- Node.js/Express

All backends rely on Postgresql for the database. Ruby (and/or Node.js) will be used as a glue language when I can't find some library that I think is required to build the app (e.g. database migrations).

I've already found that I had to build a simple database cleaner for the types of tests that I want to do in the clojure version. If the library takes to long to write then I'm happy to shell out to a script.

## Testing

Everything will be tested, in the hope that it can be an example of how testing differs between languages and frameworks.

## Tiered Architecture

- Router
- Controller
- Services
- Commands
- Models
- Records

This is a large architecture, particularly for a tiny app. I'm fine to skip tiers as needed as long as there is only one way coupling between tiers. My goal is to have an approach for complex applications that can be applied universally.
