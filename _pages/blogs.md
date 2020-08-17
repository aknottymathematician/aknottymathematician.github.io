---
layout: tag
permalink: /blogs/
author_profile: true
header:
  image: "/assets/images/KM_blog-posts-banner_16-August-2020.jpg"
author_profile: true
taxonomy: blog
entries_layout: list
---

```{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}
```
