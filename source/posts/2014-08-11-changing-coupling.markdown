---
title: Orchestration Focused Design
layout: post
---

Recently I've started worshipping the Crossfit cult. A lot of people in Crossfit take to social media to share their involvement with the sport. Coming from the programming world it was easy to start following Crossfit people on Instragram and Facebook but I didn't want to invest the time of:

- Finding all the right people to follow; and
- Having to check 2 - 3 feeds for Crossfit news.

For a weekend project I made [thechipper.io](http://thechipper.io). This project grabs all of the top Crossfit feeds and puts them in one place.

<video width="666" height="324" autoplay loop>
  <source src="http://cl.ly/1v2y1F241x0j/download/thechipper.mp4" type="video/mp4">
</video>

This post is about coupling not Crossfit. Starting with the architecture of the project.


<svg xmlns="http://www.w3.org/2000/svg" xmlns:xl="http://www.w3.org/1999/xlink" version="1.1" viewBox="35 51 489 148" width="489pt" height="148pt"><metadata xmlns:dc="http://purl.org/dc/elements/1.1/"><dc:date>2014-08-10 22:20Z</dc:date><!-- Produced by OmniGraffle Professional 5.4.4 --></metadata><defs><font-face font-family="Helvetica" font-size="12" units-per-em="1000" underline-position="-75.683594" underline-thickness="49.316406" slope="0" x-height="532.22656" cap-height="719.72656" ascent="770.01953" descent="-229.98047" font-weight="bold"><font-face-src><font-face-name name="Helvetica-Bold"/></font-face-src></font-face></defs><g stroke="none" stroke-opacity="1" stroke-dasharray="none" fill="none" fill-opacity="1"><title>Canvas 3</title><g><title>Layer 1</title><path d="M 208.09856 51 L 351.17699 51 C 353.93841 51 356.17699 53.238576 356.17699 56 L 356.17699 72.117647 C 356.17699 74.87907 353.93841 77.117647 351.17699 77.117647 L 208.09856 77.117647 C 205.33714 77.117647 203.09856 74.87907 203.09856 72.117647 L 203.09856 56 C 203.09856 53.238576 205.33714 51 208.09856 51 Z" fill="#1d73c5"/><text transform="translate(208.09856 57.058824)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="12.2042534" y="11" textLength="118.66992">Angular JS Frontend</tspan></text><path d="M 208.09856 91.62745 L 351.17699 91.62745 C 353.93841 91.62745 356.17699 93.86603 356.17699 96.62745 L 356.17699 112.7451 C 356.17699 115.50652 353.93841 117.7451 351.17699 117.7451 L 208.09856 117.7451 C 205.33714 117.7451 203.09856 115.50652 203.09856 112.7451 L 203.09856 96.62745 C 203.09856 93.86603 205.33714 91.62745 208.09856 91.62745 Z" fill="#1d73c5"/><text transform="translate(208.09856 97.686275)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="51.198394" y="11" textLength="40.68164">Sinatra</tspan></text><line x1="279.7906" y1="77.117647" x2="279.9604" y2="91.62745" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 208.09856 132.2549 L 351.17699 132.2549 C 353.93841 132.2549 356.17699 134.49348 356.17699 137.2549 L 356.17699 153.37255 C 356.17699 156.13397 353.93841 158.37255 351.17699 158.37255 L 208.09856 158.37255 C 205.33714 158.37255 203.09856 156.13397 203.09856 153.37255 L 203.09856 137.2549 C 203.09856 134.49348 205.33714 132.2549 208.09856 132.2549 Z" fill="#1d73c5"/><text transform="translate(208.09856 138.313725)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="51.866363" y="11" textLength="39.345703">Sequel</tspan></text><line x1="279.7906" y1="117.7451" x2="279.9604" y2="132.2549" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 208.09856 172.88235 L 351.17699 172.88235 C 353.93841 172.88235 356.17699 175.12093 356.17699 177.88235 L 356.17699 194 C 356.17699 196.76142 353.93841 199 351.17699 199 L 208.09856 199 C 205.33714 199 203.09856 196.76142 203.09856 194 L 203.09856 177.88235 C 203.09856 175.12093 205.33714 172.88235 208.09856 172.88235 Z" fill="#1d73c5"/><text transform="translate(208.09856 178.94118)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="44.85855" y="11" textLength="53.361328">Database</tspan></text><line x1="279.63778" y1="158.37255" x2="279.63778" y2="172.88235" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 40.810194 91.62745 L 183.88862 91.62745 C 186.65005 91.62745 188.88862 93.86603 188.88862 96.62745 L 188.88862 112.7451 C 188.88862 115.50652 186.65005 117.7451 183.88862 117.7451 L 40.810194 117.7451 C 38.04877 117.7451 35.810194 115.50652 35.810194 112.7451 L 35.810194 96.62745 C 35.810194 93.86603 38.04877 91.62745 40.810194 91.62745 Z" fill="#1d73c5"/><text transform="translate(40.810194 97.686275)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="25.194488" y="11" textLength="92.689453">Fetch Instagram</tspan></text><path d="M 375.38692 91.62745 L 518.46535 91.62745 C 521.22677 91.62745 523.46535 93.86603 523.46535 96.62745 L 523.46535 112.7451 C 523.46535 115.50652 521.22677 117.7451 518.46535 117.7451 L 375.38692 117.7451 C 372.6255 117.7451 370.38692 115.50652 370.38692 112.7451 L 370.38692 96.62745 C 370.38692 93.86603 372.6255 91.62745 375.38692 91.62745 Z" fill="#1d73c5"/><text transform="translate(375.38692 97.686275)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="25.862457" y="11" textLength="91.353516">Fetch Facebook</tspan></text><line x1="393.68797" y1="117.7451" x2="334.53446" y2="132.2549" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><line x1="166.06168" y1="117.7451" x2="225.74199" y2="132.2549" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/></g></g></svg>

This is a standard architecture for an application of this type but the rules for the design aren't:

1. All data objects are structs without any extra methods.
2. All database models are dumb transaction processors, nothing more.
3. Logic to be held in services.
4. Services are to be stateless.
5. State is to be held in main loops and external interfaces.

The patterns here are very familiar after writing code in Elixir or other functional languages.

The experiment here is __if you code with these goals in mind and extract any object oriented-ness out to an adapter setting (for external interfaces only) do you end up writing code that is easier to reason about and maintain?__

Serving posts is the simplest slice of code to breakdown:

```ruby
class Server < Sinatra::Base
  get "/posts.json" do
    page = (params[:page] || 1).to_i
    PostService.all_posts(page).to_json
  end
end

module PostService
  class << self
    def all_posts(page)
      total = Post.order(Sequel.desc(:created_at)).count
      posts = Post.order(Sequel.desc(:created_at)).paginate(page, 40).all
      PostRequest.new total: total, posts: posts, :page => page
    end
  end
end

class Source < Sequel::Model; end
class Post < Sequel::Model; end

class PostRequest < Hashie::Dash
  property :total
  property :posts
  property :page
end
```

- All services are modules without any state.
- All models are dumb structs with transaction processors attached to them or just fancy hashes.

Fetching posts from Instagram or Facebook is more complicated but uses the same design rules.

```ruby
# fetch_instagram.rb
loop do
  sources = SourceService.for_instagram
  sources.each do |source|
    source = InstragramService.ensure_system_id_is_set source

    InstragramService.posts_for(source.system_id).each do |instagram_attrs|
      PostService.create InstagramToPostTransformer.transform(instagram_attrs)
    end

    sleep 5
  end
end

module InstragramService
  class << self
    def user_id_for(username)
      ...
    end

    def posts_for(system_id)
      ...
    end

    def ensure_system_id_is_set(source)
      ...
    end
  end
end

module SourceService
  class << self
    def for_instagram
      ...
    end

    def for_facebook
      ...
    end

    def update_system_id(source, system_id)
      ...
    end
  end
end

module PostService
  class << self
    def create(post_attrs)
      ...
    end
  end
end

module InstagramToPostTransformer
  class << self
    def transform(instagram_attrs)
      ...
    end
  end
end
```

I have removed the logic from the code to keep it brief.

__fetch_instagram.rb illustrates a different approach to coupling__. Rather then they typical approach of having one way coupling code moves down through the stack, have the main loop (fetch_instagram.rb) be the orchestration layer and ensure that it has the logic to push and pull data between all of the other layers in the stack.

__This becomes a major system design rule, that only orchestration layers can depend on other tiers. There isn't any other dependencies allowed.__

Comparing this approach to that I used in a recent large application:

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xl="http://www.w3.org/1999/xlink" version="1.1" viewBox="203 17 154 189" width="154pt" height="189pt"><metadata xmlns:dc="http://purl.org/dc/elements/1.1/"><dc:date>2014-08-10 23:03Z</dc:date><!-- Produced by OmniGraffle Professional 5.4.4 --></metadata><defs><font-face font-family="Helvetica" font-size="12" units-per-em="1000" underline-position="-75.683594" underline-thickness="49.316406" slope="0" x-height="532.22656" cap-height="719.72656" ascent="770.01953" descent="-229.98047" font-weight="bold"><font-face-src><font-face-name name="Helvetica-Bold"/></font-face-src></font-face></defs><g stroke="none" stroke-opacity="1" stroke-dasharray="none" fill="none" fill-opacity="1"><title>Canvas 4</title><g><title>Layer 1</title><path d="M 208.09857 17 L 351.177 17 C 353.93842 17 356.177 19.238576 356.177 22 L 356.177 38.117647 C 356.177 40.87907 353.93842 43.117647 351.177 43.117647 L 208.09857 43.117647 C 205.33714 43.117647 203.09857 40.87907 203.09857 38.117647 L 203.09857 22 C 203.09857 19.238576 205.33714 17 208.09857 17 Z" fill="#1d73c5"/><text transform="translate(208.09857 23.058824)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="24.207183" y="11" textLength="94.66406">Controller/Route</tspan></text><path d="M 208.09857 57.62745 L 351.177 57.62745 C 353.93842 57.62745 356.177 59.866027 356.177 62.62745 L 356.177 78.7451 C 356.177 81.50652 353.93842 83.7451 351.177 83.7451 L 208.09857 83.7451 C 205.33714 83.7451 203.09857 81.50652 203.09857 78.7451 L 203.09857 62.62745 C 203.09857 59.866027 205.33714 57.62745 208.09857 57.62745 Z" fill="#1d73c5"/><text transform="translate(208.09857 63.686275)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="37.209136" y="11" textLength="68.660156">Coordinator</tspan></text><line x1="279.63776" y1="43.117647" x2="279.63776" y2="57.62745" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 208.09857 98.2549 L 351.177 98.2549 C 353.93842 98.2549 356.177 100.49348 356.177 103.2549 L 356.177 119.37255 C 356.177 122.13397 353.93842 124.37255 351.177 124.37255 L 208.09857 124.37255 C 205.33714 124.37255 203.09857 122.13397 203.09857 119.37255 L 203.09857 103.2549 C 203.09857 100.49348 205.33714 98.2549 208.09857 98.2549 Z" fill="#1d73c5"/><text transform="translate(208.09857 104.313725)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="50.187652" y="11" textLength="42.703125">Service</tspan></text><line x1="279.63776" y1="83.7451" x2="279.63776" y2="98.2549" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 208.09857 138.88235 L 351.177 138.88235 C 353.93842 138.88235 356.177 141.12093 356.177 143.88235 L 356.177 160 C 356.177 162.76142 353.93842 165 351.177 165 L 208.09857 165 C 205.33714 165 203.09857 162.76142 203.09857 160 L 203.09857 143.88235 C 203.09857 141.12093 205.33714 138.88235 208.09857 138.88235 Z" fill="#1d73c5"/><text transform="translate(208.09857 144.94118)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="42.204253" y="11" textLength="58.669922">Command</tspan></text><line x1="279.63779" y1="124.37255" x2="279.63779" y2="138.88235" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 208.09857 179.5098 L 351.177 179.5098 C 353.93842 179.5098 356.177 181.74838 356.177 184.5098 L 356.177 200.62745 C 356.177 203.38887 353.93842 205.62745 351.177 205.62745 L 208.09857 205.62745 C 205.33714 205.62745 203.09857 203.38887 203.09857 200.62745 L 203.09857 184.5098 C 203.09857 181.74838 205.33714 179.5098 208.09857 179.5098 Z" fill="#1d73c5"/><text transform="translate(208.09857 185.56863)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="48.869292" y="11" textLength="45.339844">Adapter</tspan></text><line x1="279.63779" y1="164.99999" x2="279.63779" y2="179.5098" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/></g></g></svg>

The design of the interface would change to:

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xl="http://www.w3.org/1999/xlink" version="1.1" viewBox="117 21 326 148" width="326pt" height="148pt"><metadata xmlns:dc="http://purl.org/dc/elements/1.1/"><dc:date>2014-08-10 23:08Z</dc:date><!-- Produced by OmniGraffle Professional 5.4.4 --></metadata><defs><font-face font-family="Helvetica" font-size="12" units-per-em="1000" underline-position="-75.683594" underline-thickness="49.316406" slope="0" x-height="532.22656" cap-height="719.72656" ascent="770.01953" descent="-229.98047" font-weight="bold"><font-face-src><font-face-name name="Helvetica-Bold"/></font-face-src></font-face></defs><g stroke="none" stroke-opacity="1" stroke-dasharray="none" fill="none" fill-opacity="1"><title>Canvas 5</title><g><title>Layer 1</title><path d="M 122.09856 61.627455 L 265.17699 61.627455 C 267.93841 61.627455 270.17699 63.86603 270.17699 66.627455 L 270.17699 82.7451 C 270.17699 85.506526 267.93841 87.7451 265.17699 87.7451 L 122.09856 87.7451 C 119.33714 87.7451 117.09856 85.506526 117.09856 82.7451 L 117.09856 66.627455 C 117.09856 63.86603 119.33714 61.627455 122.09856 61.627455 Z" fill="#1d73c5"/><text transform="translate(122.09856 67.68628)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="24.207183" y="11" textLength="94.66406">Controller/Route</tspan></text><path d="M 294.09856 21 L 437.177 21 C 439.93841 21 442.177 23.238576 442.177 26 L 442.177 42.117647 C 442.177 44.87907 439.93841 47.117647 437.177 47.117647 L 294.09856 47.117647 C 291.33714 47.117647 289.09856 44.87907 289.09856 42.117647 L 289.09856 26 C 289.09856 23.238576 291.33714 21 294.09856 21 Z" fill="#1d73c5"/><text transform="translate(294.09856 27.058824)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="50.187652" y="11" textLength="42.703125">Service</tspan></text><line x1="248.92348" y1="61.627455" x2="310.35207" y2="47.117647" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 294.09856 60.62745 L 437.177 60.62745 C 439.93841 60.62745 442.177 62.866027 442.177 65.62745 L 442.177 81.7451 C 442.177 84.50652 439.93841 86.7451 437.177 86.7451 L 294.09856 86.7451 C 291.33714 86.7451 289.09856 84.50652 289.09856 81.7451 L 289.09856 65.62745 C 289.09856 62.866027 291.33714 60.62745 294.09856 60.62745 Z" fill="#1d73c5"/><text transform="translate(294.09856 66.686275)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="50.187652" y="11" textLength="42.703125">Service</tspan></text><path d="M 294.09856 102.2549 L 437.177 102.2549 C 439.93841 102.2549 442.177 104.49348 442.177 107.2549 L 442.177 123.37255 C 442.177 126.13397 439.93841 128.37255 437.177 128.37255 L 294.09856 128.37255 C 291.33714 128.37255 289.09856 126.13397 289.09856 123.37255 L 289.09856 107.2549 C 289.09856 104.49348 291.33714 102.2549 294.09856 102.2549 Z" fill="#1d73c5"/><text transform="translate(294.09856 108.313725)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="42.204253" y="11" textLength="58.669922">Command</tspan></text><line x1="270.17699" y1="74.24128" x2="289.09856" y2="74.13127" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 294.09856 142.88235 L 437.177 142.88235 C 439.93841 142.88235 442.177 145.12093 442.177 147.88235 L 442.177 164 C 442.177 166.76142 439.93841 169 437.177 169 L 294.09856 169 C 291.33714 169 289.09856 166.76142 289.09856 164 L 289.09856 147.88235 C 289.09856 145.12093 291.33714 142.88235 294.09856 142.88235 Z" fill="#1d73c5"/><text transform="translate(294.09856 148.941175)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="48.869292" y="11" textLength="45.339844">Adapter</tspan></text><line x1="248.9235" y1="87.7451" x2="310.35206" y2="102.2549" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 211.26337 87.7451 L 266.09856 128.37255 L 318.48762 142.88235" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/></g></g></svg>

The goal of this approach is:

- Controllers/routes tests are automatically full stack tests and can be consistent across the system.
- Testing functions in every other tier of the system is isolated and requires very little setup.
- Programmers can forget about what state an object is in and focus on transforming data.

The downside of this is that controllers grow in size but the upside is that complexity is brought to the surface rather than having iceberg style services. It also allows for some tiers to be introduced, like transformers for converting between data structures and validators that just check data integrity.

Summing up, the rules for designing systems in this manner are:

1. All data objects are structs without any extra methods.
2. All database models are dumb transaction processors, nothing more.
3. Logic to be held in services.
4. Services are to be stateless (i.e. use modules).
5. State is to be held in main loops and external interfaces.
6. __Only orchestration layers (routers, controllers, main loops) can depend on other tiers.__

Having used this on a small system with great success, I'm confident it will help with large system design greatly.

I love flame wars so tweet me your thoughts: @cjwoodward and use the hashtag #orchestrationfocuseddesign.
