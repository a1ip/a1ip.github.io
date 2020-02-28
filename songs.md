---
layout: audiopage
title: Songs
files:
  - /assets/audio/На_перекрёстках_жизни_много_трудностей.mp3
---

- [audio1][0]
- [audio1][0]
- [audio2][2]


{% for file in page.files %}
[{% increment i %}]: {{ files | relative_url }}?autoplay=1&loop=1&controls=0
{% endfor %}

[2]:{{ page.files[0] | relative_url }}?autoplay=1&loop=1&controls=0

