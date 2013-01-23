---
title: Shows
layout: page
---

{% for post in site.categories.Shows %}
<h2 style="display: inline;">[{{ post.title }}]({{ post.url }})</h2><br/>
<em>Posted {{ post.date | date_to_long_string }}</em>
{% endfor %}