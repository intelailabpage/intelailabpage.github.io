---
title: "Intel AI Lab - Team"
layout: gridlay
excerpt: "Intel AI Lab: Team members"
sitemap: false
permalink: /team/
---

# Group Members 

 <!-- **We are  looking for new PhD students, Postdocs, and Master students to join the team** [(see openings)]({{ site.url }}{{ site.baseurl }}/openings) **!** -->


<!-- Jump to [staff](#staff), [master and bachelor students](#master-and-bachelor-students), [alumni](#alumni), [administrative support](#administrative-support), [lab visitors](#lab-visitors). -->


## Lab Director

<div class="row">

{% for member in site.data.director_members %}

<div class="col-sm-4 clearfix">
  <img src="{{ site.url }}{{ site.baseurl }}/images/teampic/{{ member.photo }}" class="img-responsive" width="50%" style="float: up" />
  <h4>{{ member.name }}</h4>
  <h5> <a href="{{ member.website }}">Personal website</a>   <br> <a href="{{member.linkedin}}"> LinkedIn </a> </h5>
<!--   <i>{{ member.info }} <br> <a href="{{member.linkedin}}"> LinkedIn </a> </i> -->
<!--   <i>{{ member.info }} <br>email: <{{ member.email }}></i> -->
  <ul style="overflow: hidden"></ul>
</div>

{% endfor %}

</div>


## Researchers

<div class="row">

{% for member in site.data.researchers_members %}

<div class="col-sm-4 clearfix">
  <img src="{{ site.url }}{{ site.baseurl }}/images/teampic/{{ member.photo }}" class="img-responsive" width="50%" style="float: up" />
  <h4>{{ member.name }}</h4>
  <h5> <a href="{{ member.website }}">Personal website</a> <br> <a href="{{member.linkedin}}"> LinkedIn </a> </h5>
<!--   <i>{{ member.info }} <br> <a href="{{member.linkedin}}"> LinkedIn </a> </i> -->
<!--   <i>{{ member.info }} <br>email: <{{ member.email }}></i> -->
  <ul style="overflow: hidden"></ul>
</div>

{% endfor %}

</div>



## Interns

<div class="row">

{% for member in site.data.interns_members %}

<div class="col-sm-4 clearfix">
  <img src="{{ site.url }}{{ site.baseurl }}/images/teampic/{{ member.photo }}" class="img-responsive" width="50%" style="float: up" />
  <h4>{{ member.name }}</h4>
  <h5> <a href="{{ member.website }}">Personal website</a> <br> <a href="{{member.linkedin}}"> LinkedIn </a> </h5>
<!--   <i>{{ member.info }} <br> <a href="{{member.linkedin}}"> LinkedIn </a> </i> -->
<!--   <i>{{ member.info }} <br>email: <{{ member.email }}></i> -->
  <ul style="overflow: hidden"></ul>
</div>

{% endfor %}

</div>
