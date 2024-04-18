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


This is part 1 focusing on video representation as "object-centric" spatio-temporal graphs and how to learn light-weghts graph neural networks for several video understanding applications. See <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part2.html"> Part II </a> on video as temporal graphs for modeling additional video understanding tasks. 
<a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part3.html"> Part III </a> focuses on sparse video-text transformers and a sneak peek to our current explorations. <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part4.html"> Part IV </a> is about how 
we are pushing the boundaries boundaries of long-form video representation learning which leads to context aggregation 
over 10X-50X longer time support by leveraging existing "short-form" foundation models.  


# What is long-form reasoning and why #

As we saw the huge leap of success of image-based understanding tasks with deep learning models such as 
convolutions or transformers, it was natural to go beyond still images and explore video video understanding. Developing video understanding models require two equally important focus areas. First is a large scale video dataset and the second is the learnable backbone for extracting video features. Creating finer-grained and consistent annotations for a dynamic signal such as a video is not trivial even with the best intention from both the system designer as well as the annotators. Naturally, the large video datasets that were created, took the relatively easier way of annotating at the whole video label. About the second focus area, again it was natural to extend image-based models (such as CNN or transformers) for video understanding since videos are perceived as a collection of video frames each is identical in size and shape of an image. Researchers made their models that use sampled frames as inputs as opposed to all the video frames for ovbious memory budget. To put things into perspective, when analyzing a 5-minute video clip at 30 frames/second, we need to process a bundle of 9,000 video frames. Neither CNN nor Transformers can operate on a sequence of 9,000 frames as a whole if it involves dense computations at the level of 16x16 rectangular patches corresponding to each frame. 
Thus most models operate in the following way. They take a short video clip as an input, do prediction, followed up temporal smoothing as opposed to the ideal scenario where we want the model to look at the video in its entirety. 

Now comes this question. If we need to know whether a video is of type 'swimming' vs 'tennis', do we really need to analyze a minute-worth content? The answer is most certainly NO. In other words, the models optimized for video recognition, most likely learned to look at background and other spatial context information instead of learning to reason over what is actually happening in a 'long' video. We can term this phenomenon as learning the spatial shortcut. These models were good for video recognition tasks in general. Can you guess how do these model generalize for other tasks that require actual temporal reasoning such as action forecasting, video question-answering, and recently proposed episodic memory tasks? Not at all surprising that there is a lot of room for improvement. since they weren't trained for doing temporal reasoning, they aren't good for those applications. So we understand that datasets / annotations prevented most video models to learn temporal reasoning. Gradually, researchers realized this problem and started coming up with different benchmarks addressing long-form reasoning. However, one problem still persisted which was mostly memory-bound i.e. how do we even make the first practical stride where a model can take a long-video as input as opposed to a sequence of short-clips processed one after another.  


# Video as "object-centric" spatio-temporal graph #

![spell-asd-overall]({{ site.url }}{{ site.baseurl }}/images/pubpic/spell-asd-overall.png){: style="width: 950px; float: left; margin: 0px 10px"} 
*Figure 1: We convert a video into a canonical graph from the audio-visual input data, where each node corresponds to a person in a frame, and an edge represents a spatial or temporal interaction between the nodes. The constructed graph is dense enough for modeling long-term dependencies through message passing across the temporally-distant but relevant nodes, yet sparse enough to be processed within low memory and computation budget. The ASD task is posed as a binary node classification in this long-range spatial-temporal graph.*


### Tasks formulated as node classification : Active Speaker Detection ###

