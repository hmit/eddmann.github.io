---
title: "Handling Retries and Back-off Attempts with JavaScript Promises"
link: http://tech.mybuilder.com/handling-retries-and-back-off-attempts-with-javascript-promises/
meta: "Looking into handling Retries and Back-off Attempts with JavaScript Promises"
---

Promises are an invaluable abstraction around 'eventual' results within asynchronous operations.
I recently had the need to be able to retry a Promise-based action in the event of a failure.
It turned out to be very easy to implement such a process using simple recursive constructs.
<!--more-->
