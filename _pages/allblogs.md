---
title: "Blogs"
layout: post
excerpt: "Intel AI Lab."
sitemap: false
permalink: /allblogs.html
---


{% for blog in site.posts %}
<div> 

<h3> <a href="{{site.url }}{{ site.baseurl }}{{blog.permalink}}"> {{blog.title}}  </a> </h3>
<h5><mark>Click the title for the details.</mark></h5> 
Debug: check site address: {{ site.url }}{{ site.baseurl }}{{post.permalink}}
{{ blog.excerpt}} 

</div>

{% endfor %}
