---
layout: post
title: "A List of My Repositories"
date: 2021-02-01
tags: [Github]
---

## List of my repositories [{{site.github.public_repositories.size}}]:

{% for repository in site.github.public_repositories %}
* [{{ repository.name }}]({{ repository.html_url }})
{%- endfor %}

## Next ...