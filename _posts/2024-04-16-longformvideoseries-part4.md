---
layout: post
title: "Long-form video representation learning (Part 4: Long-form video reasoning)"
date: 2024-04-16
permalink: /2024/04/16/longformvideoseries-part4.html
author: <a href="https://subarnatripathi.github.io/"> Subarna Tripathi </a>
excerpt: "Current video understanding systems accurately recognize patterns in short video clips, but fails to process a video content over a few seconds due to computation and memory bottleneck. We propose a video representation method based on a spatio-temporal graph learning (SPELL) to equip it with long-term reasoning ability... "  
---



Current video understanding systems accurately recognize patterns in short video clips. 
However, they fail to capture how the present connects to the past or future in a world of never-ending visual stimuli. 
Existing video architectures tend to hit computation or memory bottlenecks after processing only a few seconds of video content. 
So, how do we enable accurate and efficient long-term visual understanding? An important first step is to have a model that practically 
runs on long videos. To that end, we explore novel video represnetation learning methods that are equipped with long-form reasoning capability. 

This is part 4 focusing on how we are pushing the boundary of "long-form" reasoning leveraging "short-form" foundation models in a memory and computation-efficient ways. 
See <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part1.html"> Part I </a> on video as "object-centric" spatio-temporal graphs and <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part2.html"> Part II </a> on video as temporal graphs for modeling several video understanding tasks. 
See <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part3.html"> Part III </a> to learn about sparse video-text transformers and a sneak peek to our current explorations. 


<p>
We showed how explicit graph based methods can aggregate 10X temporal context, but they were two-stage methods. Next, we explored how we can make end to end models based on transformers memory and compute efficient and aggregate 2X temporal context. In this post, we show a glimpse of what we are doing to aggregate ambitious 20X-50X temporal context aggregation using just a fraction of memory and compute requirement comparing with existing foundation models. The long story short is we are leveraging exisiting foundation models (essentially "short-term") for creating "long-form" reasoning. A sneak peek to our current work in progress looks something like below:

![]({{ site.url }}{{ site.baseurl }}/images/pubpic/lavi-t.png){: style="width: 970px; float: left; margin: 0px 10px"}  

The first thing you will notice about our method is that our model is not tied to a fixed number of input frames anymore. Our method is extremely memory and compute efficient. Two example evaluations zero-shot and fine-tuned activity recognition on Charades-ego show the efficacy of our method. Please note, we are using Ego4D as our pretraining dataset. 

<br>
Stay tuned to know more about this exciting and promising line of work !!

  
</p>
