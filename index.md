---
title: Projects
layout: single
---

{% for collection in site.pages %}
  {% assign name = collection.label %}
  <section>
    <h1>{{ name }}</h1>
    {% for page in site.[name] %}
    <article>
      <h2>{{ page.title }}</h2>
      <p>{{ page.content | markdownify }}</p>
    </article>
    {% endfor %}
    
  </section>
{% endfor %}
