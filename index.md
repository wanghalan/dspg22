---
title: Projects
layout: single
---

{% for page in site.pages %}
  ## {{ page.title }}
  {{ page.excerpt | markdownify }}
  [read more](page.url)
{% endfor %}
