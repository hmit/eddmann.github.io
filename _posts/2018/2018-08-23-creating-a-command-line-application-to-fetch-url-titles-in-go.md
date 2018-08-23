---
title: "Creating a Command Line Application to Fetch URL Titles in Go"
link: https://tech.mybuilder.com/creating-a-command-line-application-to-fetch-url-titles-in-go/
meta: "Creating a Command Line Application to Fetch URL Titles in Go"
---

When writing show-notes for [Three Devs and a Maybe](https://threedevsandamaybe.com/) it is tedious work to extract the associated show-link titles and generate a Markdown list from them.
This is something that I have [documented in the past](https://eddmann.com/posts/fetching-link-titles-using-promises-and-async-await-in-javascript/), providing an automated solution to this problem.
However, in this post I would like to discuss implementing such a command-line tool using [Golang](https://golang.org/), creating self-reliant executables that can be cross-compiled for Mac, Windows and Linux.
<!--more-->
