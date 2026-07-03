---
layout: default
title: Welcome
description: Discover mossy paths, drying herbs, and timeless crafts.
---

<section>
  <h3>Latest Posts</h3>
  <ul>
    {% for post in site.posts %}
      <li><a href="{{ post.url }}">{{ post.title }}</a> <small>{{ post.date | date: "%B %-d, %Y" }}</small></li>
    {% endfor %}
  </ul>
</section>
