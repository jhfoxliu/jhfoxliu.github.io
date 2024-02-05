---
layout: page
title: Simple simulations
description: Boost studies with simple computations
img: assets/img/Simulations/cover.png
importance: 2
category: tools
---

As a technique, simulation should be an important paradigm that helps us predict the results before real experiments, and assist us to build an intution about how the real data should look like. If we can ponder before action, material and reagents can be save, and of course, less time to be waste. I was taught to simulate the genetic pattern of a population on my ***Population Genetics*** class, and it is famaliar to me to do some simulations. Here is a collection of my simulations. 

If you're interested in them, please **email me** for the codes.

### Simulate a plate

Human is not so good in handling the concept of `density` or `huge number`. For example, we are confused when the article states that 50,000 colonies per plate were harvested, or the density of bacteria should be ~200 per cm<sup>2</sup>.

Let's make it intutively within minutes. Simply use `random` and `matplotlib` in `Python`, we can generate the distributions of colonies on a 15-cm LB plate. And here is the simulation results. Much clear, right?

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-1">
        {% include figure.html path="assets/img/Simulations/plates.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    So that 50,000 colonies per plate means a density of ~283. We should not incubate the plates too long to prevent their conjunctions.
</div>

### Simulate a microwell

Same as plates, in microwell studies, we are hard to intutively learn the density of cells from a microscope vision. This trouble will make us hard to estimate the cell duplication rate before we obtain the sequencing data. Let's do the same thing!

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-1">
        {% include figure.html path="assets/img/Simulations/microwell_cells.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Based on Poison distribution, we should use a density of 10%-20% to avoid multiple cells in a well.
</div>

<br/>

<br/>
<a href="/projects/"><u>Back</u></a>
