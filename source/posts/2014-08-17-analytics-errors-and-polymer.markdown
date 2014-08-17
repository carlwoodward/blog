---
title: Analytics, Errors and Polymer
layout: post
---

With Revisit.io being in beta, the priority right now is reviewing what features are being used and responding to feedback/bugs/errors. After looking into a bunch of analytics tools and error tracking apps, it became clear that an app that combines error tracking and analytics would be very useful.

Revisit Analytics and Errors is a custom prototype that combines:

- Analytics on a per user basis
- Error tracking
- Grouping data by day
- Filter analytics and errors by user and day basis - to show the path a user took to get to any given error

<video width="512" height="258" autoplay loop>
  <source src="http://cl.ly/2n1F0j1t1v0i/download/supportalytics.mp4" type="video/mp4">
</video>

## Architecture

Having a tiny data model and wanting to make the app super fast made Golang standout as the right choice for the backend. A bonus was being able to run it on a 512mb server. After writing a lot of Elixir and [Orchestration Focused Design](/changing-coupling), it has become much easier to abstract out common issues with Golang and make it very enjoyable to program in.

There has been a lot of hype about Polymer as a new structure for frontend development recently. The platform has been maturing quite rapidly and it was worth trying in a small project before diving into something bigger.

The architecture for the app is shown below:

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xl="http://www.w3.org/1999/xlink" version="1.1" viewBox="78 14 404 368" width="404pt" height="368pt"><metadata xmlns:dc="http://purl.org/dc/elements/1.1/"><dc:date>2014-08-17 05:23Z</dc:date><!-- Produced by OmniGraffle Professional 5.4.4 --></metadata><defs><font-face font-family="Helvetica" font-size="12" units-per-em="1000" underline-position="-75.683594" underline-thickness="49.316406" slope="0" x-height="522.94922" cap-height="717.28516" ascent="770.01953" descent="-229.98047" font-weight="500"><font-face-src><font-face-name name="Helvetica"/></font-face-src></font-face><font-face font-family="Helvetica" font-size="12" units-per-em="1000" underline-position="-75.683594" underline-thickness="49.316406" slope="0" x-height="532.22656" cap-height="719.72656" ascent="770.01953" descent="-229.98047" font-weight="bold"><font-face-src><font-face-name name="Helvetica-Bold"/></font-face-src></font-face><marker orient="auto" overflow="visible" markerUnits="strokeWidth" id="FilledArrow_Marker" viewBox="-1 -3 7 6" markerWidth="7" markerHeight="6" color="#b3b3b3"><g><path d="M 4.8000002 0 L 0 -1.8000001 L 0 1.8000001 Z" fill="currentColor" stroke="currentColor" stroke-width="1"/></g></marker></defs><g stroke="none" stroke-opacity="1" stroke-dasharray="none" fill="none" fill-opacity="1"><title>Canvas 6</title><g><title>Layer 1</title><path d="M 80.137787 16 L 479.1378 16 L 479.1378 157 L 80.137787 157 Z" stroke="black" stroke-linecap="round" stroke-linejoin="round" stroke-width="1" stroke-dasharray="4,4"/><text transform="translate(85.137787 138.5)" fill="black"><tspan font-family="Helvetica" font-size="12" font-weight="500" x="0" y="11" textLength="24.011719">POL</tspan><tspan font-family="Helvetica" font-size="12" font-weight="500" x="23.126953" y="11" textLength="34.669922">YMER</tspan></text><path d="M 80.137787 232 L 479.1378 232 L 479.1378 380 L 80.137787 380 Z" stroke="black" stroke-linecap="round" stroke-linejoin="round" stroke-width="1" stroke-dasharray="4,4"/><text transform="translate(85.137787 361.5)" fill="black"><tspan font-family="Helvetica" font-size="12" font-weight="500" fill="black" x="0" y="11" textLength="51.345703">GOLANG</tspan></text><path d="M 208.09856 324 L 351.17699 324 C 353.93841 324 356.17699 326.23858 356.17699 329 L 356.17699 345.11765 C 356.17699 347.87907 353.93841 350.11765 351.17699 350.11765 L 208.09856 350.11765 C 205.33714 350.11765 203.09856 347.87907 203.09856 345.11765 L 203.09856 329 C 203.09856 326.23858 205.33714 324 208.09856 324 Z" fill="#1d73c5"/><text transform="translate(208.09856 330.05882)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="24.409332" y="11" textLength="63.345703">In Memory </tspan><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="87.31558" y="11" textLength="31.353516">Array</tspan></text><path d="M 122.559335 264 L 265.63776 264 C 268.39919 264 270.63776 266.23858 270.63776 269 L 270.63776 285.11765 C 270.63776 287.87907 268.39919 290.11765 265.63776 290.11765 L 122.559335 290.11765 C 119.79791 290.11765 117.559335 287.87907 117.559335 285.11765 L 117.559335 269 C 117.559335 266.23858 119.79791 264 122.559335 264 Z" fill="#1d73c5"/><text transform="translate(122.559335 270.05882)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="10.847808" y="11" textLength="121.38281">CreateEventsHandler</tspan></text><path d="M 293.63778 264 L 436.71621 264 C 439.47764 264 441.71621 266.23858 441.71621 269 L 441.71621 285.11765 C 441.71621 287.87907 439.47764 290.11765 436.71621 290.11765 L 293.63778 290.11765 C 290.87636 290.11765 288.63778 287.87907 288.63778 285.11765 L 288.63778 269 C 288.63778 266.23858 290.87636 264 293.63778 264 Z" fill="#1d73c5"/><text transform="translate(293.63778 270.05882)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="18.857574" y="11" textLength="105.36328">ListEventsHandler</tspan></text><line x1="212.71591" y1="290.11765" x2="250.45944" y2="316.59219" marker-end="url(#FilledArrow_Marker)" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><line x1="298.25514" y1="324" x2="335.99866" y2="297.52546" marker-end="url(#FilledArrow_Marker)" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 122.559335 186 L 265.63776 186 C 268.39919 186 270.63776 188.23858 270.63776 191 L 270.63776 207.11765 C 270.63776 209.87907 268.39919 212.11765 265.63776 212.11765 L 122.559335 212.11765 C 119.79791 212.11765 117.559335 209.87907 117.559335 207.11765 L 117.559335 191 C 117.559335 188.23858 119.79791 186 122.559335 186 Z" fill="#1d73c5"/><text transform="translate(122.559335 192.05882)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="44.86441" y="11" textLength="53.34961">Revisit.io</tspan></text><line x1="194.09854" y1="212.11765" x2="194.09854" y2="251.1" marker-end="url(#FilledArrow_Marker)" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 293.63778 39 L 436.71621 39 C 439.47764 39 441.71621 41.238576 441.71621 44 L 441.71621 60.117647 C 441.71621 62.87907 439.47764 65.117647 436.71621 65.117647 L 293.63778 65.117647 C 290.87636 65.117647 288.63778 62.87907 288.63778 60.117647 L 288.63778 44 C 288.63778 41.238576 290.87636 39 293.63778 39 Z" fill="#1d73c5"/><text transform="translate(293.63778 45.058824)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="10.194488" y="11" textLength="122.68945">core-ajax Component</tspan></text><line x1="365.177" y1="65.117647" x2="365.177" y2="251.1" marker-end="url(#FilledArrow_Marker)" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 122.559324 39 L 265.63775 39 C 268.39918 39 270.63775 41.238576 270.63775 44 L 270.63775 60.117647 C 270.63775 62.87907 268.39918 65.117647 265.63775 65.117647 L 122.559324 65.117647 C 119.7979 65.117647 117.559324 62.87907 117.559324 60.117647 L 117.559324 44 C 117.559324 41.238576 119.7979 39 122.559324 39 Z" fill="#1d73c5"/><text transform="translate(122.559324 45.058824)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="5.214019" y="11" textLength="132.65039">time-group Component</tspan></text><path d="M 122.559324 95 L 265.63775 95 C 268.39918 95 270.63775 97.23858 270.63775 100 L 270.63775 128 C 270.63775 130.761426 268.39918 133 265.63775 133 L 122.559324 133 C 119.7979 133 117.559324 130.761426 117.559324 128 L 117.559324 100 C 117.559324 97.23858 119.7979 95 122.559324 95 Z" fill="#1d73c5"/><text transform="translate(122.559324 100)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="28.185699" y="11" textLength="90.041016">analytics-event </tspan><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="38.21109" y="25" textLength="66.65625">Component</tspan></text><line x1="194.09853" y1="65.117647" x2="194.09853" y2="82.1" marker-end="url(#FilledArrow_Marker)" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><line x1="270.63775" y1="52.077257" x2="275.73779" y2="52.078486" marker-end="url(#FilledArrow_Marker)" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/></g></g></svg>

