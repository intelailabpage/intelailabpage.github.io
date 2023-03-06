---
title: "Blogs"
layout: post
excerpt: "Intel AI Lab."
sitemap: false
permalink: /allblogs.html
---


{% for blog in site.posts %}
<div> 
{{site.url }}{{site.baseurl }} {{blog.permalink}}
<h3> <a href="{{ site.url }}{{ site.baseurl }}{{blog.permalink}}"> {{blog.title}}  </a> </h3>
<!-- <h4>{{blog.author}} </h4> -->
<h5><mark>Click the title for the details.</mark></h5>
{{ blog.excerpt}} 

</div>

{% endfor %}
