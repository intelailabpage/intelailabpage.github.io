---
layout: post
title: "Long-form video representation learning (Part 4: Sparse Transformers for video representation)"
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
