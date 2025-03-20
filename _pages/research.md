---
title: "Intel AI Lab - Research"
layout: textlay
excerpt: "Intel AI Lab -- Research"
sitemap: false
permalink: /research/
---

# Research #

We are a group of machine learning researchers working on “Multi-modal, Complex reasoning systems at Scale”. 
For `foundation model optimization`, we continued to expand `GEARBox`, our suite of techniques for optimizing the compute and memory requirements of large-scale foundation models. We also developed AFLORA, a novel parameter-efficient fine-tuning method for `LLMs`. We do research on inference-efficiency of large models, be it Transformer-based models or recurrent models such as MAMBA. We worked on `long-form` video representation research using sparse transformers and graphs and produced state-of-the-art results on several benchmarks. We innovate in video-llm space for improved temporal understanding.  
We do advanced research on AI for chip design. Finally, we are accelerating and democratizing AI for science - focusing on new benchmarks and tools for Material Science and Protein Synthesis.
We built one of the `first foundation models` for `graphs and geometric deep learning`: graph node classification, knowledge graph reasoning; we devise the fastest billion-scale graph learning platforms. 

Here are some themes and techniques that we currently work on:

### Long-Form Video Representation Learning. ### 
![]({{ site.url }}{{ site.baseurl }}/images/respic/long-form-video.png){: style="width: 250px; float: left; margin: 0px 10px"} 
<!-- Current video understanding systems often can precisely recognize patterns in short video clips. However, they fail to capture how the present connects to the past or future in a world of never-ending visual stimuli. Existing video architectures tend to hit computation or memory bottlenecks after processing only a few seconds of video content. So, how do we enable accurate and efficient long-term visual understanding? An important first step is to have a model that practically runs on long videos. To that end, we propose a novel video representation method based on Spatio-Temporal Graphs Learning (SPELL) to equip it with long-term reasoning capability. This structured video representation lets processing of ~1 minute content of video in contrast to the existing transformer-based or CNN-based models that can only look up to~10 seconds window.
    In a parallel thread of research, we identify why existing video transformer models show strong tendency towards frame-based spatial representations while temporal reasoning remains largely unsolved. We identify several key challenges in temporal learning of video-text transformers. Guided by our findings, we propose SViTT [2], a sparse video-text architecture that performs multi-frame reasoning with significantly lower cost than naive transformers with dense attention. Analogous to graph-based networks, SViTT employs two forms of sparsity: edge sparsity that limits the query-key communications between tokens in self-attention, and node sparsity that discards uninformative visual tokens. We show that SViTT outperforms dense transformer baselines on multiple video-text retrieval and question answering benchmarks, with a fractional computational cost. -->

We push the boundaries of long-form video representation learning, devising architectural motifs which leads to context aggregation over 10X-50X longer time support compared to existing methods. We take the approach of sparse models, either by explicitly modeling videos as a spatio-temporal graph or by learning sparse video-text transformers. 
Our method achieves state-of-the-art results at a fraction of the memory and compute cost of dense transformers. On a wide range of settings, the longer temporal support enabled by the novel representations consistently increases accuracy. They outperform on several downstream applications and benchmarks including but not limited to video recognition, video question-answering, episodic memory tasks, active speaker detection, action detection, temporal segmentation, multimodal retrieval, keystep recognition, and video summarization. 

Refer to the <a href="https://towardsdatascience.com/long-form-video-representation-learning-part-1-video-as-graphs-c55b609d9100"> 3-series TDS blog </a> to know more about this project. With a focus on open research, we established Intel Labs as a thoughtleader for video and multimodal foundation models; we published heavily on prestigious AI venues; be at top-positions on leadersboards targeting several different video understanding applications.  

We do research on making Video-llms more accurate on temporal understanding tasks. We do so by harnessing grounded-object information into several SOTA Video-LLM models and show how the performance on several temporal understandings improve with minimal finetuning. We developed a training-free dense video-caption generator, VideoNarrator, which powers several internal and external usecases. We have developed a quality evaluation framework for video captioning evaluating several metrics including "reference-free" methods as well. Many exciting algorithms are being developed right now! We are looking forward to share those works with the world soon!   

### Foundation Model Optimization (FoMo). ###
The foundation model optimization research of AIL focuses on model architecture develpment, efficient fine-tuning, latency and/or throughput efficient inference methodologies. The borader goal is to support million scale tokens at limited compute and memory budget. In the model architecture development space, our research primarily focuses on sub-quadratic attention mechanisms. Towards that goal, our work SAL-ViT (ICCV 2023) presents an hybrid architecture having quadratic attention and sub-quadratic attentions at different layers based on their operational performance sensitivity. Refer to <a href="https://openaccess.thecvf.com/content/ICCV2023/papers/Zhang_SAL-ViT_Towards_Latency_Efficient_Private_Inference_on_ViT_using_Selective_ICCV_2023_paper.pdf"> the paper.

