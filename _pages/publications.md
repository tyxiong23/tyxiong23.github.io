---
layout: archive
title: "Selected Publications"
compact_title: true
permalink: /publications/
author_profile: true
---

<!-- {% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %} -->

A full list of my publications can be found on my <a href="https://scholar.google.com/citations?user=dv0NRZgAAAAJ">Google Scholar</a>.

{% include base_path %}

<hr style="border-top:3px">

{% for publication in site.publications reversed %}
  {% unless publication.display_after %}
    {% assign post = publication %}
    {% include archive-single-pub.html %}
    {% assign following_publications = site.publications | where: "display_after", publication.url %}
    {% for post in following_publications reversed %}
      {% include archive-single-pub.html %}
    {% endfor %}
  {% endunless %}
{% endfor %}
