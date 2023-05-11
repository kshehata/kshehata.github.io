---
layout: post
title:  "How I Made This Site"
date:   2023-05-10 15:17:21 +0800
---

This site uses:
* [Jekyll](https://jekyllrb.com/)
* [GitHub Pages](https://pages.github.com/)
* [Katex](https://katex.org/) for math formatting
* Custom sed script for taking Notion-exported pages and fixing the math formatting
* Jekyll Collection for talks and pubs

# Steps

1.  Follow the [Jekyll docs](https://jekyllrb.com/docs/) to install
Jekyll and all its dependencies. Much easier than the GitHub docs.

2. Once you have a site working locally, then follow the GitHub docs for setting up pages.

3. From [this SO answer](https://stackoverflow.com/questions/34347818/using-mathjax-on-a-github-page)
to enable MathJax you have to add the JS for it in your head. I wrapped it in a Liquid if-statement
so that it's only loaded when needed, but that's optional.

4. Follow [Daniel Sieger's guide](https://www.danielsieger.com/blog/2019/03/03/publication-pages-using-jekyll-collections.html) to make a publications list from a collection.

# Notion Export

For some reason, Notion exports to markdown using a single dollar
sign ($) for inline formulas. Unfortunately, this kinda breaks
everything, since most markdown expects a dollar sign to be just a
dollar sign, and a double-dollar sign for math.

Fortunately, `sed` exists to solve this problem. Here's a simple script that fixes it.

``` sed
s/\([^\$]\)\$\([^\$]\)/\1$$\2/g
s/\([^\$]\)\$\([^\$]\)/\1$$\2/g
s/\([^\$]\)\$\\/\1$$\\/g
s/\([^\$]\)\$$/\1$$/
s/^\$\([^\$]\)/$$\1/
```
