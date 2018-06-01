---
layout: default
title: Pathways
---

# Pathways found so far

{% assign allpaths = site.pathways | where_exp: "item", "item.title != 'Pathways'" | sort: 'date' | reverse %}
{% for p in allpaths %}
- <a href="{{ p.url | relative_url }}">{{ p.title }}</a>
{% endfor %}