---
layout: post
title: "Long-form video representation learning (Part 1: video as spatio-temporal graphs)"
date: 2024-04-16
permalink: /2024/04/16/longformvideoseries-part1.html
author: <a href="https://subarnatripathi.github.io/"> Subarna Tripathi </a>
excerpt: "Current video understanding systems accurately recognize patterns in short video clips, but fails to process a video content over a few seconds due to computation and memory bottleneck. We propose a video representation method based on a spatio-temporal graph learning (SPELL) to equip it with long-term reasoning ability... "  
---



Current video understanding systems accurately recognize patterns in short video clips. 
However, they fail to capture how the present connects to the past or future in a world of never-ending visual stimuli. 
Existing video architectures tend to hit computation or memory bottlenecks after processing only a few seconds of video content. 
So, how do we enable accurate and efficient long-term visual understanding? An important first step is to have a model that practically 
runs on long videos. To that end, we explore novel video represnetation learning methods that are equipped with long-form reasoning capability. 


This is part 1 focusing on video representation as a spatio-temporal graphs and how to learn light-weghts graph neural networks for several video understanding applications. See <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part2.html"> Part II </a> on video as temporal graphs for modeling additional video understanding tasks. 
<a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part3.html"> Part III </a> focuses on sparse video-text transformers and a sneak peek to our current explorations. <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part4.html"> Part IV </a> is about how 
we are pushing the boundaries boundaries of long-form video representation learning which leads to context aggregation 
over 10X-50X longer time support by leveraging existing "short-form" foundation models.  


# What is long-form reasoning and why #

As the computer vision community experienced the huge leap of success of image-based pattern recognition with deep learning models such as 
convolutions or transformers, it was natural to go beyond still images and explore video representation learning to address video understanding. Developing video understanding models required two equally important focus areas. First is a large scale video dataset and the second is the trainable backbone for extracting video features. No wonder creating finer-grained and temporally consistent annotations for videos is one of the most challenging problems despite of the best intention from both the system designer as well as the annotators. Naturally, the large video datasets that were created, took the relatively easier way of annotating at the whole video label. About the second focus area, again it was natural to extend image-based models (such as CNN or transformers) for videos since videos are perceived as a collection of video frames each of them is identical in size and shape that of an image. Researchers needed to make their models which take input of sampled frames for ovbious memory constraint. To put things into perspective, when analyzing content from a 5-minute video clip at 30 frames/second, we need to process a bundle of 9,000 video frames. None of the existing models utilizing 3D CNN or Transformers can operate on a sequence of 9,000 frames as a single processing unit if dense computations involve even 16x16 rectangular patches at each frame. 
Most models operate in the following way. They take a short video clip as an input, do prediction, followed up temporal smoothing as opposed to the ideal scenarion where we want to model to look at the video in its entirety. 

Now, comes this question. If we need to know whether a video is of type swimming vs tennis, do we really need a minute-worth content? The answer is most certainly NO. Meaning the models optimized for video recognition, learned to look at background and other spatial context information instead of learning to reason over what is actually happening in a long video. We can term this phenomenon as a spatial shortcuts. These models were good for video recognition tasks in general. Can you guess how do these model generalize for other tasks that require temporal reasoning such as action forecasting, video question-answering, and recently proposed episodic memory tasks? Again, the answer is ovbious since they weren't trained for doing temporal reasoning, they aren't good for those applications. So we understand that datasets / annotations prevented most video models to learn temporal reasoning. Gradually, researchers realized this problem and started coming up with different benchmarks addressing long-form reasoning. However, one problem still persisted which was mostly memory-bound - how do we even make the first practical stride where a model can take a long-video as input as opposed to a sequence of short-clips processed one after another.  


# Our approach of video as spatio-temporal graph #

![]({{ site.url }}{{ site.baseurl }}/images/pubpic/spell.png){: style="width: 550px; float: left; margin: 0px 10px"} 
we propose a novel video representation method based on Spatio-Temporal Graphs Learning (SPELL) to equip it with long-term reasoning capability. 

