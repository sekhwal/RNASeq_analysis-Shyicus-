### tools implement for pseudo-alignment.

```
# use salmon
# Create a new environment.
conda create --name salmon_env

# Activate the new environment and install packages.
conda activate salmon_env salmon parallel
```
### Preparing the transcriptome
```
# The transcriptome in fasta format.
REF=refs/transcripts.fa

# The name of the salmon index
IDX=idx/salmon.idx

# Build the index with salmon.
salmon index -t ${REF} -i ${IDX}

```
### Running the classification
```
cat ids.txt | parallel -j 4 "salmon quant -i ${IDX} -l A --validateMapping -r reads/{}_R1.fastq.gz -o salmon/{}"
```
We now have a’ salmon’ directory containing subdirectories for each sample.
```
ls -1 salmon
```
### Combine your counts
```
# rename the salmon output .sf files using the script
bash change.sh

#combine the .sf files using the python script
python salmon_combine.py

```
