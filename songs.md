---
layout: audiopage
title: Songs
files:
  - /assets/audio/На_перекрёстках_жизни_много_трудностей.mp3
---

- [audio1][1]
- [audio1][1]
- [audio2][2]

{% assign i = 0 %}
{% for file in page.files %}
{% increment i %}
[{{ i }}]: {{ files | relative_url }}?autoplay=1&loop=1&controls=0
{% endfor %}

[2]:{{ page.files[0] | relative_url }}?autoplay=1&loop=1&controls=0

