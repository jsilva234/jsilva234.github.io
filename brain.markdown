---
layout: default
title: Second Brain
permalink: /brain/
---

# Second Brain

{% assign subtopic_pages = site.pages | where: "layout", "subtopic" %}
{% assign topics = subtopic_pages | group_by: "topic" | sort: "name" %}

<ul>
  {% for topic in topics %}
    <li>{{ topic.name }}
      <ul>
        {% assign subs = topic.items | sort: "subtopic" %}
        {% for sub in subs %}
          <li><a href="{{ sub.url | relative_url }}">{{ sub.subtopic }}</a></li>
        {% endfor %}
      </ul>
    </li>
  {% endfor %}
</ul>
