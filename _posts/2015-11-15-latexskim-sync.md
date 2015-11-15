---
layout: post
title: LaTeX-Skim Sync
tags:
- emacs
- latex
comments: true
date: 2015-11-15 17:18:41
---

I recently started using John Wiegley's [use-package](https://github.com/jwiegley/use-package ) for my Emacs init files. For Auctex, I used


```
(use-package tex
  :ensure auctex)
```

and everything worked except for sync with Skim on OS X. ```C-c v``` would not launch the Skim, even though I was confident that the Skim was set to be the default viewer. Instead, no viewer would launch, and I'd see "View command: dvi2tty -q -w 132" in the minibuffer.

After seeing that some others had used a slightly different configuration, I changed mine to

```
(use-package tex-site
  :ensure auctex)
```

and everything started working fine. I still have no idea why, but it may help someone else.
