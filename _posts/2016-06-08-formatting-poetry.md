---
layout: post
title: Formatting Poetry
tags:
- jekyll
- poetry 
comments: true
date: 2016-06-08 13:18:29
---

I have been browsing [Jekyll](http://jekyllrb.com/) themes lately, and found a very nice theme for academics, the [Ed. Theme](http://elotroalex.github.io/ed/documentation/#bibliographies). Its main purpose seems to be publishing classic texts and poetry on the web, and it includes some very handy tools. 

Getting indentation right is a problem with poetry on the web. For example, consider these lines from "The Code—Heroics" by Robert Frost.

Here is the Markdown source:

``` markdown
What was there wrong?
                     Something you said just now.
What did I say?
               About our taking pains.
```

It renders like this:

What was there wrong?  
                     Something you said just now.  
What did I say?  
               About our taking pains.

With help from the CSS in the .Ed theme, I can get the indentation right.

``` markdown
- What was there wrong?
- {:.indent-10}Something you said just now.
- What did I say?
- {:.indent-10}About our taking pains.
{:.poetry}
```

produces

- What was there wrong?
- {:.indent-10}Something you said just now.
- What did I say?
- {:.indent-4}About our taking pains.
{:.poetry}

