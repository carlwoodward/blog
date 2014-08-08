---
title: Web Sockets, Ember and Elixir
layout: post
---

[Revisit.io](https://revisit.io) is prodominatly made of Elixir and Ember.js code. It has some Node.js and Ruby code thrown in for good
measure. One thing that makes it quite different/interesting is that the communication between the client and
the application is done with web sockets.

## Posting a bookmark in Revisit

When a user posts a bookmark in Revisit the process is broken down into:

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xl="http://www.w3.org/1999/xlink" version="1.1" viewBox="53 19 453 258" width="453pt" height="258pt"><metadata xmlns:dc="http://purl.org/dc/elements/1.1/"><dc:date>2014-08-08 04:56Z</dc:date><!-- Produced by OmniGraffle Professional 5.4.4 --></metadata><defs><font-face font-family="Helvetica" font-size="12" units-per-em="1000" underline-position="-75.683594" underline-thickness="49.316406" slope="0" x-height="532.22656" cap-height="719.72656" ascent="770.01953" descent="-229.98047" font-weight="bold"><font-face-src><font-face-name name="Helvetica-Bold"/></font-face-src></font-face></defs><g stroke="none" stroke-opacity="1" stroke-dasharray="none" fill="none" fill-opacity="1"><title>Canvas 1</title><g><title>Layer 1</title><path d="M 58.775542 19 L 259.77554 19 C 262.53697 19 264.77554 21.238576 264.77554 24 L 264.77554 50 C 264.77554 52.761424 262.53697 55 259.77554 55 L 58.775542 55 C 56.01412 55 53.775542 52.761424 53.775542 50 L 53.775542 24 C 53.775542 21.238576 56.01412 19 58.775542 19 Z" fill="#1d73c5"/><text transform="translate(58.775542 30)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="66.16992" y="11" textLength="68.660156">Submit URL</tspan></text><path d="M 58.775542 129 L 259.77554 129 C 262.53697 129 264.77554 131.23858 264.77554 134 L 264.77554 160 C 264.77554 162.76142 262.53697 165 259.77554 165 L 58.775542 165 C 56.01412 165 53.775542 162.76142 53.775542 160 L 53.775542 134 C 53.775542 131.23858 56.01412 129 58.775542 129 Z" fill="#1d73c5"/><text transform="translate(58.775542 140)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="28.148438" y="11" textLength="144.703125">Start Screenshot Capture</tspan></text><line x1="159.27556" y1="55" x2="159.27556" y2="129" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 299.49999 76 L 500.5 76 C 503.2614 76 505.5 78.238576 505.5 81 L 505.5 107 C 505.5 109.761424 503.2614 112 500.5 112 L 299.49999 112 C 296.73857 112 294.49999 109.761424 294.49999 107 L 294.49999 81 C 294.49999 78.238576 296.73857 76 299.49999 76 Z" fill="#1d73c5"/><text transform="translate(299.49999 87)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="61.59961" y="11" textLength="58.007812">Request T</tspan><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="118.722656" y="11" textLength="20.677734">ags</tspan></text><path d="M 299.5 129 L 500.5 129 C 503.26142 129 505.5 131.23858 505.5 134 L 505.5 160 C 505.5 162.76142 503.26142 165 500.5 165 L 299.5 165 C 296.73858 165 294.5 162.76142 294.5 160 L 294.5 134 C 294.5 131.23858 296.73858 129 299.5 129 Z" fill="#1d73c5"/><text transform="translate(299.5 140)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="40.145508" y="11" textLength="120.708984">Broadcast Bookmark</tspan></text><line x1="399.99999" y1="112" x2="399.99999" y2="129" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><line x1="294.49999" y1="94" x2="159.27556" y2="94" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 58.775542 185 L 259.77554 185 C 262.53697 185 264.77554 187.23858 264.77554 190 L 264.77554 216 C 264.77554 218.76142 262.53697 221 259.77554 221 L 58.775542 221 C 56.01412 221 53.775542 218.76142 53.775542 216 L 53.775542 190 C 53.775542 187.23858 56.01412 185 58.775542 185 Z" fill="#1d73c5"/><text transform="translate(58.775542 196)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="45.823242" y="11" textLength="109.353516">Upload Screenshot</tspan></text><line x1="159.27555" y1="165" x2="159.27555" y2="185" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 58.775542 241 L 259.77554 241 C 262.53697 241 264.77554 243.23858 264.77554 246 L 264.77554 272 C 264.77554 274.76142 262.53697 277 259.77554 277 L 58.775542 277 C 56.01412 277 53.775542 274.76142 53.775542 272 L 53.775542 246 C 53.775542 243.23858 56.01412 241 58.775542 241 Z" fill="#1d73c5"/><text transform="translate(58.775542 252)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="40.145508" y="11" textLength="120.708984">Broadcast Bookmark</tspan></text><line x1="159.27553" y1="221" x2="159.27553" y2="241" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/></g></g></svg>

What this actually does on the frontend is:

<video width="518" height="494" autoplay loop>
  <source src="http://cl.ly/1o2z3c0b1h3Q/download/post-bookmark-2.mp4" type="video/mp4">
</video>

Using web sockets allows Revisit to skip polling for changes and just receive a push message when a bookmark is updated.

The most interesting thing here is broadcast bookmark. It works like a chat server, in that it iterates over the users who should receive the message and then sends the message to each of the open connections:

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xl="http://www.w3.org/1999/xlink" version="1.1" viewBox="174 19 212 148" width="212pt" height="148pt"><metadata xmlns:dc="http://purl.org/dc/elements/1.1/"><dc:date>2014-08-08 04:56Z</dc:date><!-- Produced by OmniGraffle Professional 5.4.4 --></metadata><defs><font-face font-family="Helvetica" font-size="12" units-per-em="1000" underline-position="-75.683594" underline-thickness="49.316406" slope="0" x-height="532.22656" cap-height="719.72656" ascent="770.01953" descent="-229.98047" font-weight="bold"><font-face-src><font-face-name name="Helvetica-Bold"/></font-face-src></font-face></defs><g stroke="none" stroke-opacity="1" stroke-dasharray="none" fill="none" fill-opacity="1"><title>Canvas 2</title><g><title>Layer 1</title><path d="M 179.27553 19 L 380.27553 19 C 383.03696 19 385.27553 21.238576 385.27553 24 L 385.27553 50 C 385.27553 52.761424 383.03696 55 380.27553 55 L 179.27553 55 C 176.51411 55 174.27553 52.761424 174.27553 50 L 174.27553 24 C 174.27553 21.238576 176.51411 19 179.27553 19 Z" fill="#1d73c5"/><text transform="translate(179.27553 30)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="60.826172" y="11" textLength="79.347656">Get Followers</tspan></text><path d="M 179.27553 75 L 380.27553 75 C 383.03696 75 385.27553 77.238576 385.27553 80 L 385.27553 106 C 385.27553 108.761424 383.03696 111 380.27553 111 L 179.27553 111 C 176.51411 111 174.27553 108.761424 174.27553 106 L 174.27553 80 C 174.27553 77.238576 176.51411 75 179.27553 75 Z" fill="#1d73c5"/><text transform="translate(179.27553 86)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="28.371094" y="11" textLength="39.351562">Check </tspan><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="67.283203" y="11" textLength="105.3457">Active Conneciton</tspan></text><line x1="279.77552" y1="55" x2="279.77552" y2="75" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/><path d="M 179.27553 131 L 380.27553 131 C 383.03696 131 385.27553 133.23858 385.27553 136 L 385.27553 162 C 385.27553 164.76142 383.03696 167 380.27553 167 L 179.27553 167 C 176.51411 167 174.27553 164.76142 174.27553 162 L 174.27553 136 C 174.27553 133.23858 176.51411 131 179.27553 131 Z" fill="#1d73c5"/><text transform="translate(179.27553 142)" fill="white"><tspan font-family="Helvetica" font-size="12" font-weight="bold" fill="white" x="21.155273" y="11" textLength="158.68945">Send Bookmark to Follower</tspan></text><line x1="279.77552" y1="111" x2="279.77552" y2="131" stroke="#b3b3b3" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"/></g></g></svg>

Elixir makes it really easy to persist the pid of a connection to the database so it can be associated to a user:

```elixir
pid = to_string :erlang.pid_to_list(self)
```

And checking whether a process is still running is simple:

```elixir
Process.alive?(pid)
```

Using send with the given pid allows you to send the data back to the socket in Elixir:

```elixir
send pid, { :message, ExJSON.generate([uuid: "push", payload: App.TimelineEntriesPresenter.present(timeline_entry), type: "timeline_entry"]) }
```

Once data is being pushed to the client adding support for web sockets to Ember is well documented around the web.

Revisit's implementation generates a UUID for all requests that are initiated by the client. When a request is initiated by the server
a "PUSH" request is received and interpreted by the client. The data is pushed into Ember Data like so:

```javascript
var payload = serializer.extract(this, type, adapterPayload, null, 'findAll');

this.pushMany(type, payload);
```

Ember does an amazing job of updating the screen when new data is sent and pushed into Ember Data. Using store.filter is a great way to ensure live
data matches the query that was made to the server previously.

## Browser gets Sleepy

When a user closes their laptop and then comes back later, they will expect the application responds normally to clicks. Even though the web socket
has died (but isn't erroring).

Luckily, it is simple to trap this in the browser and re-establish the connection.

```javascript
window.addEventListener("online", establishConnection);
```

## Join the Beta

If you like bookmarks, join the beta: [Revisit.io](https://revisit.io).
