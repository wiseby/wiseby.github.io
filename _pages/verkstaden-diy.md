---
title: "Gör det själv"
permalink: /verkstaden/gor-det-sjalv/
layout: archive
author_profile: true
locale: sv-SE
---

Här beskriver jag hur man åstadkommer diverse och gör det möjligt för dig att göra samma sak, förhoppningsvis.

{% for item in site.diy %}
  {% include archive-single.html post=item %}
{% endfor %}
