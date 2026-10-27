---
layout: default
title: Second Brain
permalink: /brain/
---

# Second Brain

{% assign topics = site.notes | group_by: "topic" | sort: "name" %}

<ul>
  {% for topic in topics %}
    <li>{{ topic.name }}
      <ul>
        {% assign subtopics = topic.items | group_by: "subtopic" | sort: "name" %}
        {% for sub in subtopics %}
          <li>{{ sub.name }}
            <ul>
              {% for note in sub.items %}
                <li><a href="#{{ note.title | slugify }}">{{ note.title }}</a></li>
              {% endfor %}
            </ul>
          </li>
        {% endfor %}
      </ul>
    </li>
  {% endfor %}
</ul>

{% for topic in topics %}
<h2>{{ topic.name }}</h2>
  {% assign subtopics = topic.items | group_by: "subtopic" | sort: "name" %}
  {% for sub in subtopics %}
<h3>{{ sub.name }}</h3>
    {% for note in sub.items %}
<h4 id="{{ note.title | slugify }}">{{ note.title }}</h4>
{{ note.content | markdownify }}
    {% endfor %}
  {% endfor %}
{% endfor %}
