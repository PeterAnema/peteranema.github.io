---
layout: post
title: "How to work with ... Jekyll"
description: "Tips and tricks for working with Github Pages, Jekyll and Markdown"
date: 2021-02-01
category: Dev
tags: [web, jekyll, markdown]
---

## Resources

### GitHub Pages

* <https://pages.github.com>

### Jekyll

* [Jekyll Home](https://jekyllrb.com)
* [Jekyll Tags on Github Pages - Long Qian](http://longqian.me/2017/02/09/github-jekyll-tag/)

### Markdown

* [Markdown Guide](https://www.markdownguide.org/basic-syntax)
* [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)

## Markdown Fenced Code Block

```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

## Code Snippit Highlighting

Jekyll has built in support for syntax highlighting of over 100 languages thanks to Rouge. Rouge is the default highlighter in Jekyll 3 and above.

{% highlight python linenos %}
def do_something():
  return 'Did it!'
{% endhighlight %}
