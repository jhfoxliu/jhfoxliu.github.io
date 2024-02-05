---
layout: page
title: Taiyaki and mRNA m5C
description: Retraining a Nanopore model
img: assets/img/Taiyaki/cov.jpg
importance: 998
category: trials
---

[`Taiyaki`](https://github.com/nanoporetech/taiyaki) is a model-retraining algorithm developed by `Oxford Nanopore`. This software is very useful in re-train Nanopore models from raw signals to recognize modified bases.

It a very interesting experience for me to seek for a Nanopore model can decipher mRNA m5C directly. In our hands, we used modified and unmodified *in vitro* transcripts to construct the training set, then process them to `Taiyaki`. Unfortunately, we found that the model was easily overfit.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-1">
        {% include figure.html path="assets/img/Taiyaki/res.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Seems good, but no m5C site was found correctly in the real data.
</div>

<br/>

<br/>
<a href="/projects/"><u>Back</u></a>