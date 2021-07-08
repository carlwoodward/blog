---
title: Building out the Clojure Backend
layout: post
---

I've made 6 commits to _moodtracker_ since my last post. I must says it's been an interesting few days. It's my first time writing any real clojure code that I intend to run in some sort of production environment (in this case it will probably only be used by one person). The commits I've added are:

```
db95598 Add password encryption.
49fef59 Fix error in validation so users can be valid.
82657bc Add validations to create user.
88a83c7 Create user record with date time coercion.
6e214e3 Change registration to signup.
d63bd21 Add sign up to frontend.
```

## Database Cleaner

After briefly looking for a database cleaner, like the one used in Rails, I was sad to find that this was the first bit of framework code that I would need to write. It ended up being rather easy, taking only an hour or two to understand how to insert functions around tests.

In a test helper file there is a _clean-database_ function:

```clojure
(defn clean-database [test-function]
  (test-function)
  (println "DATABASE CLEANER: cleaning database")
  (apply #(exec-raw [(str "TRUNCATE TABLE " %)]) (all-tables)))
```

Adding a call to _use-fixtures_ allows the database cleaner to be called for each test.

```clojure
(use-fixtures :each clean-database)
```

Once this was in place the database was truncated on all tests. This isn't as fast as what Rails does (with its transaction wrapping) but I'd like to start with a simple solution first.

## Adding Timestamps

Coming from Rails, and liking a lot of the ideas that Rails has about doing things, adding timestamps to tables is a convention that I want to follow. In Rails, created-at and updated-at are used to store timestamps for a row.

The first pass of adding this in looks like:

```clojure
(defn run [attributes]
  (create-user-record (merge attributes {:created_at (time/now) :updated_at (time/now)})))
```

This is great, but sqlkorma doesn't know how to convert these types to sql. Below adds some generic code to handle time coercion but leaves room to add more types down the track.

```clojure
(defn sql-coorce-attributes [attributes]
  (let [coorce #(if (= (type %) org.joda.time.DateTime) (time-coerce/to-sql-time %) %)]
    (apply merge (map (fn [[field value]] {field (coorce value)}) attributes))))
```

And making sure it is called in the create function:

```clojure
(defn create-user-record [attributes]
  (insert users (values (records/sql-coorce-attributes attributes))))
```

At this point I started to feel really comfortable with composing functions of list operations together, destructuring hashes and using apply/merge to put the back together again.

## Encrypting Passwords

Making passwords turned out to be as easy as it is in Rails.

```clojure
(defn encrypt-password [attributes]
  (let [requested-password (:password attributes) salt (BCrypt/gensalt)]
    {:password_salt salt :password_hash (BCrypt/hashpw requested-password salt)}))
```

This function returns a hash that has the password salt and the password hash ready to be merged into the attibutes of the row.

## The good, the bad and the ugly

There are currently 275 lines of clojure in the project. I've still got one thing left to do for this component:

_Currently my test isn't working with nested data, e.g. {:user {:username "testuser"}}, I'd like to make it standard for the project that all data is nested like that from the JSON request._

But I'm getting really comfortable with making functions, putting them in a file and calling them from another file. I haven't worked in this manner for many years as I've been building object oriented programs. It's also really easy to see how a program can be made up of tiny functions that build upon the data structures that have been passed to them.

The power of clojure and lisp like languages comes from how easy it is to manipulate data structures in one line. A really good example of that form is in the timestamps code, where the attributes are taken, destructured, coerced, and punched back together like nothing ever happened. When most people do this in ruby, python or javascript it is a long winded function that has a lot of temporary variables and feels like it is driven through state, i.e. this hash has x value in it at this point of the loop. Clojure (like any lisp) strips all of that back.

The bad bits are that the community just isn't as strong as the ruby community. I found there wasn't anywhere near the level of organisation around documentation and a lot of the sites out there are lacking the design aesthetics that the ruby community (and the js community) have. For example compare the rubygems (and npm) site to the clojars site.

The projects also don't have the same traction, e.g. sql korma is a very prominant project in the clojure community. It works very well, is used in many projects and is over 2 years old (it is even talked about in multiple books) but it still isn't at 1.0 and probably won't be for a long time. I guess that is what you get when you are trying to use something that may be more interesting but harder for a lot of programmers to pick up.

## Still going to use it?

At this stage I'm not sure if it is going to be the language that I'm going to use on my next major project. Even though it feels great to code in, that might not be enough to take the shiny away from the competitors.
