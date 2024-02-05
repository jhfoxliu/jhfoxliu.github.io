---
layout: page
title: SJM+ and my wrapper
description: SJM is the best cluster manager I have work with
img: assets/img/SJM/SJM.jpg
importance: 1
category: tools
---

[`Simple Job Manager (SJM)`](https://github.com/StanfordBioinformatics/SJM) is a wrapper of `Sun Grid Engine (SGE)`, developed by Stanford SCGPM Bioinformatics.

SJM is a super powerful software that enables us to split a run into several sections. For each section, the `standard outputs` and `standard errors` are recorded into separated files with timestamps, so that the users can easily manage their jobs. This is very important for the users to efficiently pick up a small piece of logs from the numerous outputs, and esepcaially essential for the users to find bugs in their test pipeline. SJM also has friendly coding style that close to the native shell. <sub> I guess the only one drawback is from the deployment of SGE, which never succeeded in my hands...</sub>

{% raw %}
```shell
[liujh@master logs]$ ll -thr
total 60K
-rw-r--r-- 1 liujh zhanglab  18K Feb  1  2020 QC_o200201140112.txt
-rw-r--r-- 1 liujh zhanglab  451 Feb  1  2020 QC_e200201140112.txt
-rw-r--r-- 1 liujh zhanglab    0 Feb  1  2020 hisat2_o200201140112.txt
-rw-r--r-- 1 liujh zhanglab 1.3K Feb  2  2020 hisat2_e200201140112.txt
-rw-r--r-- 1 liujh zhanglab    0 Feb  2  2020 bowtie2_o200201140112.txt
-rw-r--r-- 1 liujh zhanglab 1.9K Feb  2  2020 bowtie2_e200201140112.txt
-rw-r--r-- 1 liujh zhanglab    0 Feb  2  2020 LiftOver_o200201140112.txt
-rw-r--r-- 1 liujh zhanglab  229 Feb  2  2020 LiftOver_e200201140112.txt
-rw-r--r-- 1 liujh zhanglab   73 Feb  2  2020 Merge_e200201140112.txt
-rw-r--r-- 1 liujh zhanglab  454 Feb  2  2020 Merge_o200201140112.txt
-rw-r--r-- 1 liujh zhanglab    0 Feb  2  2020 Pileup_o200201140112.txt
-rw-r--r-- 1 liujh zhanglab  146 Feb  2  2020 Pileup_e200201140112.txt
-rw-r--r-- 1 liujh zhanglab    0 Feb  2  2020 Call_o200201140112.txt
-rw-r--r-- 1 liujh zhanglab 6.9K Feb  3  2020 Call_e200201140112.txt
-rw-r--r-- 1 liujh zhanglab    0 Feb  3  2020 gzip_e200201140112.txt
-rw-r--r-- 1 liujh zhanglab  220 Feb  3  2020 gzip_o200201140112.txt
```
{% endraw %}
<div class="caption">
    Cool, right?
</div>

SJM was introduced into Zhanglab as early as its establishment. For me, I heavily relay on SJM, but it's tired to write them one-by-one for a big project. Literately speaking, we have some batching codes in `Perl`<sub>(written in the last centery)</sub>, but they are too bad in maintenance. So that I finally designed the [`sjm-tools`](https://github.com/jhfoxliu/Bioinfo-toolkit/tree/master/sjm_tools), a `Python` based wrapper of `SJM`. 

(To install `sjm-tools`, please type `pip install sjm-tools` in your command lines)

With this package, we can simply handle our jobs like this:

Load the package:

{% raw %}
```python
from sjm_tools import job,check_env
```
{% endraw %}

Check the input variables:

{% raw %}
```python
ref_genome = check_env("/path/to/Homo_sapiens.GRCh37.75.dna_sm.primary_assembly.fa")
python = check_env('/share/public/apps/bin/python')
```
{% endraw %}

Declear a job:

{% raw %}
```python
SJM = name + ".sjm"
workpath = PATH + "/" + name + "/"
if os.path.isdir(workpath) == False:
        os.mkdir(workpath)
JOB = job(workpath,SJM)
```
{% endraw %}

Add a step:

{% raw %}
```python
JOB.step_start(step_name="QC",memory="50G")
JOB.add_process("{cutadapt} -a NNNNNNAGATCGGAAGAGCACACGTCTGAACTCCAGTCAC -A NNNNNNAGATCGGAAGAGCGTCGTGTAGGGAAAGAG -e 0.25 -q 25 --trim-n -o read1.cutadapt.fastq -p read2.cutadapt.fastq ../{read1} ../{read2}".format(cutadapt=cutadapt,name=name,read1=read1,read2=read2))
JOB.add_process("{java} -jar {trimmomatic} PE -threads 2 -phred33 read1.cutadapt.fastq read2.cutadapt.fastq rev.fastq rev.UP.fastq fwd.fastq fwd.UP.fastq HEADCROP:10 SLIDINGWINDOW:4:22 AVGQUAL:25 MINLEN:40".format(java=java,trimmomatic=trimmomatic))
JOB.add_process("rm read1.cutadapt.fastq read2.cutadapt.fastq")
JOB.step_end()
```
{% endraw %}

And finnaly submit the job automatically:

{% raw %}
```python
JOB.job_finish()
JOB.submit()
```
{% endraw %}

I also have an ***evil*** modification of `SJM` to submit jobs to `a specific node`, personally I term it [`SJM+`](https://github.com/jhfoxliu/SJM).

(This package is not released on `Pypi` currently.)

<br/>

<br/>
<a href="/projects/"><u>Back</u></a>