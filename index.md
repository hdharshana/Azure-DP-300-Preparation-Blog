---
layout: default
title: blog
pagination:
  enabled: true
  collection: posts
  <!-- permalink: /page/:num/ -->
  per_page: 3
  sort_field: date
  sort_reverse: true
  trail:
    before: 1 # The number of links before the current page
    after: 3  # The number of links after the current page
---

<div class="post">

  <div class="header-bar">
    <h2>{{ site.blog_name }}</h2>
    <h2>{{ site.blog_description }}</h2>
  </div>


  <ul class="post-list">
    {% for post in site.posts %}
      <li>
        <h3 style="color:red"><a class="post-title" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h3>
        <p class="post-meta">{{ post.date | date: '%B %-d, %Y' }}</p>
        <p>{{ post.description }}</p>
      </li>
    {% endfor %}
  </ul>

</div>