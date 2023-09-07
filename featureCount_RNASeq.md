### Convert feature file gff3 to gft format
```
#activate conda environment
conda activate gfread_env

#convert gff3 to gtf
gffread shyicus_features.gff3 -T -o shyicus_features.gtf
```
### count features
```
# Run the featureCounts program to summarize the number of reads that overlap with features/genes.
cat ids.txt | parallel -j 1 echo "bam/{}.bam" | xargs  featureCounts -a ref/shyicus_features.gtf -o counts.txt
```
### Standardizing the count matrix
```
#activate conda environment
conda activate rnaseq_env

#install r-base
conda install -c conda-forge r-base

#run the script to standardizing the counts.txt in counts.csv
Rscript code/parse_featurecounts.r
```
The counts.csv file may be considered the primary output of the alignment-based quantification method.
### See you in next chapter!