- Secondly, we have dedicated research efforts ongoing to advance the foundation model fine-tuning research for their efficient trainability on downstream task with limited data and resources (CVPR 2024, ICLR 2024). A recent work from our lab that maintains the current SoTA in PEFT is <a href="https://arxiv.org/pdf/2403.13269.pdf"> here.

- Lastly, to advance the LLM inference efficiency, we have recently collaborated on a multi-institution project, namely project GEAR (generative inference via approximation and error recovery). To know more about the project please refer to the <a href="https://github.com/opengear-project/GEAR"> project page.

- Other research in this thread includes data-free quantization for privacy preserving fine-tuning, foundation model applications in RTL design, robsutness vulnerability of efficient model deplyment. 

### Graph Foundation Models. ###
Foundation Models in language, vision, and audio have been among the primary research topics in Machine Learning in 2024 whereas FMs for graph-structured data have somewhat lagged behind. We argue that the era of Graph FMs has already begun and developing algorithms and novel primitives for graph foundation models. 

For years, GNN-based node classifiers have been limited to a single graph dataset. We have developed GraphAny is, the first Graph FM where a single pre-trained model can perform node classification on any graph with any feature dimension and any number of classes. A single GraphAny model pre-trained on 120 nodes of the standard Wisconsin dataset successfully generalizes to 30+ other graphs of different sizes and features and, on average, outperforms GCN and GAT graph neural network architectures trained from scratch on each of those graphs. Please refer to this <a href="https://towardsdatascience.com/foundation-models-in-graph-geometric-deep-learning-f363e2576f58"> TDS blog </a> to know more about GraphAny. 

We developed ULTRA, a foundation model for knowledge graph (KG) reasoning. A single pre-trained ULTRA model performs link prediction tasks on any multi-relational graph with any entity / relation vocabulary. Performance-wise averaged on 50+ KGs, a single pre-trained ULTRA model is better in the 0-shot inference mode than many SOTA models trained specifically on each graph. Following the pretrain-finetune paradigm of foundation models, you can run a pre-trained ULTRA checkpoint immediately in the zero-shot manner on any graph as well as use more fine-tuning.
ULTRA provides unified, learnable, transferable representations for any KG. Under the hood, ULTRA employs graph neural networks and modified versions of NBFNet. ULTRA does not learn any entity and relation embeddings specific to a downstream graph but instead obtains relative relation representations based on interactions between relations. Refer to the <a href="https://github.com/DeepGraphLearning/ULTRA"> website </a> to learn more on our graph foundation model. 

Democratizing machine learning on billion-scale graphs is a core focus of Intel AI Lab. Our goal has been to shift this important AI training workload from expensive GPUs to inexpensive CPUs. Our <a href="https://github.com/IntelLabs/SAR"> SAR framework </a> already allows a seamless transition from training on a single machine to fully distributed training with linear peak-memory scaling guarantees - this set the fastest reported training times on CPUs for billion scale graph learning. 


### AI for Science. ###
We have been leading a variety of research efforts on AI for Science at Intel Labs along with external collaboration spanning various research institutions, including: 
- Matter Lab led by Alán Aspuru-Guzik at the University of Toronto <a href="https://www.intel.com/content/www/us/en/artificial-intelligence/podcast-episodes/intel-on-ai-season-3-episode-8.html"> Overview. </a>
- MILA, including multiple academic PIs <a href="https://medium.com/intel-tech/intel-and-mila-strengthen-their-open-innovation-commitment-to-responsible-ai-24412c576614"> Overview. </a>
- Intel + Merck Group Research Center on AI for Sustainable Semiconductor Manufacturing. <a href="https://www.emdgroup.com/en/news/semiconductor-manufacturing-09-03-2023.html"> Overview. </a>
- We organized the 1st AI for Accelerated Materials Design (AI4Mat) Workshop at NeurIPS 2022, followed by the next one at NeurIPS 2023. <a href="https://sites.google.com/view/ai4mat"> Overview. </a>

### AI for Chip Design. ###

Learning mechanisms for Electronic Design Automation (EDA) are increasingly becoming a focal point in research. These mechanisms hold the promise of delivering performance gains and quality improvements by orders of magnitude. Currently, our work is centered on the floor planning problem. We have developed solutions that outperform classical search solutions in both speed and quality. We extended our “human-quality floorplanner” to handle irregularly shaped rectilinear partitions instead of only rectangles. We also published FloorSet, the first ever large-scale open benchmark comprising more than 2M synthetic floorplan layouts that mimic the statistical distribution of real SOC floorplans and a range of real-world design constraints. 