[Building Sourcegraph, a large-scale code search engine in Go](https://sourcegraph.com/blog/google-io-2014-building-sourcegraph-a-large-scale-code-search-engine-in-go) is a great post on how to structure Golang web applications. Following it meant that only one external package was required for this application: [Gorilla / Mux](https://github.com/gorilla/mux). [Best Practices for Production Environments](http://www.confreaks.com/videos/3434-gophercon2014-best-practices-for-production-environments) is also a great break down of tips for writing Golang code.

Routing in the backend is quite simple:

```go
router := mux.NewRouter()
router.HandleFunc("/events.json", ListEventsHandler).Methods("GET")
router.HandleFunc("/events.json", CreateEventHandler).Methods("POST")
router.HandleFunc("/create_event.json", CreateEventHandler).Methods("GET")

http.Handle("/", router)

http.ListenAndServe(":3001", nil)
```

The other big tip with Golang is don't be fancy. For loops are used over and over in the code for filtering the main array. They are quick and simple. Abstracting them is very tempting but the Golang ethos is to keep programming simple, even if it involves a little bit of repetition. Below is an example:

```go
func filterEventsByDate(events []Event, date string) []Event {
  var eventsByDate []Event

  for i := 0; i < len(events); i++ {
    if events[i].CreatedAt.Format("2006-01-02") == date {
      eventsByDate = append(eventsByDate, events[i])
    }
  }

  return eventsByDate
}
```

On to Polymer. Polymer lets you structure frontend components in one file. Each file encapsulates its own templating, stylesheets and javascript.

The structure of a Polymer component looks like:

```
<link rel="import" href="/bower_components/polymer/polymer.html">
<link rel="import" href="/bower_components/core-ajax/core-ajax.html">

<polymer-element name="time-group" noscript>
  <template>
    <style>
      :host .analytics-events {
        position: absolute;
        width: 82.5%;
        top: 4rem;
        right: 0;
      }
    </style>

    <core-ajax auto url="{{url}}" handleAs="json" on-core-response="{{eventsLoaded}}"></core-ajax>

    <section class="analytics-events">
      <template repeat="{{event in events}}">
        <analytics-event on-select="{{changeSelection}}" event="{{event}}"></analytics-event>
      </template>
    </section>
  </template>

  <script>
    Polymer('time-group', {
      events: null,

      created: function() {
        this.events = [];
      },

      eventsLoaded: function(event, result) {
        this.events = result.response || [];
        this.eventCount = this.events.length;
      }
    });
  </script>
</polymer-element>
```

The code above is a skeleton of the real code but you can see that all sections of the code are used to encapsulate the display and behaviour of the component.

Because Polymer uses Shadow DOM, it means that each component is fully encapsulated. This article http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-201/ has a great explanation of how Shadow DOM styling works and how you can punch through it when needed. The hard thing is that styles can't leak through from the main stylesheet into the Shadow DOM, which means that all SASS helpers were useless without a small trick. Below is an example:

```css
.events-menu a.logo {
  color: pink;
}
```

![Without Shadow DOM punching](http://cl.ly/image/190D2H3e3W0Z/logo-no-punch.png)

If you explicitly reference the ::shadow pseudo-element then you can create styles that apply across Shadow DOM elements.

```css
::shadow .events-menu a.logo {
  color: pink;
}
```

![With Shadow DOM punching](http://cl.ly/image/1q1U1c0X1R3C/logo-with-punch.png)

Polymer leverages components to try and remove as much hand coding of javascript as possible. A good example of this is the __core-ajax__ component. It provides a html tag like interface to making an ajax call. It can call a javascript function or just set a bound variable. If the data doesn't need any transformation then having it populate a variable that is iterated over is a simple way to list data from a server in plain old tags.

Components can publish the variables that they allow invokers to pass in. And variables in the form of {{variable}} are passed by reference to the component so the template can access all of the nested data in the variable. A simple example is below:

```javascript
var event = { name: 'Revisit Event' };
```

```
<analytics-event event="{{event}}"></analytics-event>
```

```
<link rel="import" href="/bower_components/polymer/polymer.html">

<polymer-element name="analytics-event" attributes="event" noscript>
  <template>
    <style>
    </style>

    <div class="name">{{event.name}}</div>
  </template>

  <script>
    Polymer('analytics-event', {});
  </script>
</polymer-element>
```

Overall Polymer feels like an evolution of nesting controllers in Angular and laying out code in React. Polymer has all the fancy two way binding that Angular has. Most people are using Polymer with Angular for routing. This sounds like a great idea. I definitely think it is a great way to make apps and I'd consider using it over straight Angular.

My next post will be comparing Angular and Polymer with Angular on the same code base.
