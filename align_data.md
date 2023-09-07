### Run statistics on the reads:
```
seqkit stat *.fastq.gz > stat.txt
```
### Prepare experimental design file.
```
#we can also generate just the ids for the samples like so:
cat design.csv | csvcut -c sample | sed 1d > ids.txt
```
### Index reference genome
```
# The reference genome.
IDX=ref/shyicus_genome.fasta

# Build the genome index.
hisat2-build $IDX $IDX

# Index the reference genome with samtools.
samtools faidx $IDX
```
### Generate the alignments
```
# The index name.
IDX=refs/genome.fa

# Create the BAM folder.
mkdir -p bam

# Align the FASTQ files to the reference genome.
cat ids.txt | parallel "hisat2 -x $IDX -U reads/{}_R1.fastq.gz | samtools sort > bam/{}.bam"

# Index each BAM file.
cat ids.txt | parallel "samtools index bam/{}.bam"

#we can see all the resulting files with:
ls -l bam
```
### Making a bigWig coverage file
```
#activate conda environment
conda activate bigwig_env

# Turn each BAM file into bedGraph coverage. The files will have the .bg extension.
cat ids.txt | parallel "bedtools genomecov -ibam  bam/{}.bam -split -bg  > bam/{}.bg"

# Convert each bedGraph coverage into bigWig coverage. The files will have the .bw extension.
cat ids.txt | parallel "bedGraphToBigWig bam/{}.bg  ${IDX}.fai bam/{}.bw"
```

The resulting bedGraph and bigWig files will have *.bg and *.bw extensions and are placed in the bam directory.

Drag bigWig files in the IGV panels, and the coverage information will load up much-much faster. 

### See you in next chapter!! Thanks!!
