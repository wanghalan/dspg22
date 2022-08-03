---
title: Projects
layout: single
---

{% for page in site.pages %}
  <section>
      <h2>{{ page.title }}</h2>
      <p>{{ page.content | markdownify }}</p>
    </article>
    {% endfor %}
  </section>
{% endfor %}
