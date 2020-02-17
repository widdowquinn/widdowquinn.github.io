---
layout: splash
permalink: /group/
title: "Group Pages"
toc: true
---

## PhD student info

{% for post in site.categories.PhD %}
- {{ post.date | date_to_string }}: [{{ post.title }}]({{ post.url }})
{% endfor %}

## `Python` group style

{% for post in site.categories.Style %}
- {{ post.date | date_to_string }}: [{{ post.title }}]({{ post.url }})
{% endfor %}

## Coding guidelines

{% for post in site.categories.Coding %}
- {{ post.date | date_to_string }}: [{{ post.title }}]({{ post.url }})
{% endfor %}