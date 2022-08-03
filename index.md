---
title: Projects
layout: single
---

{% for page in site.pages %}
  {% if page.identifier == 'dspg22' %}
    
    ## {{ page.title }}
    {{ page.excerpt | markdownify }}
    [read more here]({{ page.url }})
    
  {% endif %}
{% endfor %}
