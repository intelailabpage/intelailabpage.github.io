---
title: "News"
layout: textlay
excerpt: "Intel AI Lab."
sitemap: false
permalink: /allnews.html
---


# 🔥 News
{% for article in site.data.news %}
<div>
<!-- {{ article.date }} : {{ article.headline | markdownify}} -->
{{ article.date }} : {{ article.headline}}  
</div>
{% endfor %}
