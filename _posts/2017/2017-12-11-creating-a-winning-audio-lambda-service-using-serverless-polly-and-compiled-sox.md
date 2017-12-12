---
title: "Creating a 'Winning' Audio Lambda Service using Serverless, Polly and compiled SOX"
link: http://tech.mybuilder.com/creating-a-winning-audio-lambda-service-using-serverless-polly-and-compiled-sox/
meta: "Creating a 'Winning' Audio Lambda Service using Serverless, Polly and compiled SOX"
---

Following on from my previous post which discussed [manipulating images](http://tech.mybuilder.com/memes-as-a-service-using-lambda-serverless-and-imagemagick/), I would now like to expand upon this and look into how you can interact with audio using Lambda.
To highlight this use-case we will be creating a simple service which given a name and optional voice (provided by [Polly](https://aws.amazon.com/polly/)), will synthesise the name and include it in a returned 'And the winner is...' applause MP3 file.
This will demonstrate how to integrate Polly within Lambda, compile and execute native-code within Lambda and return a binary MP3 file to the client.
<!--more-->