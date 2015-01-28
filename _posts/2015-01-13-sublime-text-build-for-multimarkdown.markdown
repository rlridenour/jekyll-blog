---
layout: post
title: "Sublime Text Build for MultiMarkdown"
date: 2014-01-08 17:11:00 -0600
comments: true
tags: Sublime Text
---

I added some variants to Brett Terpstra's Marked.sublime-build file, which is part of the Marked [Bonus Pack](http://brettterpstra.com/introducing-the-marked-bonus-pack/). It adds options for building tex, opml, and odf files. To build a tex file, open the command palette and search for "MMD to LaTeX." The file is saved as "Marked.sublime-build" in /Users/YourUserName/Library/Application Support/Sublime Text 3/Packages. Here is the complete build file:


	{
		"cmd": ["open","-a","/Applications/Marked.app","$file"],
		"selector": "text.html.markdown",

		"variants": [
			{
				"cmd": ["mmd2tex", "$file"],
				"path": "/usr/local/bin",
				"name": "MMD to LaTeX"
			},

			{
				"cmd": ["mmd2odf", "$file"],
				"path": "/usr/local/bin",
				"name": "MMD to ODF"
			},

			{
				"cmd": ["mmd2opml", "$file"],
				"path": "/usr/local/bin",
				"name": "MMD to OPML"
			}

		]
	}

Happy New Year!
