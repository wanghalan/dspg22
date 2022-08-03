---
title: Projects
---

{% for page in site.pages %}
  {% if page.identifier == "dspg22" %}    
  <h1> {{ page.title }} </h1>
    <p> 
    {{ page.content | markdownify | strip_html | truncatewords: 50 }}
    <a href= {{ page.url }}> read more here </a>
    </p>
  {% endif %}
{% endfor %}
