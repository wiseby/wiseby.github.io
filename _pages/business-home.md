---
title: "Wiseby Design"
permalink: /business/
layout: archive
author_profile: true
---

Integration and platform work — Laravel, .NET, and the plumbing that connects
webshops, ERPs, and warehouses. Mostly written up here as I go.

## Latest articles

{% for post in site.categories.articles limit: 5 %}
  {% include archive-single.html post=post %}
{% endfor %}
