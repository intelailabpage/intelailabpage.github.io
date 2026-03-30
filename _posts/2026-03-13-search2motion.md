---
layout: post
title: "Search2Motion"
date: 2026-03-13
permalink: /2026/03/13/search2motion.html
author: <b> Sainan Liu, Tz-Ying Wu, Hector A Valdez, Subarna Tripathi </b>  
excerpt: "We present a training-free approach for image-to-video generation that enables object-level motion control under a stable camera ... "
permalink: /2026/03/13/search2motion.html
---
<p>
    <a href="https://arxiv.org/abs/2603.16711"> [arXiv] </a>
</p>



<h3>
Search2Motion Overview: 
</h3>
<div class="text">
<p>
We present Search2Motion, a training-free framework for object-level motion editing in image-to-video generation. Unlike prior methods requiring trajectories, bounding boxes, masks, or motion fields, Search2Motion adopts target-frame-based control, leveraging first-last-frame motion priors to realize object relocation while preserving scene stability without fine-tuning. Reliable target-frame construction is achieved through semantic-guided object insertion and robust background inpainting. We further show that early-step self-attention maps predict object and camera dynamics, offering interpretable user feedback and motivating ACE-Seed (Attention Consensus for Early-step Seed selection), a lightweight search strategy that improves motion fidelity without look-ahead sampling or external evaluators. Noting that existing benchmarks conflate object and camera motion, we introduce S2M-DAVIS and S2M-OMB for stable-camera, object-only evaluation, alongside
FLF2V-Obj metrics that isolate object artifacts without requiring ground-truth trajectories. Search2Motion consistently outperforms baselines on FLF2V-Obj and VBench. 
</p>

<h3> Search2Motion: Training-Free Pipeline and User Interface </h3>
<style>
    img {
        max-width:100%;
        height: auto;
    }
</style>
<img src="/images/pubpic/edit2motion.png" >


<p>
The Search2Motion Pipeline is constructed with three components, where the user can interact with the application at stage 1 (Background Inpainting) and stage 2 (Object Placement). Then the original input image and the user-edited last frame are sent to a
first-frame last-frame (FFLF) video generator to acquire the final video generated based on the given input image and user preference</p>



<h3> Search2Video Overview: </h3>  
<p>
This short video describes the core idea and the overall pipeline. 
</p>  
<iframe width="1100" height="550" src="https://www.youtube.com/embed/Pec3Anpbnz0" frameborder="0" allowfullscreen></iframe> 



<h3> Demo 1: </h3>  
<p>
The following screen capture shows the steps: user starts with the first frame, then just a click on the chitah to automatically get the segmented chitah and an impainted background. Next the user automatically receives a visually grounded signal about where the Chitah can move. Once the user places the Chitah anywhere in the suggested area, the last frame of the video gets created. Next, the first-frame last-frame guided video generation happens in the final step. For the sake of easier visualization, we have captured everything running in real-time except for object insertion and video generation which takes about 2 minutes to complete. 
</p>  
<iframe width="1100" height="550" src="https://www.youtube.com/embed/CeCGk8VbDGQ" frameborder="0" allowfullscreen></iframe> 



<h3> Demo 2: </h3>  
<p>
Next demo shows a bird flying animation generated using the pipeline. Note how the object motion is rendered realistic while the background changes from plain sky to the birdeye view of the scene below.  
</p>  
<iframe width="1100" height="550" src="https://www.youtube.com/embed/xHps4qeldyw" frameborder="0" allowfullscreen></iframe> 


<h3> Demo 3: </h3>  
<p>
The last demo shows a dynamic scene under the sea. 
</p>  
<iframe width="1100" height="550" src="https://www.youtube.com/embed/m5BS4BVGPA0" frameborder="0" allowfullscreen></iframe> 


