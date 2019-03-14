---
title: "Throttling and Debouncing Function Invocation in JavaScript"
link: http://tech.mybuilder.com/throttling-and-debouncing-function-invocation-in-javascript/
meta: "Looking into Throttling and Debouncing Function Invocation in JavaScript"
---

Whilst working on resolving a recent JavaScript event handler bug, it deemed necessary to implement a form of throttling to make sure a race-condition would not occur.
Throughout the fix I found myself seeking a clear definition of what both `throttling` and `debouncing` a function actually entailed; as it can be very easy to mix the two subtly different concepts.
<!--more-->
