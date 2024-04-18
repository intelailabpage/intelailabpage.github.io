---
layout: post
title: "Long-form video representation learning (Part 2: video as temporal graphs)"
date: 2024-04-16
permalink: /2024/04/16/longformvideoseries-part2.html
author: <a href="https://subarnatripathi.github.io/"> Subarna Tripathi </a>
excerpt: "Current video understanding systems accurately recognize patterns in short video clips, but fails to process a video content over a few seconds due to computation and memory bottleneck. We propose a video representation method based on a spatio-temporal graph learning (SPELL) to equip it with long-term reasoning ability... "  
---



Current video understanding systems accurately recognize patterns in short video clips. 
However, they fail to capture how the present connects to the past or future in a world of never-ending visual stimuli. 
Existing video architectures tend to hit computation or memory bottlenecks after processing only a few seconds of video content. 
So, how do we enable accurate and efficient long-term visual understanding? An important first step is to have a model that practically 
runs on long videos. To that end, we explore novel video represnetation learning methods that are equipped with long-form reasoning capability. 

This is part 2 focusing on video representation as a temporal graph and how to learn light-weights graph neural networks for several video 
understanding applications. See <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part1.html"> Part I </a> on video as "object-centric" spatio-temporal graphs for modeling additional video understanding tasks. 
<a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part3.html"> Part III </a> focuses on sparse video-text transformers and a sneak peek to our current explorations. <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part4.html"> Part IV </a> is about how we are pushing the boundaries boundaries of long-form video representation learning which leads to context aggregation 
over 10X-50X longer time support by leveraging existing "short-form" foundation models.  


# Video as a temporal graph #

Let G = (V, E) be a graph with the node set V and edge set E. For domains such as social networks, citation networks, and molecular structure, the V and E are available to the system, and we say the graph is given as an input to the learnable models. Now, let’s consider the simplest possible case in a video where each of the video frame is considered a node leading to the formation of V. However, it is not clear whether and how node t1 (frame at time=t1) and node t2 (frame at time=t2) are connected. Thus, the set of edges, E, is not provided. Without E, the topology of the graph is not complete resulting into unavailability of the “ground truth” graphs. One of the most important challenges remains how to convert a video to a graph. This graph can be considered as a latent graph since there is no such labeled (or “ground truth”) graph available in the dataset.

When a video is modeled as a temporal graph, many video understanding problems can be formulated as either node classification or graph classification problems. We utilize a SPELL framework for other tasks in video understanding such as Action Boundary Detection, Temporal Action Segmentation, Video summarization / highlight reels detection. Very recently, we are working on utilizing the same framework for leveraging correlation across multiple view for other video understanding tasks. Watch out for our updates on new applications using GraVi-T. 


