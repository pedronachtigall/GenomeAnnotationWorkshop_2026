# Annotating genomes: the first step to gather biological meaning from genomic data

Welcome to the **Annotating genomes: the first step to gather biological meaning from genomic data** course! In this hands-on workshop, you will learn how to take a raw *de novo* genome assembly and transform it into a biologically meaningful resource by identifying repetitive elements, predicting protein-coding genes, assigning functional annotations, and assessing annotation quality.

This workshop was part of the 5th Oslo Bioinformatics Workshop Week, which took place from December 7 to December 11, 2026 at *Livsvitenskapsbygningen* (LVB; *The Life Science Building*), University of Oslo. The workshops were open to the scientific community in Oslo and the surrounding area.

## 🎯 Learning Objectives

By the end of this course, you will be able to:
1. **Identify and mask repetitive elements** in a genome assembly to prevent false-positive gene predictions.
2. **Perform *ab initio* and evidence-based structural gene prediction** using RNA-seq and protein homology data.
3. **Assign functional annotations** to predicted proteins.
4. **Evaluate and visualize** the completeness and quality of your final gene set.
5. **Manually inspect complex genomic regions** to ensure a comprehensive and accurate annotation of genomic regions that are error-prone.


## 🛠️ Prerequisites & Software Environment

| Category | Tools Used |
| :--- | :--- |
| **Repeat Masking** | `RepeatModeler`, `RepeatMasker` |
| **Read Alignment** | `HISAT2`, `SAMtools` |
| **Structural Annotation** | `GALBA`, `Tiberius`, `ToxCodAn-Genome` |
| **Functional Annotation** | `eggNOG-mapper`, `InterProScan` |
| **Quality Control & Stats** | `BUSCO`, `AGAT` |
| **Visualization** | `IGV` (open-source), `JBrowse` (open-source), `Geneious` (paid) |


## Study case
We will use the Golden lancehead (*Bothrops insularis*) as a model for this tutorial ([Nachtigall et al., 2026](https://doi.org/10.1093/gbe/evaf243)). This species is a venomous snake and has venom genes that comprise complex genomic regions, which suits well as a study case manually inspect gene annotation.

This genome is publicly available in the NCBI ([PRJNA679826](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA679826/)) and [figshare](https://figshare.com/projects/Bothrops_insularis_genome/237995) repositories.

This genome has 18 chromosomes, but we will use two chromosomes containing two toxin families that are classified as major venom components and hard to annotate. Specifically, we will use chromosomes mi-1 and mi-4 that contains the toxin families snake venom metalloproteinase (SVMP) and phospholipase A2 (PLA2), respectively.

