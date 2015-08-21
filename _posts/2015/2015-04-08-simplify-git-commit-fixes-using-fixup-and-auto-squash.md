---
title: "Simplify Git commit fixes using fixup and auto-squash"
link: http://tech.mybuilder.com/simplify-git-commit-fixes-using-fixup-and-auto-squash/
meta: "Use fixup and auto-squash commands to manage 'fix' commits in Git"
---

Throughout a project I will typically make commits that could be categorised as fixes to previous commits.
To help highlight such commits I would follow the pattern of starting the message with 'fix: ...', making the final rebase step (before merging into master) easier.
However, as time passed locating which 'fix-commits' related to other previous commits became harder to determine.
<!--more-->