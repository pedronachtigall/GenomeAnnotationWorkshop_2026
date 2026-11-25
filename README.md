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
| **Quality Control & Stats** | `BUSCO`, `AGAT`, `IGV` (for visualization) |
| **Visualization** | `IGV` (open-source), `JBrowse` (open-source), `Geneious` (paid) |
