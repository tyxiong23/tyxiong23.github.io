---
layout: archive
title: "Selected Publications"
permalink: /publications/
author_profile: true
---

<!-- {% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %} -->

A full list of my publications can be found on my <a href="https://scholar.google.com/citations?user=dv0NRZgAAAAJ">Google Scholar</a>.

{% include base_path %}

<hr style="border-top:3px">

{% for post in site.publications reversed %}
  {% include archive-single-pub.html %}
{% endfor %}
