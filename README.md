<div align="center">
<center>

![GA_workshop_logo](/figs/GA_workshop_logo.png)

# Annotating genomes: the first step to gather biological meaning from genomic data

</center>
</div>

Welcome to the **Annotating genomes: the first step to gather biological meaning from genomic data** course! In this hands-on workshop, you will learn how to take a raw *de novo* genome assembly and transform it into a biologically meaningful resource by identifying repetitive elements, predicting protein-coding genes, assigning functional annotations, and assessing annotation quality.

This workshop was part of the [5th Oslo Bioinformatics Workshop Week](https://www.mn.uio.no/bils/english/events/oslo-bioinfomatics-week/oslo-bioinformatics-workshop-week-2026/), which took place from December 7 to December 11, 2026 at *Livsvitenskapsbygningen* (LVB; *The Life Science Building*), University of Oslo. The workshops were open to the scientific community in Oslo and the surrounding area.

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
| **Repeat Masking** | RepeatModeler, RepeatMasker |
| **Read Alignment** | HISAT2, SAMtools |
| **Structural Annotation** | GALBA, Tiberius, ToxCodAn-Genome |
| **Functional Annotation** | eggNOG-mapper, InterProScan |
| **Quality Control & Stats** | BUSCO, AGAT |
| **Visualization** | IGV, JBrowse, Geneious (paid) |
| **Misc** | BEDtools, GFFread, miniprot, BLAST, seqkit |

Note: most tools are open-source and freely available.

## 🐍 Study case
We will use the Golden lancehead (*Bothrops insularis*) as a model for this tutorial ([Nachtigall et al., 2026](https://doi.org/10.1093/gbe/evaf243)). This species is a venomous snake and has venom genes that comprise complex genomic regions, which suits well as a study case to manually inspect gene annotation.

This genome is publicly available in the NCBI ([PRJNA679826](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA679826/)) and [figshare](https://figshare.com/projects/Bothrops_insularis_genome/237995) repositories.

This genome has 18 chromosomes, but we will use two chromosomes containing two toxin families that are classified as major venom components and hard to annotate. Specifically, we will use chromosomes mi-1 and mi-4 that contains the toxin families snake venom metalloproteinase (SVMP) and phospholipase A2 (PLA2), respectively. 

SVMPs and PLA2s are genes detected in tandem arrays (ranging from 2 to 36 copies) in the genome of vipers and represent regions hard to annotate due to similarity of paralogs and the distance between genes. These duplications usually are accompanied by repetitive regions, which usually add another layer of complexity on the genome annotation process.

To make it easier for the workshop, most files were previously subset and are in the subdirectory named "data" as follow:
```text
GenomeAnnotationWorkshop_2026/
├── data/
    ├── assembly/               # Input genome assembly (.fasta)
    |   └── genome.fasta.gz
    ├── annotation_reference/   # Folder containing annotation files to be used as reference (compare with the results obtained by the workshop)
    |   ├── gene_annotation.gtf.gz
    |   └── repeat_annotation.gff.gz
    ├── rnaseq/                 # Paired-end RNA-seq reads (.fastq.gz)
    |   ├── VG_R1.fastq.gz
    |   ├── VG_R2.fastq.gz
    |   ├── Liver_R1.fastq.gz
    |   └── Liver_R2.fastq.gz
    └── proteins/               # Reference protein database (.fasta)
        └── protein.fasta
```
 - The data is based on real sources and it was subset for teaching reasons. Remember that it is not completed. 


## Getting started

## Repeat annotation
The repeat annotation identify repetitive DNA, such as transposons and simple repeats, that can inflate substantially the number of false positives in the gene annotation step because repetitive elements often mimic coding signals or attract misleading sequence alignments. To handle such issue, we can soft-mask the genome by indicating repetitive regions with lower case. It allow gene annotation tools to take into account repetitive sequences without losing real coding regions. Soft-masking a genome means to lower case letters that represent repetitive sequences (see the example below). But to soft-mask a genome, we first need to identify the repetitive regions through a step known as repeat annotation.

```
# genome
ATCGATCGAAAAAAAAAAAAAAATCGATCGATCG

# soft-masked genome
ATCGATCGaaaaaaaaaaaaaaaTCGATCGATCG
```

The repeat annotation can be performed using [RepeatModeler2](https://github.com/Dfam-consortium/RepeatModeler), to generate a *de novo* species-specific library, and [RepeatMasker](https://github.com/Dfam-consortium/RepeatMasker), to perform the annotation. We can complement the species-specific TE library using a curated TE library of snakes previously published ([Castoe et al., 2013](https://doi.org/10.1073/pnas.1314475110)).

This step can take a while. To make our life easier for the workshop, we have made the soft-masked genome available in the data subdirectory (i.e., ```genome.soft.masked.fasta```). But you can give it a try by expanding the section.

<details>
<summary>Expand "Repeat masking" </summary>

```
# run repeatmodeler
BuildDatabase -name Bothrops_insularis -engine ncbi genomes.fasta
RepeatModeler -pa 20 -engine ncbi -database Bothrops_insularis

# add a prefix
cat Bothrops_insularis-families.fa | seqkit fx2tab | awk '{ print "Binsularis_"$0 }' | seqkit tab2fx > Bothrops_insularis-families.prefix.fa

# download the snakes TE set available and merge to the species-specific library
wget https://raw.githubusercontent.com/pedronachtigall/Repeat-annotation-pipeline/refs/heads/main/TElibs/BovB_CR1_TElib.fasta
wget https://raw.githubusercontent.com/pedronachtigall/Repeat-annotation-pipeline/refs/heads/main/TElibs/Boa_Snakes_Known_TElib_CLEAN.fasta
cat Bothrops_insularis-families.prefix.fa BovB_CR1_TElib.fasta Boa_Snakes_Known_TElib_CLEAN.fasta > Binsu_curated_TElib.fasta

#run repeatmasker
RepeatMasker -pa 20 -gff -s -a -inv -no_is -norna -xsmall -nolow -div 40 -lib Binsu_curated_TElib.fasta -cutoff 225 genome.fasta

```

</details>
<br>

A complete pipeline with commands and scripts used to perform the repeat annotation is well described in the following tutorial: [https://github.com/pedronachtigall/Repeat-annotation-pipeline](https://github.com/pedronachtigall/Repeat-annotation-pipeline)




<!---


EVERYTHING IN THE COMMENT IS BEING HERE FOR FURTHER USE AND NEED ADJUSTMENTS


<details>
<summary>Expand "Transcriptome Assembly" Section</summary>

</details>
<br>


-->

