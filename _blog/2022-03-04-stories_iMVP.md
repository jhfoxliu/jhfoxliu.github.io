---
layout: post
title:  The iMVP project
date:   2022-03-7 01:00:00
description: A revolutionary by-product
tags: 
categories: story
---

The [`interactive epitranscriptomic Motif Visualization and Sub-type Partitioning (iMVP)`](https://github.com/jhfoxliu/iMVP) project is a by-product in my m5C studies. At the end of 2021, the days I was trying to set up a deep-learning based classifier for m5C sites, I was wondering about if I can know the composition of the input data of the k-mers sequences. So I tried to draw them on a 2D plane to visulize them. The direct way to do so is firstly converting the sequences into `one-hot` encoded ones, just like what we do in deep-learning. Then it is normal for us to use `UMAP` and other methods to project them. Most guys might stop here. With the labels, the problem should be already solved. But I noticed that, **if we can find out the regions on the 2D plane with higher densities, we can directly find the sequence patterns from the projections!** I hence began to find some `unsupervised clustering methods` to extract the clusters. I finally found the best partner for `UMAP` - the powerful density-based method `HDBSCAN`. With such a combination, I developed a lot of applications in RNA modification motif research. In practices, this framework exhibit ultra-high sensitivity and analysis capacity. I have finished an analysis of >500 million k-mers for >1500 million A-to-I editing sites. I guess this frame work can bring a revolution in the field.

I made an important decision in this project that everything should be transparent and clear. It is a good tendency that the academia is seeking for better reproducibility. We are now asked for more and more details about our experiments and analysis in the study. So why don't we make everything ready for that at the every beginning? I made a lot efforts about this:

1. I use `notebooks` rather than stand-alone `scripts` in this study. So that others can repeat my jobs easily and can preview the outputs.

2. I generate and store the raw data used for each plot in the analyses. So that I will no longer need to fetch everything before I sumbit my manuscript.

3. I try to prepare everything according to NPG's guideline.

4. I will try to set up a `container` of `Docker` to keep a stable enviroment.

<br/>

<br/>
<a href="/blog/"><u>Back</u></a>