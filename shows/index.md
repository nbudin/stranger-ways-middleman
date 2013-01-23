---
title: Shows
layout: page
---

{% for post in site.categories.Shows %}
<h2 class="entry-title">[{{ post.title }}]({{ post.url }})</h2>
<span class="entry-meta">Posted on <time datetime="{{ post.date | date_to_xmlschema}}">{{ post.date | date_to_long_string }}</time></span>
<div class="entry-summary">
  <p>{{ post.content | strip_html | truncatewords words:25 }}</p>
  <a href="{{post.url}}">Continue reading →</a>
</div>
{% endfor %}