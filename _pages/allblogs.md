---
title: "Blogs"
layout: post
excerpt: "Intel AI Lab."
sitemap: false
permalink: /allblogs.html
tipue_search_active: true
exclude_from_search: true
---

# 🚧 ⛏️ 🛠️ 👷

{% for blog in site.posts %}
<div> 
<h3> <a href="{{site.url }}{{ site.baseurl }}{{blog.permalink}}"> {{blog.title}}  </a> </h3>
<h5><mark>Click the title for the details.</mark></h5> 
<!-- <mark>{{site.url }}{{ site.baseurl }}{{blog.permalink}} </mark> -->
{{ blog.excerpt}} 

</div>

{% endfor %}

