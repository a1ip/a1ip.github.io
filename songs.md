---
layout: audiopage
title: Songs
files:
  - /assets/audio/На_перекрёстках_жизни_много_трудностей.mp3
---

- [audio1][1]
- [audio1][1]

{% assign i = 0 %}
{% for file in files %}
{% increment i %}
[{{ i }}]: {{ files | relative_url }}?autoplay=1&loop=1&controls=0
{% endfor %}

