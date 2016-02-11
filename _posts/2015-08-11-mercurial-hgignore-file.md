---
layout: post
title: Mercurial HGIgnore File
tags: 
- mercurial
comments: true
date: 2015-08-11 21:01:27
---

I could not figure out why Mercurial was not using my hgignore file. I didn't realize that it needed to be declared in the .hgrc file. Adding

`ignore = ~/.hgignore_global`

to the [ui] section fixed it.

Thanks goes to [we are all robots](http://prototypef.tumblr.com/post/1185499766/mercurial-global-ignore-pattern-its-awesome).


