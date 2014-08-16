---
title: Building Golang Code on OSX from Homebrew for Linux
layout: post
---

After searching for a while I couldn't find this exact snippet. Use it to build golang code on your mac for linux servers.

```bash
export GOROOT=/usr/local/Cellar/go/1.3/libexec # Make sure this gets set at login.
cd $GOROOT/src
GOOS=linux GOARCH=amd64 ./make.bash --no-clean # Only need to do this once.

cd PATH_TO_PROJECT
GOOS=linux GOARCH=amd64 go build FILE.go
```
