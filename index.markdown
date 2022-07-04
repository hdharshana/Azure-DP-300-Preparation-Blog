---
layout: default
title: Azure DP-300 Learning Notes
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
---
layout: post
title:  Welcome to my Azure DP-300 Certification Blog!
date: 2020-07-01 21:00:00 -0300
categories: DP-300
---

# __Purpose__

This blog summarizes the important take aways and key points to help prepare for the DP-300 Microsoft certtification exam. 

# __Resources__

* [MS Learn Content Path if you like to read and practice](https://docs.microsoft.com/en-us/learn/certifications/exams/dp-300)
* [Video Series Related to the MS learning Path on Channel 9](https://www.youtube.com/playlist?list=PLlrxD0HtieHi5c9-i_Dnxw9vxBY-TqaeN)

# __Time Estimate__

This certification took me about 3 days to prepare for from scatch to the end! I started on a Friday and took my certification test on a Monday! The time also involved 
me blogging all this journey along...

# __Certification Scheduling__

You can schedule your certification by clicking [here](https://examregistration.microsoft.com/?whr=uri:MicrosoftAccount&locale=en-us&examcode=DP-300&examname=Exam%20DP-300:%20Administering%20Relational%20Databases%20on%20Microsoft%20Azure&returnToLearningUrl=https%3A%2F%2Fdocs.microsoft.com%2Flearn%2Fcertifications%2Fexams%2Fdp-300#userlegalprofile/)
Note: I scheduled to take an online exam at the comfort of my home, but you have options to either take it online from home or at a test center.

__Set a date for your exam and get started!__


<div class="post">

  <div class="header-bar">
    <h2>{{ site.blog_name }}</h2>
    <h2>{{ site.blog_description }}</h2>
  </div>


  <ul class="post-list">
    {% for post in site.posts %}
      <li>
        <h3 style="color:red"><a class="post-title" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h3>
        # <p class="post-meta">{{ post.date | date: '%B %-d, %Y' }}</p>
        <p>{{ post.description }}</p>
      </li>
    {% endfor %}
  </ul>

