---
title: Fall in 2021
date: 2021-11-05
---


# 2021 Fall, UCI CMB program rotation 

### Author: Runhang Shu, [PhD student](www.runhangshu.com)      
### Affiliation: University of California, Irvine 
### Contact: darsonshu@gmail.com

### Date started: 2021-11-05
### Date end (last modified): 2021-11-05

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.    

**Introduction:**    
Notebook for rotation in Dr. Katrine White and Dr. Charles Glabe lab. It'll log notes, ideas and inspirations from papers I read; Save a copy of bioinformatic and statistical analysis I did for reproducible science!


# Table of contents    
* [Page 1: 2021-11-05](#id-section1) Literature review 1 - The concurrence of DNA methylation and demethylation is associated with transcription regulation
* [Page 2: 2021-11-17](#id-section2) The Brucella data



------

<div id='id-section1'/>    

### Page 1:
**Background**

In mammals DMNT (DNA methyltransferases) methylaze while TET (Ten-Eleven translocation deoxygenases) demethylaze DNA. Despite these two processes are apparently antagonizing, a few studies shed the light on the jointed effects of these two players on tumorigenesis. 

**Obstacles** (what need to be improved?)

The DNA methylation level are usually assessed by "averaging" level or calculating the methylation heterogeneity/variation. Neither of these two approaches can delineate the degree of concurrence between active methylation and demethylation (unmethylated CpGs in partially methylated reads). Additionally, although a recent mathematical model takes methylation and demethylation into account for individual CpGs in stem cells, this model is not good enough in that it does not consider the spatial coupling of concurrence methylation at adjacent CpGs, which is critical for transcription factor and cancer gene regulation.


**Objective**

To test to what extend that the two players affect cancer gene regulations. 

**Methods**

Bisulfite sequencing of embryonic stem cells of mice

**Key findings**

* Methylation concurrence represents a better metrics than traditional average methylation level and methylation variation to predict gene expression.  
* Using DMNT- and TET-knowout mice, the authors indicate that there might be hidden patterns unseen by simply using "average" methylation level. 
* Methylation concurrence is negatively correlated with gene expression.
  * Uisng public available data: WGBS and RNA-seq data from Epigenetic Roadmao Consortium 
  * DNMT3A and TET1 prevent binding of each other mainly in *TSS-proximal regions*
* Methylation concurrence is associated with the repression of tumor suppressor genes
  * TSGs (Tumor Suppressor Genes) are negatively associated with methylation concurrence
  * Cell lineage genes are positively asscoaited with methylation concurrence 
  * Housekeeping genes have no association with methylation concurrence 
* Methylation concurrence can see the unseen patterns in Undermethylated regions (UMRs) in relation to average methylation and methylation variation.

------

<div id='id-section2'/> 

### Page2:
```
**Processed all fasta files (txt format) in HPC3 using a bash script**

#!/bin/bash

#SBATCH --job-name=Bru      ## Name of the job.
#SBATCH -A CGLABE_LAB ## account to charge
#SBATCH -p free ## partition/queue name  highmem,hugemem,maxmem
#SBATCH --nodes=1            ## (-N) number of nodes to use
#SBATCH --ntasks=1           ## (-n) number of tasks to launch
#SBATCH --cpus-per-task=4    ## number of cores the job needs
#SBATCH --error=slurm-%J.err ## error log file

../pratt_package_500000/pratt fasta ./USA_naive/Bru1.txt -C% 2 -PL 11 -PX 1 -E 0 -FN 0 -FL 1 -ON 50
../pratt_package_500000/pratt fasta ./USA_naive/Bru2.txt -C% 2 -PL 11 -PX 1 -E 0 -FN 0 -FL 1 -ON 50
../pratt_package_500000/pratt fasta ./USA_naive/Bru3.txt -C% 2 -PL 11 -PX 1 -E 0 -FN 0 -FL 1 -ON 50
../pratt_package_500000/pratt fasta ./USA_naive/Bru4.txt -C% 2 -PL 11 -PX 1 -E 0 -FN 0 -FL 1 -ON 50
../pratt_package_500000/pratt fasta ./USA_naive/Bru6.txt -C% 2 -PL 11 -PX 1 -E 0 -FN 0 -FL 1 -ON 50
../pratt_package_500000/pratt fasta ./USA_naive/Bru7.txt -C% 2 -PL 11 -PX 1 -E 0 -FN 0 -FL 1 -ON 50
../pratt_package_500000/pratt fasta ./USA_naive/Bru8.txt -C% 2 -PL 11 -PX 1 -E 0 -FN 0 -FL 1 -ON 50
../pratt_package_500000/pratt fasta ./USA_naive/Bru9.txt -C% 2 -PL 11 -PX 1 -E 0 -FN 0 -FL 1 -ON 50

```

* Tried different C% (the minimum number of frequency of each pattern)
  1. C%=0.5% and 500 patterns 
  2. C%=2% and 50 patterns 
  

