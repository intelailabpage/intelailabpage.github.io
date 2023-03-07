---
title: "Intel AI Lab - Pictures"
layout: piclay
excerpt: "Intel AI Lab -- Pictures"
permalink: /pictures/
---

# Pictures
<!-- Jump to: [Leiden](#leiden), [ETHZ](#ethz), [Cornell](#cornell), [St Andrews](#st-andrews) -->


## Events and Talks

<!-- #### Test test [(see LION news item)](https://www.physics.leidenuniv.nl/index.php?id=11573&news=867&type=lion&ln=EN): -->
<!-- #### AI Journey talk, 2021                               -->
<iframe width="460" height="280" src="https://www.youtube.com/embed/jFdsJiejZyw??start=76&end=120" frameborder="0" allowfullscreen></iframe>
<iframe width="460" height="280" src="https://www.youtube.com/embed/WCOOxsY0z34" frameborder="0" allowfullscreen></iframe> 

### Gallery
(Right-click *'view image'* to see a larger image.)
{% assign number_printed = 0 %}
{% for pic in site.data.pictures_Leiden %}

{% assign even_odd = number_printed | modulo: 4 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-3 clearfix">
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/Gallery/{{ pic.image }}" class="img-responsive" width="95%" style="float: left" />
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd > 2 %}
</div>
{% endif %}


{% endfor %}

{% assign even_odd = number_printed | modulo: 4 %}
{% if even_odd == 1 %}
</div>
{% endif %}

{% if even_odd == 2 %}
</div>
{% endif %}

{% if even_odd == 3 %}
</div>
{% endif %}

<p> &nbsp; </p>


<!-- ## Cornell
From the [group of Seamus JC Davis](http://davisgroup.lassp.cornell.edu).
<figure>
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/WebpageCornell_red.jpg" width="60%">
</figure> -->


