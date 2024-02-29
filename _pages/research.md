---
title: "Intel AI Lab - Research"
layout: textlay
excerpt: "Intel AI Lab -- Research"
sitemap: false
permalink: /research/
---

# Research #

We are a group of machine learning researchers working on “Foundational AI Research at Scale”. We build one of the fastest billion-scale graph learning platforms, and one of the first foundation models for knowledge graph reasoning. We are working on “long-form” video understanding research using sparse transformers and graphs and producing state-of-the-art on many academic benchmarks. We do forefront research on efficient multimodal generative AI including fastest NeRF in the wild. We do advanced research on AI for chip design and deep learning workload optimization. Finally, we are accelerating and democratizing AI for science - focusing on new benchmarks and tools for Material Science and Protein Synthesis.



Here are some themes and techniques that we currently work on:

### Long-Form Video Representation Learning. ### 
![]({{ site.url }}{{ site.baseurl }}/images/respic/long-form-video.png){: style="width: 250px; float: left; margin: 0px 10px"} 
<!-- Current video understanding systems often can precisely recognize patterns in short video clips. However, they fail to capture how the present connects to the past or future in a world of never-ending visual stimuli. Existing video architectures tend to hit computation or memory bottlenecks after processing only a few seconds of video content. So, how do we enable accurate and efficient long-term visual understanding? An important first step is to have a model that practically runs on long videos. To that end, we propose a novel video representation method based on Spatio-Temporal Graphs Learning (SPELL) to equip it with long-term reasoning capability. This structured video representation lets processing of ~1 minute content of video in contrast to the existing transformer-based or CNN-based models that can only look up to~10 seconds window.
    In a parallel thread of research, we identify why existing video transformer models show strong tendency towards frame-based spatial representations while temporal reasoning remains largely unsolved. We identify several key challenges in temporal learning of video-text transformers. Guided by our findings, we propose SViTT [2], a sparse video-text architecture that performs multi-frame reasoning with significantly lower cost than naive transformers with dense attention. Analogous to graph-based networks, SViTT employs two forms of sparsity: edge sparsity that limits the query-key communications between tokens in self-attention, and node sparsity that discards uninformative visual tokens. We show that SViTT outperforms dense transformer baselines on multiple video-text retrieval and question answering benchmarks, with a fractional computational cost. -->

We push the boundaries of long-form video representation learning, devising architectural motifs which leads to context aggregation over 10X-50X longer time support compared to existing methods. We take the approach of sparse models, either by explicitly modeling videos as a spatio-temporal graph or by learning sparse video-text transformers. 
Our method achieves state-of-the-art results at a fraction of the memory and compute cost of dense transformers. On a wide range of settings, the longer temporal support enabled by the novel representations consistently increases accuracy. They outperform on several downstream applications and benchmarks including but not limited to video recognition, video question-answering, episodic memory tasks, active speaker detection, action detection, temporal segmentation, multimodal retrieval, and video summarization. 

Refer to the <a href="https://community.intel.com/t5/Blogs/Tech-Innovation/Artificial-Intelligence-AI/Spatio-Temporal-Graphs-for-Long-Term-Video-Understanding/post/1425258#.Y1oG7jhUOBs.linkedin"> blog </a> we wrote for our research on structured representation learning for long-term video understanding. We opensourced the <a href="https://github.com/IntelLabs/GraVi-T"> toolbox </a> for graph-based video representation learning.  

Refer to the <a href="http://svcl.ucsd.edu/projects/svitt/"> website </a> to learn more on sparse video-text transformers. 


### Graph Foundation Models. ###
We developed ULTRA, a foundation model for knowledge graph (KG) reasoning. A single pre-trained ULTRA model performs link prediction tasks on any multi-relational graph with any entity / relation vocabulary. Performance-wise averaged on 50+ KGs, a single pre-trained ULTRA model is better in the 0-shot inference mode than many SOTA models trained specifically on each graph. Following the pretrain-finetune paradigm of foundation models, you can run a pre-trained ULTRA checkpoint immediately in the zero-shot manner on any graph as well as use more fine-tuning.

ULTRA provides unified, learnable, transferable representations for any KG. Under the hood, ULTRA employs graph neural networks and modified versions of NBFNet. ULTRA does not learn any entity and relation embeddings specific to a downstream graph but instead obtains relative relation representations based on interactions between relations.

Refer to the <a href="https://github.com/DeepGraphLearning/ULTRA"> website </a> to learn more on our graph foundation model. 

### AI for Science. ###
We have been leading a variety of research efforts on AI for Science at Intel Labs along with external collaboration spanning various research institutions, including: 
- Matter Lab led by Alán Aspuru-Guzik at the University of Toronto (https://www.intel.com/content/www/us/en/artificial-intelligence/podcast-episodes/intel-on-ai-season-3-episode-8.html)
- MILA, including multiple academic PIs (https://medium.com/intel-tech/intel-and-mila-strengthen-their-open-innovation-commitment-to-responsible-ai-24412c576614)
- Intel + Merck Group Research Center on AI for Sustainable Semiconductor Manufacturing (https://www.emdgroup.com/en/news/semiconductor-manufacturing-09-03-2023.html)
Organizer of the 1st AI for Accelerated Materials Design (AI4Mat) Workshop at NeurIPS 2022 (https://sites.google.com/view/ai4mat)

### AI for Chip Design. ###

Learning mechanisms for Electronic Design Automation (EDA) are increasingly becoming a focal point in research. These mechanisms hold the promise of delivering performance gains and quality improvements by orders of magnitude. Currently, our work is centered on the floor planning problem. We have developed solutions that outperform classical search solutions in both speed and quality.

### Deep learning workload optimization. ###
