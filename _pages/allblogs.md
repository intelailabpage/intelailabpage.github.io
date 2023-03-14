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


<form action="{{ post.url }}">
  <!-- <div class="tipue_search_left"> <p><img src="/assets/tipuesearch/search.png" class="tipue_search_icon"></p></div> -->
  <div class="tipue_search_right"><p> <img src="/assets/tipuesearch/search.png"> <input type="text" name="q" id="tipue_search_input" pattern=".{3,}" title="At least 3 characters" required></p></div>
  <div style="clear: both;"></div>
</form>

<div id="tipue_search_content"><p></p></div>

<script>
$(document).ready(function() {
  $('#tipue_search_input').tipuesearch();
});
</script>



{% for blog in site.posts %}
<div> 
<h3> <a href="{{site.url }}{{ site.baseurl }}{{blog.permalink}}"> {{blog.title}}  </a> </h3>
<h5><mark>Click the title for the details.</mark></h5> 
<!-- <mark>{{site.url }}{{ site.baseurl }}{{blog.permalink}} </mark> -->
{{ blog.excerpt}} 

</div>

{% endfor %}

