---
title: Projects
layout: single
---

{% for page in site.pages %}
  {% if page.identifier == 'dspg22' %}    
    <h1> {{ page.title }} </h1>
    <p> 
      {{ page.excerpt | markdownify }} 
      <a href= {{ page.url }}> read more here </a>
    </p>
  {% endif %}
{% endfor %}
