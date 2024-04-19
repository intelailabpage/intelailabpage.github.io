---
layout: post
title: "Long-form video representation learning (Part 5: Modeling visual relationships and actions)"
date: 2024-04-18
permalink: /2024/04/18/longformvideoseries-part5.html
author: <a href="https://subarnatripathi.github.io/"> Subarna Tripathi </a>
excerpt: "Current video understanding systems accurately recognize patterns in short video clips, but fails to process a video content over a few seconds due to computation and memory bottleneck. We propose a video representation method based on a spatio-temporal graph learning (SPELL) to equip it with long-term reasoning ability... "  
---



Current video understanding systems accurately recognize patterns in short video clips. 
However, they fail to capture how the present connects to the past or future in a world of never-ending visual stimuli. 
Existing video architectures tend to hit computation or memory bottlenecks after processing only a few seconds of video content. 
So, how do we enable accurate and efficient long-term visual understanding? An important first step is to have a model that practically 
runs on long videos. To that end, we explore novel video represnetation learning methods that are equipped with long-form reasoning capability. 

In this blog, we will take you to the journey of how to model visual relations. 
See <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part1.html"> Part I </a> on video as "object-centric" spatio-temporal graphs and <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part2.html"> Part II </a> on video as temporal graphs for modeling several video understanding tasks. 
See <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part3.html"> Part III </a> to learn about sparse video-text transformers and a sneak peek to our current explorations. 
See <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part3.html"> Part IV </a> to know how we are pushing the boundary of "long-form" reasoning leveraging "short-form" foundation models in a memory and computation-efficient ways. 

<p>
We showed how explicit graph based methods can aggregate 10X temporal context, but they were two-stage methods. Next, we explored how we can make end to end models based on transformers memory and compute efficient and aggregate 2X temporal context. We also showed a glimpse of what we are doing to aggregate ambitious 20X-50X temporal context aggregation using just a fraction of memory and compute requirement comparing with existing foundation models.
We start by modeling visual relationships in images, where the core problem is to convert an image to a semantic graph where nodes represent object instances and directed edges represent relationship between a pair of objects. Often, the 
relationship might mean action or some other kind of spatial relation.

ICCV 2021 : long-tailed distribution;
ICCV 2021 : application of scene graphs for image captioning
NeurIPS 2022: Single stage SGG detection
WACV 2023: video scene graph generation; temporal context
CVPR 2023: video scene graph generation; unbiased

We wanted to leverage such structured representation for egocentric video understanding. What to do if there is no scene graph ground truth? 
We created a dataset, showed how they are useful for different tasks such as action anticipation and summarization;

CVPR 2024: Action scene graphs
  
</p>
