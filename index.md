---
title: Projects
---

{% for page in site.pages %}
{% if page.identifier == "dspg22" %}    
## {{ page.title }}
{{ page.content | markdownify | strip_html | truncatewords: 50 }} ([read more]({{ site.baseurl }}{{ page.url }}))
{% endif %}
{% endfor %}
