---
layout: splash
permalink: /home/
header:
  overlay_color: "#ff0000"
  overlay_image: bg.jpg
  caption:
excerpt: '...freelance engineer and blogger to the internet, father to a sneaky son, husband to a brilliant wife and I will have my PhD in this life or the next. <br> Applogies- I am experimenting here :)'
intro:
  - excerpt: 'Get notified when I add new stuff &nbsp; [<i class="fa fa-twitter"></i> @ip_v1](https://twitter.com/ip_v1){: .btn .btn--twitter}'
---

{% include feature_row id="intro" type="center" %}

{% include feature_row %}

{% include base_path %}
{% include group-by-array collection=site.posts field="categories" %}

{% for category in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ category | slugify }}" class="archive__subtitle">{{ category }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}
