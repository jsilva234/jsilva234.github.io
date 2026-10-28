---
title: Second Brain
icon: fas fa-brain
order: 2
permalink: /brain/
---

{% assign subtopic_pages = site.pages | where: "layout", "subtopic" %}
{% assign topics = subtopic_pages | group_by: "topic" | sort: "name" %}

{% for topic in topics %}
- {{ topic.name }}
  {% assign subs = topic.items | sort: "subtopic" %}
  {% for sub in subs %}
  - [{{ sub.subtopic }}]({{ sub.url | relative_url }})
  {% endfor %}
{% endfor %}
