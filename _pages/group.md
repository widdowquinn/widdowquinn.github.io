---
layout: splash
permalink: /group/
title: "Group Pages"
toc: true
toc_label: "Table of Contents"
toc_icon: "book-reader"
toc_sticky: true
---

## General group info

- [Group code of conduct](/group/code_of_conduct)
- [Group philosophy](/group/philosophy)
- [Group responsibilities](/group/responsibilities)
- [Group Python coding style guidelines](/group/python_style)

## PhD student info

- [**Current Opportunities**](/phd/opportunities){: .btn .btn--success}

{% for post in site.categories.PhD %}
- {{ post.date | date_to_string }}: [{{ post.title }}]({{ post.url }})
{% endfor %}

## How do I edit this website?

Anyone in the group can edit or add to these pages. To do so, please fork this repository from [https://github.com/widdowquinn/widdowquinn.github.io](https://github.com/widdowquinn/widdowquinn.github.io), make your changes, and issue a pull request against the original repository, tagging Leighton as a reviewer. Most requests will be merged without question, but the time to changes going live may vary.