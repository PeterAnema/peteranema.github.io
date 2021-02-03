---
layout: post
title: "How to work with ... Github Pages"
description: "Tips and tricks for working with Github Pages, Markdown, Jekyll and Liquid"
date: 2021-02-01
category: Dev
tags: [Github, Markdown, Jekyll, Liquid]
---

## Resources

### GitHub Pages

* <https://pages.github.com>
* <http://jmcglone.com/guides/github-pages/>

### Jekyll

* [Jekyll Home](https://jekyllrb.com)
* [Jekyll Tags on Github Pages - Long Qian](http://longqian.me/2017/02/09/github-jekyll-tag/)

### Markdown

* [Markdown Guide](https://www.markdownguide.org/basic-syntax)
* [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)

### Liquid
* [Jekyll & Liquid Cheatsheet](https://gist.github.com/magicznyleszek/9803727)
* [Getting Started with Jekyll and GitHub Pages](https://www.aleksandrhovhannisyan.com/blog/getting-started-with-jekyll-and-github-pages/#dr-jekyll-and-mr-liquid)
* [Liquid](https://shopify.github.io/liquid/basics/introduction/)
* [Jekyll Default Variables](https://it.knightnet.org.uk/kb/ghjekyll/standard-attributes/)



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
