---
layout: blog
title: Blog Posts
---

<div class="section bg-blue text-white container" markdown="1" align="center">

{% for file in site.blog %}
  {% if file.blogpost %}
### <i class="fa fa-2x fa-{{file.icon}}"></i> [{{file.title}}]({{file.url}})
{{file.description}}
  {% endif %}
{% endfor %}

</div>
