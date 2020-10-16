---
layout: post
title: "Tutorial: set up jekyll locally"
date: 2020-10-15
tags: [jekyll]
---
There can be some extra steps besides the instructions in the official doc.

+ [install Jekyll](https://jekyllrb.com/docs/installation/ubuntu/)

+ [create the gem file and populate it with jekyll](https://stackoverflow.com/questions/59913903/how-to-run-bundle-exec-jekyll-new)

	```
	bundle init
	bundle add jekyll
	```

+ [add kramdown parser to gemfile](https://stackoverflow.com/questions/63335953/jekyll-error-building-page-related-to-kramdown-parser)

	```
	gem "kramdown-parser-gfm"
	```

+ [open terminal and type command bundler](https://stackoverflow.com/questions/63335953/jekyll-error-building-page-related-to-kramdown-parser)

+ `bundle exec jekyll serve`