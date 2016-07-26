# TF-binding-prediction

Task: Identify potential transcription factor binding sites
Current pipeline model:
1. Use RNA-seq/transcript expression/microARray chipseq data, group genes into “co-expression networks”
  a) R package WGCNA for module development and calculations
  b) Extra fancy: R package rsgcc for a special correlation statistic that is optimized for transcription data
  c) Extra extra fance: Limit the modules by genes with known similar function (called “enrichment analysis”)
The idea here is that genes that share similar expression patterns are related in some way functionally and so can be grouped into expression modules

2. For each module, extract the promoter sequences of the genes based on the best available gene annotation
  a) Look for Coding sequences, extract 1000-2000 bp upstream of this to include 5’ UTR

3. Run a motif recognition algorithm on these extracted sequences
  a) HOMER-- the function is called findMotifs.pl
  b) Validate results with randomly selected promoter sequences run through HOMER as well
    i) We eliminate motifs found in both groups, so we know the ones we have found are actually specific to a co-expresssed group of genes

4. Perform some kind of conservation testing on the motifs we have identified
  a) Do they appear in other organisms that are well documented?
  b) This is easy for a plant (what I’m working on…), but much harder in humans
  c) Compare to the chimp genome??
  d) Keep only motifs that pass some selected conservation threshold

5. Compare the motifs that pass the threshold to a database of known binding motifs
  a) This will allow us to both confirm our pipeline (i.e. we are getting what we are expecting) as well as possibly identify “novel” binding sites

From here, we will want to see how we can integrate the other data we have access to (DNase-seq, etc.), as well as what we could do to generate “tissue specific results”

One idea would be to use the genome wide results from the pipeline above as our general standard, and then run a similar pipeline on tissue specific data, and identify motifs that are unique to certain tissue types.
This will be quite computationally intensive.  Get ready marylouuuuuuu
