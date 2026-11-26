### Commands to generate the study case

```bash
wget https://figshare.com/ndownloader/files/52416596 -O Binsularis_primary_chromosomes.fasta.gz

gzip -d Binsularis_primary_chromosomes.fasta.gz

samtools faidx Binsularis_primary_chromosomes.fasta
samtools faidx Binsularis_primary_chromosomes.fasta "Binsu_mi-1" > Binsu_mi-1.fasta
samtools faidx Binsularis_primary_chromosomes.fasta "Binsu_mi-4" > Binsu_mi-4.fasta

cat Binsu_mi-1.fasta Binsu_mi-4.fasta > genome.fasta
gzip genome.fasta

#soft-mask genome using the repeat annotation
bedtools maskfasta -soft -fi genome.fasta -bed ../annotation_reference/repeat_annotation.gff -fo genome.soft.masked.fasta
```
