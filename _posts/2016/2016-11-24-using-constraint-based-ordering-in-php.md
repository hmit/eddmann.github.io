---
title: "Using Constraint-based Ordering in PHP"
link: http://tech.mybuilder.com/using-constraint-based-ordering-in-php/
meta: "Looking into using Constraint-based Ordering in PHP"
---

An interesting problem arose last week when we wished to generate a listing of recently completed jobs (along with their shortlist fees).
Upon review of some earlier attempts, we did not like the aesthetics present when many of a particular shortlist fee were clustered together (i.e. two or more adjacent jobs with the same shortlist fee).
What we were instead looking for was to create a constraint-based ordering that when applied to the recently completed jobs, would give an even distribution of shortlist fees (data-set permitting).
<!--more-->