We propose a novel video representation method based on Spatio-Temporal Graphs Learning (SPELL) to equip it with long-term reasoning capability. 
Figure 1 illustrates an overview of our framework designed for Active Speaker Detection (ASD) task. With the audio-visual data as input, we construct a multimodal graph and cast the ASD as a graph node classification task. Figure 2 demonstrates the graph construction process. 
First, we create a graph where the nodes correspond to each person within each frame, and the edges represent spatial or temporal relationships among them. The initial node features are constructed using simple and lightweight 2D convolutional neural networks (CNNs) instead of a complex 3D CNN or a transformer. Next, we perform binary node classification i.e. active or inactive speaker – on each node of this graph by learning a light-weight three-layer graph neural network (GNN). In our framework, graphs are constructed specifically for encoding the spatial and temporal dependencies among the different facial identities. Therefore, the GNN can leverage this graph structure and model the temporal continuity in speech as well as the long-term spatial-temporal context, while requiring low memory and computation. 
We perform extensive experiments on the AVA-ActiveSpeaker dataset. Our results show that SPELL outperforms all previous state-of-the-art (SOTA) approaches. Thanks to ~95% sparsity of the constructed graphs, SPELL requires significantly less hardware resources for the visual feature encoding (11.2M #Params) compared to ASDNet (48.6M #Params), one of the leading state-of-the-art methods of that time.

![spell-asd]({{ site.url }}{{ site.baseurl }}/images/pubpic/spell-asd.png){: style="width: 950px; float: left; margin: 0px 10px"} 
*Figure 2: (a): An illustration of our graph construction process. The frames above are temporally ordered from left to right. The three colors of blue, red, and yellow denote three identities that are present in the frames. Each node in the graph corresponds to each face in the frames. SPELL connects all the inter-identity faces from the same frame with the undirected edges. SPELL also connects the same identities by the forward/backward/undirected edges across the frames (controlled by a hyperparameter, τ) . In this example, the same identities are connected across the frames by the forward edges, which are directed and only go in the temporally forward direction. (b): The process for creating the backward and undirected graph is identical, except in the former case the edges for the same identities go in the opposite direction and the latter has no directed edge. Each node also contains the audio information which is not shown here.*

### Long-term temporal context ###
The hyperparameter τ (= 0.9 second in our experiments) in SPELL imposes additional constraints on direct connectivity across temporally distant nodes. The face identities across consecutive timestamps are always connected. Below is the estimate of the effective temporal context size of SPELL. The AVA-ActiveSpeaker dataset contains 3.65 million frames and 5.3 million annotated faces, resulting in 1.45 faces per frame. Averaging 1.45 faces per frame, a graph with 500 to 2000 faces in sorted temporal order can span 345 to 1379 frames, corresponding to anywhere between 13 and 55 seconds for a 25 frame/second video. In other words, the nodes in the graph might have a time difference of about 1 minute, and SPELL is able to effectively reason over that long-term temporal window within a limited memory and compute budget. It is noteworthy that the temporal window size in <a href="https://openaccess.thecvf.com/content/ICCV2021/papers/Alcazar_MAAS_Multi-Modal_Assignation_for_Active_Speaker_Detection_ICCV_2021_paper.pdf"> MAAS </a> is 1.9 seconds and TalkNet uses up to 4 seconds as long-term sequence-level temporal context.

The work on spatio-temporal graphs for active speaker detection has been published at ECCV 2022. The manuscript can be found <a href="https://link.springer.com/chapter/10.1007/978-3-031-19833-5_22"> here </a>. 
In an earlier <a href="https://community.intel.com/t5/Blogs/Tech-Innovation/Artificial-Intelligence-AI/Spatio-Temporal-Graphs-for-Long-Term-Video-Understanding/post/1425258#.Y1oG7jhUOBs.linkedin"> blog </a> we provided more details. 


![spell-time-support]({{ site.url }}{{ site.baseurl }}/images/pubpic/spell-time-support.png){: style="width: 950px; float: left; margin: 0px 10px"} 
*Figure 3: Left and right figure demonstrate the compartive time-support of our method compared to others for Active Speaker Detection and Action Detection applications, respectively.*

### Other applications ###
The ASD problem setup in Ava active speaker dataset has access to the labeled faces and labeled face tracks as input to the problem setup. That largely simplifies the construction of the graph in terms of identifying the nodes and edges. For other problems, such as Action Detection, where the ground truth object (person) locations and tracks are not provided, we use pre-processing to detect objects and object tracks, then utilize SPELL for the node classification problem. On average, we achieve ~90% sparse graphs; a key difference compared to visual transformer-based methods which rely on dense General Matrix Multiply (GEMM) operations. Our sparse GNNs allow us to (1) achieve slightly better performance than transformer-based models; (2) aggregate temporal context over 10x longer windows compared to transformer-based models (100s vs 10s); and (3) Achieve 2-5X compute savings compared to transformers-based methods.

### GraVi-T: Open Source Software Library ###
We have open-sourced our software library, GraVi-T. At present, GraVi-T supports multiple video understanding applications, including Active Speaker Detection, Action Detection, Temporal Segmentation, Video Summarization. See our post on <a href="https://intelailabpage.github.io/2023/03/29/gravi-t.html"> GraVi-T </a> to more on the applications. 

# Highlights #
Compared to transformers, our "object-centric" spatio-temporal graph approach can aggregate context over 10x longer video (as shown in Figure 3), consumes ~10x lower memory and 5x lower FLOPs.

Our approach of modeling video as a sparse graph outperformed complex SOTA methods on several applications. It secured top places in multiple leaderboards using this active speaker detection framework. The list includes ActivityNet 2022, Ego4D audio-video diarization challenge at ECCV 2022, CVPR 2023. 








