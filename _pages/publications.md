---
layout: archive
title: "Selected Publications"
permalink: /publications/
author_profile: true
---

{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

<hr style="border-top:3px">

{% for post in site.publications reversed %}
  {% include archive-single-pub.html %}
{% endfor %}
