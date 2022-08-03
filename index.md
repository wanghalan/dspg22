---
title: Projects
layout: single
---

{% for page in site.pages %}
  <section>
      <h2>{{ page.title }}</h2>
      <p>{{ page.excerpt | markdownify }}</p>
    </article>
  </section>
{% endfor %}
