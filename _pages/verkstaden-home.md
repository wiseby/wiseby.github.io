---
title: "Verkstad"
permalink: /verkstad/
layout: archive
author_profile: true
locale: sv-SE
---

Projekt, byggen och sådant som inte hör hemma på jobbet. Mest trä, metall och
elektronik — och en del dokumentation av misstag.

## Senaste artiklarna

{% for post in site.categories.artiklar limit: 5 %}
  {% include archive-single.html post=post %}
{% endfor %}
