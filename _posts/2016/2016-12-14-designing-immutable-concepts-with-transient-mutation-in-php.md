---
title: "Designing Immutable Concepts with Transient Mutation in PHP"
link: http://tech.mybuilder.com/designing-immutable-concepts-with-transient-mutation-in-php/
meta: "Looking into designing Immutable concepts with Transient Mutation in PHP"
---

In a recent project we felt it beneficial to introduce the Money pattern.
There are many good [resources](http://martinfowler.com/eaaCatalog/money.html) on this pattern, so I will delegate to those for further definition.
We decided that encapsulating this into a [immutable value object](http://hangar.runway7.net/punditry/immutability-value-objects) allowed for a cleaner API and removed the fear of any unexpected mutation bugs.
However, we noticed a spike in memory and processor usage when wishing to perform many successive actions on such values i.e. summation.
<!--more-->
