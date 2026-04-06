---
title: "News"
layout: textlay
excerpt: "Intel Multimodal AI Innovation Lab."
sitemap: false
permalink: /allnews.html
---


# 🔥 News
{% for article in site.data.news %}
<div>
<!-- {{ article.date }} : {{ article.headline | markdownify}} -->
  <b>{{ article.date }} </b>: {{ article.headline}}  
</div>
{% endfor %}
