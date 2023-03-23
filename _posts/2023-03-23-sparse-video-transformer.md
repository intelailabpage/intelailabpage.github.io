---
layout: post
title: "Temporal Learning of Sparse Video-Text Transformers"
date: 2023-03-23
permalink: /2023/03/23/sparse-video-transformers.html
author: <a href="https://subarnatripathi.github.io/"> Subarna Tripathi </a>
excerpt: "we propose SViTT, a sparse video-text architecture that performs multi-frame reasoning with significantly lower cost than naive transformers with dense attention. Analogous to graph-based networks, SViTT employs two forms of sparsity: edge sparsity that limits the query-key communications between tokens in self-attention, and node sparsity that discards uninformative visual tokens. Trained with a curriculum which increases model sparsity with the clip length, SViTT outperforms dense transformer baselines on multiple video-text retrieval and question answering benchmarks, with a fraction of computational cost.... "  
---


As a part of the summer internship project at Intel Labs, <a href="https://jerryyli.github.io/"> Yi Li </a>, explored on temporal modeling of video-text transformers. The first question we needed an answer for is that do video-text transformers learn to model temporal relationships across frames? 
We oberved that despite their immense capacity and the abundance of multimodal training data, recent video models show strong tendency towards frame-based spatial representations, while temporal reasoning remains largely unsolved. Next, we focused on identifying several key challenges in temporal learning of video-text transformers: the spatio-temporal trade-off from limited network size; the curse of dimensionality for multi-frame modeling; and the diminishing returns of semantic information by extending clip length. Guided by these findings, we propose <b>SViTT</b>, a sparse video-text architecture that performs multi-frame reasoning with significantly lower cost than naive transformers with dense attention. Analogous to graph-based networks, SViTT employs two forms of sparsity: edge sparsity that limits the query-key communications between tokens in self-attention, and node sparsity that discards uninformative visual tokens. Trained with a curriculum which increases model sparsity with the clip length, SViTT outperforms dense transformer baselines on multiple video-text retrieval and question answering benchmarks, with a fraction of computational cost. 

This work has been accepted for publication in upcoming CVPR 2023. Stay tuned for the full paper and the source code. 
<!-- Code is available at <a href="https://github.com/JerryYLi/svitt"> on GiHub </a>.  -->
<!-- Figure 1 shows the time support capability for SPELL vs other methods.  -->

