---
title: "Gör det själv"
permalink: /verkstaden/gor-det-sjalv/
layout: archive
author_profile: true
locale: sv-SE
---

Byggbeskrivningar med mått, materiallistor och de misstag jag hann göra på vägen.

{% for item in site.diy %}
  {% include archive-single.html post=item %}
{% endfor %}
