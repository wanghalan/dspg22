---
title: Projects
layout: single
---

{% for page in site.pages %}
  ## {{ page.title }}
  {{ page.excerpt | markdownify }}
  [read more here]({{ page.url }})
{% endfor %}
