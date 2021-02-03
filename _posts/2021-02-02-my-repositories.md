---
layout: post
title: "A List of My Repositories"
date: 2021-02-01
---

## List of my repositories [{{site.github.public_repositories.size}}]:

{%- for repository in site.github.public_repositories -%}
  * [{{ repository.name }}]({{ repository.html_url }})
{%- endfor -%}

## Jekyll and Liquid

This list was initially generated from the GitHub API

* [Jekyll & Liquid Cheatsheet](https://gist.github.com/magicznyleszek/9803727)
* [Getting Started with Jekyll and GitHub Pages](https://www.aleksandrhovhannisyan.com/blog/getting-started-with-jekyll-and-github-pages/#dr-jekyll-and-mr-liquid)
* [Liquid](https://shopify.github.io/liquid/basics/introduction/)
* [Jekyll Default Variables](https://it.knightnet.org.uk/kb/ghjekyll/standard-attributes/)

## Python script

This list was initially generated from the GitHub API [GitHub REST API](https://docs.github.com/en/rest) with this Python script:

{% highlight python linenos %}
import requests

github_username = 'PeterAnema'

url = f'https://api.github.com/users/{github_username}/repos'

r = requests.get(url)

if r.status_code == 200:

    for repo in sorted(r.json(), key = lambda repo: repo['name']):
        print(f'* [{repo["name"]}]({repo["html_url"]})')
{% endhighlight %}
