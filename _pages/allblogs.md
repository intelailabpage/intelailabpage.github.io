---
title: "Blogs"
layout: post
excerpt: "Intel AI Lab."
sitemap: false
permalink: /allblogs.html
---


{% for blog in site.posts %}
<!-- <p>{{ article.date }} <br>
<em>{{ article.headline | markdownify}}</em></p> -->
<div> 
<h3>{{blog.title}} - {{blog.date}} </h3>
<h4>{{blog.author}} </h4>
{{ blog.content | markdownify}} 
 <ul style="overflow: hidden"></ul>
</div>

{% endfor %}
