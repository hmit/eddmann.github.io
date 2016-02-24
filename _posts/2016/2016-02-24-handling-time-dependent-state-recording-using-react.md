---
title: "Handling Time-Dependent State Recording using React"
link: http://tech.mybuilder.com/handling-time-dependent-state-recording-using-react/
meta: "Exploration into handling Time-Dependent State Recording using React"
---

Sometimes you look at a feature request and think that it maybe a very tricky implementation to develop.
I felt this way in regard to recording input fields in an recent application I have been working on.
The idea was to be able to record a user's interaction with a HTML component (in this case a textarea), and be able to replay these events (in real-time) at a later date.
Thinking about how I would go about creating such an implementation in trivial JavaScript, with all the browser nuances and user input differences, was not very appealing.
<!--more-->
