---
layout: post
title: "Long-form video representation learning (Part 3: Sparse Transformers for video representation)"
date: 2024-04-16
permalink: /2024/04/16/longformvideoseries-part3.html
author: <a href="https://subarnatripathi.github.io/"> Subarna Tripathi </a>
excerpt: "Current video understanding systems accurately recognize patterns in short video clips, but fails to process a video content over a few seconds due to computation and memory bottleneck. We propose a video representation method based on a spatio-temporal graph learning (SPELL) to equip it with long-term reasoning ability... "  
---



Current video understanding systems accurately recognize patterns in short video clips. 
However, they fail to capture how the present connects to the past or future in a world of never-ending visual stimuli. 
Existing video architectures tend to hit computation or memory bottlenecks after processing only a few seconds of video content. 
So, how do we enable accurate and efficient long-term visual understanding? An important first step is to have a model that practically 
runs on long videos. To that end, we explore novel video represnetation learning methods that are equipped with long-form reasoning capability. 

This is part 3 focusing on sparse video-text transformers and a sneak peek to our current explorations. 
See <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part1.html"> Part I </a> on video as "object-centric" spatio-temporal graphs and <a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part2.html"> Part II </a> on video as temporal graphs for modeling several video understanding tasks. 
<a href="https://intelailabpage.github.io/2024/04/16/longformvideoseries-part4.html"> Part IV </a> is about how 
we are pushing the boundaries boundaries of long-form video representation learning which leads to context aggregation 
over 10X-50X longer time support by leveraging existing "short-form" foundation models.  



<p style='text-align: justify;'>
As a part of the summer internship project at Intel Labs, <a href="https://jerryyli.github.io/"> Yi Li </a>, explored on temporal modeling of video-text transformers. The first question we needed an answer for is that do video-text transformers learn to model temporal relationships across frames? 
We oberved that despite their immense capacity and the abundance of multimodal training data, recent video models show strong tendency towards frame-based spatial representations, while temporal reasoning remains largely unsolved. Next, we focused on identifying several key challenges in temporal learning of video-text transformers: the spatio-temporal trade-off from limited network size; the curse of dimensionality for multi-frame modeling; and the diminishing returns of semantic information by extending clip length. Guided by these findings, we propose <b>SViTT</b>, a sparse video-text architecture that performs multi-frame reasoning with significantly lower cost than naive transformers with dense attention. Analogous to graph-based networks, SViTT employs two forms of sparsity: edge sparsity that limits the query-key communications between tokens in self-attention, and node sparsity that discards uninformative visual tokens. Trained with a curriculum which increases model sparsity with the clip length, SViTT outperforms dense transformer baselines on multiple video-text retrieval and question answering benchmarks, with a fraction of computational cost. 

This work has been accepted for publication in upcoming CVPR 2023. 

<br>

![]({{ site.url }}{{ site.baseurl }}/images/pubpic/svitt2.png){: style="width: 400px; float: left; margin: 0px 10px"} 

Upon a closer investigation, we identify a few key challenges to incorporating multi-frame reasoning in video-language models. 
First, limited model size implies a trade-off between spatial and temporal learning (a classic example being 2D/3D convolutions in video CNNs. 
<!-- % Enhancing the temporal modeling of a video network often compromises its spatial modeling proficiency.  -->
For any given dataset, optimal performance requires a careful balance between the two.
Second, long-term video models typically have larger model sizes and are more prone to overfitting.  Hence, for longer term video models, it becomes more important to carefully allocate parameters and control model growth. 
Finally, even if extending the clip length improves the results, it is subject to diminishing returns since the amount of information provided by a video clip does not grow linearly with its sampling rate.  If the model size is not controlled, the computational increase may not justify the gains in accuracy. This is critical for transformer-based architectures, since self-attention mechanisms have a quadratic memory and time cost with respect to input length. In summary, model complexity should be adjusted adaptively, depending on the input videos, to achieve the best trade-off between spatial representation, temporal representation, overfitting potential, and complexity. 
Since existing video-text models
lack this ability, they either attain a suboptimal balance between spatial and temporal modeling, or do not learn meaningful temporal representations at all.  

<br>
we argue that video-text models should learn to allocate modeling resources to the video data.  Rather than uniformly extending the model to longer clips, the allocation of these resources to the relevant spatio-temporal locations of the video is crucial for efficient learning from long clips. For transformer models, this allocation is naturally performed by pruning redundant attention connections.
We then accomplish these goals by exploring transformer sparsification techniques. 



This motivates the introduction of a <i> Sparse Video-Text Transformer </i> SViTT inspired by graph models. As illustrated in Figure 1, SViTT treats video tokens as graph vertices, and self-attention patterns as edges that connect them. We design SViTT to pursue sparsity for both: 
<b> Node </b> sparsity reduces to identifying informative tokens (e.g., corresponding to moving objects or person in the foreground) and pruning background feature embeddings; <b>edge</b> sparsity aims at reducing query-key pairs in attention module while maintaining its global reasoning capability. 
<b>edge</b> sparsity aims at reducing query-key pairs in attention module while maintaining its global reasoning capability; <b> node </b> sparsity reduces to identifying informative tokens (e.g., corresponding to moving objects or person in the foreground) and pruning background feature embeddings.
To address the diminishing returns for longer input clips, we propose to train SViTT with <it>temporal sparse expansion</it>, a curriculum learning strategy that increases clip length and model sparsity, in sync, at each training stage. 

<br>

![]({{ site.url }}{{ site.baseurl }}/images/pubpic/svitt_qual.png){: style="width: 800px; float: left; margin: 0px 10px"} 

SViTT is evaluated on diverse video-text benchmarks from video retrieval to question answering, comparing to prior art and our own dense modeling baselines. First, we perform a series of ablation studies to understand the benefit of sparse modeling in transformers. Interestingly, we find that both nodes (tokens) and edges (attention) can be pruned drastically at inference, with a small impact on test performance. In fact, token selection using cross-modal attention improves retrieval results by 1% without re-training. Figure 2 shows that SViTT isolates informative regions from background patches to facilitate efficient temporal reasoning. 

<br>
We next perform full pre-training with the sparse models and evaluate their downstream performance. 
We observe that SViTT scales well to longer input clips, where the accuracy of dense transformers drop due to optimization difficulties.
On all video-text benchmarks, SViTT reports comparable or better performance than their dense counterparts with lower computational cost, outperforming prior arts including those trained with additional image-text corpora. 


<br>
<br>

To summarize, the key contributions of SViTT are: 1) a video-text architecture that unifies edge and node sparsity; 2) a sparse expansion curriculum for training on long video clips; and 3) empirical results that demonstrate its temporal modeling efficacy on video-language tasks.
This work was originally published in CVPR 2023. More details can be found <a href="http://svcl.ucsd.edu/projects/svitt/"> here </a>. 

Compared to original transformers, SViTT is 6-7 times more efficient, capable of 2X more context aggregation. 
Pre-training with SViTT improves accuracy SoTA on 5 benchmarks : retrieval, VideoQ&A


<br>

Presently, we are developing foundation models utilizing such sparse transformers for egocentric videos. Our SViTT-Ego model outperforms existing SOTA models such as EgoVLP on several downstream applications such as video multiple question answering (EgoMCQ). One such visual example is shown below. 

![]({{ site.url }}{{ site.baseurl }}/images/pubpic/egomcq-visuals.png){: style="width: 900px; float: left; margin: 0px 10px"} 

We are preparing to participate in the EgoVis workshop at CVPR with our SViTT-ego. More details coming soon. 
</p>


