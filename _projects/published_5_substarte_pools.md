---
layout: page
title: High throughput modification substrate assay
description: More oligos, please
img: assets/img/mutation_assay/cover.jpg
importance: 4
category: published
---

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-1">
        {% include figure.html path="assets/img/mutation_assay/mutation_assay_exp.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    The workflow of high-throughput mutation assay: we synthesized the oligos, inserted them into a vector, purify the library, transfect them into the cells, and get reporter methylation levels from sequencing.
</div>

This is not a new strategy. In a [previous paper](https://pubmed.ncbi.nlm.nih.gov/28073919/) studying pseudouridine, they adopt a same strategy to draw the consensus modification substrate of TRUB1. Here, we used pools to analyze the substrate recognition patterns of NSUN2 and NSUN6. A brief summary:

- NSUN2
  - NSUN2 requires a stable stem loop in the 3' downstream adjacent to the m5C sites.
  - More Gs in the stem loop will result in higher methylation levels, but G is not so necessary for methylation in some cases.
- NSUN6 
  - NSUN6 is very sensitive to the change in the core motif (Nm5CUCCA).
  - NSUN6 can tolerate some +3 C-to-U changes. 
  - The mechanism of preferences in NSUN6-mRNA recognition can be explained by our structure model.

<br/>

#### References

<div class="publications">
    {% bibliography -f assays %}
</div>

<br/>

<br/>
<a href="/projects/"><u>Back</u></a>
