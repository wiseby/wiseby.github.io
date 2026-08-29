---
title: "Services"
permalink: /business/services/
layout: archive
author_profile: true
---

What I take on, and roughly what it looks like to work together.

{% for item in site.services %}
  {% include archive-single.html post=item %}
{% endfor %}
