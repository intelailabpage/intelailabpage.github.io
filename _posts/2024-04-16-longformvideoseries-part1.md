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

![]({{ site.url }}{{ site.baseurl }}/images/pubpic/spell.png){: style="width: 950px; float: left; margin: 0px 10px"} 
{: image-caption ="*Figure 1: (a): An illustration of our graph construction process. The frames above are temporally ordered from left to right. The three colors of blue, red, and yellow denote three identities that are present in the frames. Each node in the graph corresponds to each face in the frames. SPELL connects all the inter-identity faces from the same frame with the undirected edges. SPELL also connects the same identities by the forward/backward/undirected edges across the frames (controlled by a hyperparameter, τ) . In this example, the same identities are connected across the frames by the forward edges, which are directed and only go in the temporally forward direction. (b): The process for creating the backward and undirected graph is identical, except in the former case the edges for the same identities go in the opposite direction and the latter has no directed edge. Each node also contains the audio information which is not shown here.*"}


## Tasks formulated as node classification : Active Speaker Detection ##

We propose a novel video representation method based on Spatio-Temporal Graphs Learning (SPELL) to equip it with long-term reasoning capability. 
Figure 1 illustrates an overview of our framework when used on an Active Speaker Detection (ASD) task. Taking the audio-visual data, we construct a multimodal graph and cast the ASD as a graph node classification task. First, we create a graph where the nodes correspond to each person within each frame, and the edges represent spatial or temporal relationships among them. Figure 2 shows a visualization of such a graph. The initial node features are constructed using simple and lightweight 2D convolutional neural networks (CNNs) instead of a complex 3D CNN or a transformer. Next, we perform binary node classification – active or inactive speaker – on this graph by learning a three-layer graph neural network (GNN) model each with a small number of parameters. In our framework, graphs are constructed specifically for encoding the spatial and temporal dependencies among the different facial identities. Therefore, the GNN can leverage this graph structure and model the temporal continuity in speech as well as the long-term spatial-temporal context, while requiring low memory and computation.  

The work on spatio-temporal graphs for active speaker detection has been accepted for publication at ECCV 2022. The manuscript can be found here and the code for Active Speaker Detection can be found here.

## Other applications ##
The ASD problem setup in Ava active speaker dataset has access to the labeled faces and labeled face tracks as input to the problem setup. That largely simplifies the construction of the graph in terms of identifying the nodes and edges. For other problems, such as Action Detection, where the ground truth object (person) locations and tracks are not provided, we use pre-processing to detect objects and object tracks, then utilize SPELL for the node classification problem. On average, we achieve ~90% sparse graphs; a key difference compared to visual transformer-based methods which rely on dense General Matrix Multiply (GEMM) operations. 

Our sparse GNNs allow us to (1) achieve slightly better performance than transformer-based models; (2) aggregate temporal context over 10x longer windows compared to transformer-based models (100s vs 10s); and (3) Achieve 2-5X compute savings compared to transformers-based methods.

# Highlights #

Opensourcing;
challenge winners;
4 applications already in the library;




