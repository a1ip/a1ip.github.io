---
layout: audiopage
title: Songs
files:
  - /assets/audio/На_перекрёстках_жизни_много_трудностей.mp3
---

{% for i in (1..files.size) %}
{% assign file = files[i] %}
[{{ i }}]: {{ file | relative_url }}?autoplay=1&loop=1&controls=0
{% endfor %}

