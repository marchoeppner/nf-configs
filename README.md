# nf-configs

Welcome to the central config repository of my little pipeline ecosystem. I am developing workflows vor various applications in food safety monitoring, including taxonomic profiling of food stuff, assembly, annotation and profiling of bacterial isolates as well as the characterization of signatures of genetic modification in plant materials (seeds and processed products). And possibly more to come over the next months.

All pipelines are developed in [Nextflow](https://nextflow.io/), using a common [template](https://github.com/marchoeppner/nf-template) with a focus on portability, high standard of implementation, ease of use and version control. I have previously developed within the [nf-core](https://github.com/nf-core) project and most of the coding framework used here is based on conventions originally developed by nf-core for the Nextflow community. As such, nf-core developers will find it immediately familiar and users will appreciate the overall robustness.

The config files hosted here can be jointly used across the following pipelines:

## GABI 

[GABI](https://github.com/marchoeppner/gabi), short for '**g**enomic **a**nalysis of **b**acterial **i**solates' is a workflow for the assembly of bacterial genomes from quality-controlled read data and downstream characterization (annotation, MLST typing, etc). GABI supports short reads, Nanopore long reads as well as Pacbio HiFi reads. 

## Eutaxpro

[Eutaxpro](https://github.com/marchoeppner/eutaxpro) performs taxonomic profiling of mitochondrial amplicon data to detect eukaryote species from mixed samples. The main application is in detecting food fraud, such as mis-labelled ingredients or use of endangered animals in (processed) foods. 

## GMO-check

[GMO-check](https://github.com/marchoeppner/gmo-check) is in an early development stage and will eventually allow the characterization of GMO-modifications in food stuffs from genomic reads (Amplicons, target enrichment, WGS). At the moment, only the detection of the GABA3 mutation in tomato is supported.


