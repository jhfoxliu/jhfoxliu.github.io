---
layout: page
title: mRNA BS-seq pipeline and NSUN2
description: We still don't know the function and mechanism behind it
img: assets/img/m5C_pipeline/cover.jpg
importance: 3
category: published
---

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/m5C_pipeline/NSMB.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    The schema of our optimized workflow.
</div>

### In breif

- We optimized the experimental protocol to improve the conversion rates in mRNA BS-seq.
- We analyzed the pattern of artifacts in BS-seq and located the source of false positives.
- We introduced `Gini-index` and `signal-nosie ratio` into analysis to estimate the status of library conversion.
- We introduced `C-cutoff` and `gene-specific conversion rates` into our filter to remove false positives.
- We set up a [`new pipeline`](https://github.com/jhfoxliu/RNA-m5C) with high flexibility, robustness and parallelization level for mRNA BS-seq.
- We validated that NSUN2 is one of the major m5C methyltransferase acting on mRNA.
- We profile mRNA landscapes in multiple human/mouse tissues.
- mRNA m5C might relate to translation control.

<br/>

### Where are the noise?

It's clear now that the noise in BS-seq come from many places:

1. The human-introduced Cs in hexamer.
2. The regions hard to be converted, especially some highly structured rRNA regions.
3. The false alignments and bases with bad sequencing qualities.

<br/>

### Solutions

The pipeline I designed have considered most of the situations:

1. Hexamer can be removed by trimming the bases at the end of reads.
2. We should use `gene-specific` conversion rates rather than a `global conversion rate` measured by spike-ins or the whole libray. Only analyze annotated regions.
3. Estimate the conversion status by `Gini-index` and `signal-nosie ratio`, and determine the `C-cutoff` that remove reads have more than a certain number of reads.
4. Optimize the alignment step to reduce false alignments. Normally, that should not be a matter.
5. SNPs can only **destory** m5C, but cannot create m5C in BS-seq.
6. Statistical tests have little effect on our analysis if we use a filter with high coverage and level.

In my hands, I guess we can let the sites with 5% methylation go, but we normally use a 10% cutoff for the biological importance of a site. BS-seq is very sensitive and reliable if you work with it correctly.

<br/>

<div class="row mt-3">
    <div class="col-sm mt-2 mt-md-0">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="assets/img/m5C_pipeline/GeneSpecific conversion.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <div class="row mt-1">
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.html path="assets/img/m5C_pipeline/gini.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
            </div>
        </div>
        <div class="row mt-1">
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.html path="assets/img/m5C_pipeline/C-cutoff_signal.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
            </div>
        </div>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/m5C_pipeline/steps.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    left, why gene-specific conversion rates are important; middle, gini-index vs signal rates in badly converted samples and well converted samples. And some examples for true positives and false positives; right, our filters can work perfectly!
</div>

<br/>

#### References

<div class="publications">
    {% bibliography -f nsun2 %}
</div>

<br/>

<br/>
<a href="/projects/"><u>Back</u></a>

