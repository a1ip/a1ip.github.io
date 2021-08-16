---
layout: page
subtitle: Tags
permalink: /tags
lang: en

---

{% capture tags %}
  {% for tag in site.tags %}{{ tag[0] }}{% unless forloop.last %}{{ " " }}{% endunless %}{% endfor %}
{% endcapture %}
{% assign sortedtags = tags | split: " " | sort %}

{% for tag in sortedtags %}
  <h3 id="{{ tag }}">{{ tag | replace: "-"," " }}</h3>
  <ul>
  {% capture tag_posts %}{% for post in site.posts %}{% if post.tags contains tag %}{{ post.title }}{% unless forloop.last %}{{ "\next" }}{% endunless %}{% endif %}{% endfor %}{% endcapture %}
  {% assign sorted_tag_posts = tag_posts | split:"\next" | sort %}
  {% for title in sorted_tag_posts %}
    {% for post in site.posts %}
      {% if post.title == title %}
        <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
      {% endif %}
    {% endfor %}
  {% endfor %}
  </ul>
{% endfor %}
