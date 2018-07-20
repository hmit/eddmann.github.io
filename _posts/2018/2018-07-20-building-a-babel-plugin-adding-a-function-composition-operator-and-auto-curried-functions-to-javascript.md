---
title: "Building a Babel Plugin: Adding a Function Composition Operator and Auto-Curried Functions to JavaScript"
link: https://tech.mybuilder.com/building-a-babel-plugin-adding-a-function-composition-operator-and-auto-curried-functions-to-javascript/
meta: "Building a Babel Plugin: Adding a Function Composition Operator and Auto-Curried Functions to JavaScript"
---

In a recent Software Engineering Daily [podcast](https://softwareengineeringdaily.com/2018/06/21/babel-with-henry-zhu/) Henry Zhu discussed the [Babel](https://babeljs.io/) project, and shed some light into how the transpiler works under-the-hood.
He touched upon how [Plugins](https://babeljs.io/docs/en/plugins.html) can be created to alter the resulting compiled code.
I was very interested in experimenting with this capability.
In this post I wish to highlight the process in which Babel transforms your code, developing several interesting plugins along the way.
<!--more-->
