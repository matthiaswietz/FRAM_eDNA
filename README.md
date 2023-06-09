## eDNA metabarcoding of microbial communities  

This repo describes the bioinformatic pipeline from raw fastq reads to ASV counts, including primer clipping and ASV generation. Reads were obtained by PCR of environmental DNA (eDNA) with 16S and 18S rRNA primers, followed by Illumina MiSeq sequencing and generation of amplicon sequence variants (ASVs) using DADA2. Each Illumina run was processed individually following the developer's guidelines (https://benjjneb.github.io/dada2/tutorial_1_8.html), and then merged before chimera removal and taxonomic assignment. 

This repo describes processing of eDNA samples from autonomous Remote Access Samplers (RAS) in the FRAM Observatory (https://www.awi.de/en/expedition/observatories/ocean-fram.html). Scripts are however generalizable to any ribosomal metabarcoding of eDNA. 

### Organization of directories and files 

- [bac_processing](./bac_processing): Processing of 16S rRNA reads using individual DADA2 scripts per Illumina run, followed by script [MergeChimTax.R](./bac_processing/MergeChimTax.R) for merging sequence tables, chimera removal and taxonomy assignment. 

- [euk_processing](./euk_processing): Processing of 18S rRNA reads using individual DADA2 scripts per Illumina run, followed by script [MergeChimTax.R](./euk_processing/MergeChimTax.R) for merging sequence tables, chimera removal and taxonomy assignment. 

- [output](./output): ASV table, taxonony table, and ASV sequences from both 16S and 18S metabarcoding. Furthermore, ENA accession numbers of all raw fastq files for [16S](./output/ENA_16S_fastq.txt) and [18S](./output/ENA_18S_fastq.txt) amplicons. 

- [metadata](./metadata):  physicochemical measurements and general sample information, needed for detailed analyses as described in the following. Original fastq files and sample information can be matched via columns "sample_title" listed in [sample_info.txt](./metadata/sample_info.txt) and ENA txtfiles in the [output](./output) directory.

This top-level directory contains Rscripts to further process the original data. This includes script [DataLoad.R](./DataLoad.R) to account for negative control counts, refomat taxonomic names if appropriate, and connect with environmental data deposited in [metadata](./metadata). In case samples from several timepoints were pooled, a "mean date" is calculated, and the corresponding environmental parameters averaged as well. 

The script [RarefacDiversity.R](./RarefacDiversity.R) then calculates alpha-diversity indices on ASV tables. Finally, script [DataExport.R](./DataExport.R) subsets the full ASV and metadata tables for individual studies, e.g. Wietz et al. (https://www.nature.com/articles/s43705-021-00074-4) and Priest et al. (https://www.biorxiv.org/content/10.1101/2022.08.12.503524v2).
