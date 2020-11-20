---
layout: page
title: Post archive
---

{% for post in site.posts %}

* {{ post.date | date_to_string }}

    [ {{ post.title }} ]({{ site.url }}{{ post.url }}) &raquo; {% assign words = post.content | number_of_words %}{% if words < 360 %}
    1 min {% else %}
    {{ words | divided_by:210 }} mins
  {% endif %} 
{% endfor %}
