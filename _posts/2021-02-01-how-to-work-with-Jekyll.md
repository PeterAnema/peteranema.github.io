# How to work with ... Jekyll

## Resources

* [Jekyll Home](https://jekyllrb.com)
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
