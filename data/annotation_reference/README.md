### Commands to generate the annotation reference (to compare with results obtained in the workshop)

```bash
wget https://figshare.com/ndownloader/files/52417259 -O Binsularis.gene_annotation.gtf.gz
wget https://figshare.com/ndownloader/files/52417235 -O Binsularis.repeat_annotation.gff.gz

zgrep -w "Binsu_mi-1" Binsularis.gene_annotation.gtf.gz > Binsu_mi-1.gene_annotation.gtf
zgrep -w "Binsu_mi-4" Binsularis.gene_annotation.gtf.gz > Binsu_mi-4.gene_annotation.gtf

zgrep -w "Binsu_mi-1" Binsularis.repeat_annotation.gff.gz > Binsu_mi-1.repeat_annotation.gff
zgrep -w "Binsu_mi-4" Binsularis.repeat_annotation.gff.gz > Binsu_mi-4.repeat_annotation.gff

cat Binsu_mi-1.gene_annotation.gtf Binsu_mi-4.gene_annotation.gtf > gene_annotation.gtf
cat Binsu_mi-1.repeat_annotation.gff Binsu_mi-4.repeat_annotation.gff > repeat_annotation.gff
gzip gene_annotation.gtf
gzip repeat_annotation.gff
```
