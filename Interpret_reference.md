### RNASeq_analysis-Shyicus-

```
# create conda envoronment
conda create --name rnaseq_env

conda activate rnaseq_env
```
### Make a working directory: work then inside the directory
```
mkdir -p shyicus
cd shyicus
```
### Download the reference genome.
````
#Downloaded files genome fasta, transcripts and a gbk file from GenBank
#List the contents of it:
ls -l ref/
```
### How many sequences are in our reference files?
```
# Evaluate the FASTA files:
seqkit stat ref/*.fasta
```
### What does the genome and annotation files look like?
```
cat ref/shyicus_genome.fasta | head -5
cat ref/shyicus_features.gff3 | head -5
```
### how many exons (this is an approximate count):
```
cat ref/shyicus_features.gff3 | grep exon | wc -l
```
### What do the transcripts look like?
```
cat ref/shyicus_transcripts.fasta | head -5
cat ref/shyicus_transcripts.fasta | grep ">" | head
```

