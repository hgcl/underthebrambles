---
layout: default
title: Under the Brambles
---

<section>
  <h3>Latest Posts</h3>
  <ul>
    {% for post in site.posts %}
      <li><a href="{{ post.url }}">{{ post.title }}</a> <span>{{ post.date | date: "%B %-d, %Y" }}</span></li>
    {% endfor %}
  </ul>
</section>
