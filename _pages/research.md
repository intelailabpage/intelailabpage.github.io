---
title: "Intel AI Lab - Research"
layout: textlay
excerpt: "Intel AI Lab -- Research"
sitemap: false
permalink: /research/
---

# Research #

We are a group of machine learning researchers in the fields of reinforcement learning, robotics, computer vision, deep learning workload optimization and emerging applications.


Here are some themes and techniques that we currently work on:

### Long-term video understanding. ### 
![]({{ site.url }}{{ site.baseurl }}/images/respic/spell.png){: style="width: 250px; float: left; margin: 0px 10px"} 
<!-- Current video understanding systems often can precisely recognize patterns in short video clips. However, they fail to capture how the present connects to the past or future in a world of never-ending visual stimuli. Existing video architectures tend to hit computation or memory bottlenecks after processing only a few seconds of video content. So, how do we enable accurate and efficient long-term visual understanding? An important first step is to have a model that practically runs on long videos. To that end, we propose a novel video representation method based on Spatio-Temporal Graphs Learning (SPELL) to equip it with long-term reasoning capability. This structured video representation lets processing of ~1 minute content of video in contrast to the existing transformer-based or CNN-based models that can only look up to~10 seconds window.
    In a parallel thread of research, we identify why existing video transformer models show strong tendency towards frame-based spatial representations while temporal reasoning remains largely unsolved. We identify several key challenges in temporal learning of video-text transformers. Guided by our findings, we propose SViTT [2], a sparse video-text architecture that performs multi-frame reasoning with significantly lower cost than naive transformers with dense attention. Analogous to graph-based networks, SViTT employs two forms of sparsity: edge sparsity that limits the query-key communications between tokens in self-attention, and node sparsity that discards uninformative visual tokens. We show that SViTT outperforms dense transformer baselines on multiple video-text retrieval and question answering benchmarks, with a fractional computational cost. -->

We propose a novel video representation method based on sparse spatio-temporal graphs which leads to context aggregation over 10X longer time support.
This method shows that graph-centric architectures can achieve state-of-the-art results at a fraction of the memory and compute cost of transformers.
On a wide range of settings, the longer temporal support enabled by the graph-based representations consistently increases recognition accuracy.
Spatio-temporal learning achieves state-of-the-art results on the Active Speaker Detection task, competitive results on Action Detection tasks, and encouraging progress on other applications including event boundary detection, action localization, and temporal action segmentation. 

Refer to the <a href="https://community.intel.com/t5/Blogs/Tech-Innovation/Artificial-Intelligence-AI/Spatio-Temporal-Graphs-for-Long-Term-Video-Understanding/post/1425258#.Y1oG7jhUOBs.linkedin"> blog </a> we wrote for our research on structured representation learning for long-term video understanding. 




### Hardware-algorithm co-design. ###



### XYZ. ###
