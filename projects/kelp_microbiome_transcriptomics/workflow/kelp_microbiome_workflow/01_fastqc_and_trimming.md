## Purpose:
* To check quality of the reads before and after trimming, to ensure the data has no issues that may affect downstream analyses

## Readings
* [Introduction to RNA-Seq using high-performance computing](https://hbctraining.github.io/Intro-to-rnaseq-hpc-salmon/lessons/qc_fastqc_assessment.html)
* [fastqc help](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/)

## Summary report analysis (multiqc)
### **General statistics
* %GC ranges from 42% - 49% (can be attributed to the differences in microbial species in each sample)
* Read length dropped from 101bp to ~99bp after trimming
* Total sequences range from 64.7 million to 110.1 million

### **Per-base sequence quality 
* Shows Phred quality across read position
* **Phred score Q = −10·log₁₀(error probability):** 
	* Q20 = 1 error in 100
		* The mean raw Q20% for all samples is **99.34%**. This means 99.34% of the bases in all our reads have a probability of being incorrect of ≤1%. In simpler terms, Across all nucleotide positions sequenced, 99.34% of bases have a base-call accuracy of at least 99%
		* This increases to **99.51%** in trimmed samples. This means 99.51% of the bases in all our reads have a probability of being incorrect of ≤1%. In simpler terms, Across all nucleotide positions sequenced, 99.51% of bases have a base-call accuracy of at least 99%
	* Q30 = 1 in 1000
		* The mean raw Q30% across all samples is **97.18%**. This means that 97.18% of all sequenced bases have a Phred quality score of at least Q30, corresponding to a probability of being incorrectly called of ≤0.1%. In simpler terms, across all nucleotide positions sequenced, 97.18% of bases have a base-call accuracy of at least **99.9%**
		* The mean raw Q30% across all samples is **97.49%**. This means that 97.49% of all sequenced bases have a Phred quality score of at least Q30, corresponding to a probability of being incorrectly called of ≤0.1%. In simpler terms, across all nucleotide positions sequenced, 97.49% of bases have a base-call accuracy of at least **99.9%**
	* Modern Illumina is mostly Q30+
	* Quality _always_ sags toward the 3′ end (since errors accumulate every cycle, the final bases have experienced the most accumulated error) and R2 is usually a bit worse than R1 (DNA is slightly degraded at this point due to the numerous cycles, then it goes further to accumulate cycles of errors)  . These can be attributed to:
		* **Signal decay**: Reads are produced one base at a time. for 150bp read, that means 150 cycles. Each cycle is a little less perfect than the one before. For each cycle, we have:
			* Addition of fluorescent nucleotides
			* Imaging the fluorescence
			* Removing the fluorescent dye
			* Removing the blocking group (temporary chemical cap attached to each nucleotide that **prevents DNA polymerase from adding more than one nucleotide during a single sequencing cycle, before an image is taken**)
				* Removed after imaging so that DNA polymerase can continue
				* If removal fails, the strand will be one nucleotide behind on the cycle (**phasing**)
			* Repeat
		* **Phasing:** Accumulation of errors with every cycle e.g., incomplete removal of a fluorescent dye, DNA strands fall behind or jump ahead, blocking groups remain

### Per-sequence quality score
* Average quality score =  x-axis 
* Number of sequences with that average =  y-axis
* Majority of  reads need to have a high average quality score with no large bumps at the lower quality values
* For our data, this is true

### **Per Base Sequence Content
* Always gives a FAIL for RNA-seq data - the first 10-12 bases result from ‘random’ hexamer priming that occurs during RNA-seq library preparation
* **Random hexamer priming** is a method used to start the synthesis of complementary DNA (cDNA) from RNA
	* Instead of using one primer (**short piece of DNA that provides a starting point for reverse transcriptase to begin making DNA**) that binds to a specific sequence, it uses a **mixture of millions of short, 6-nucleotide primers** that can bind at many different locations along RNA molecules
	* There are four possible nucleotides (A, T, C, G), so the total number of possible 6-base sequences is: 4^6=4096
	* A random hexamer mix contains representatives of these thousands of different sequences
	* After the primer binds, reverse transcriptase begins extending the primer and copied RNA into cDNA
	* This is advantageous as it provides good coverage across the entire transcript
	* Used mostly in bacterial and archeal RNA due to lack of poly(A) tails (oligo(dT) primers can't be used)
* This priming is not perfectly random
* Some hexamer sequences bind much more efficiently than others, hence the first few bases of many reads come from a biased subset of RNA molecules
* FastQC detects this unequal base composition and flags it as a **Per Base Sequence Content** warning or fail
* This is true for our data since it is RNA seq

### **Per Sequence GC Content
* GC distribution over all sequences - For each read, what percentage of its bases are G or C?
* Note whether the GC content of the central peak corresponds to the [expected % GC for the organism](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2909565/)
* The distribution should be normal (most fragments naturally have 42% - 58% which is near average hence normal distribution) unless **over-represented sequences** (sharp peaks on a normal distribution) or **contamination with another organism** (broad peak)
	* Many reads usually come from the same sequence or very similar sequences
	* RNA-seq samples many different transcripts
	* Different genes = different GC contents
	* This therefore produces a broad peak
* Our plot shows sharp peaks and broad peaks since we have a mix of different microbes:
	* For metatranscriptomics, many different microbial species are sequenced
	* Different bacteria have different GC contents
	* Since the reads come from a mixture of organisms and different genes within those organisms, overall GC distribution becomes broad
	* Sharp peaks suggest a large fraction of reads are coming from a limited set of highly similar sequences e.g., rRNA, rather than a diverse transcript pool (RNA-seq does not sample every transcript equally)


### **Sequence Duplication Levels
* Measures how many times the **same exact sequence read** appears in the sequencing data
* Most reads **should** be unique
* Duplication may occur due to:
	* Abundance of the original DNA/transcript (many copies)
	* The same DNA/transcript can be sequenced many times due to library prep process (PCR amplification)
* FastQC takes sequences and counts how many times each exact read occurs
* It then summarizes:
	* How many reads are unique
	* How many appear twice
	* How many appear many times
* For RNA-seq we don’t address this in the analysis:
	* Duplication is expected in RNA-seq because RNA molecules are not equally abundant
	* RNA-seq is a measure of gene expression
* In this analysis we seem to have a large number of duplicated sequences
* x ax is = duplication level (how many times an identical sequence appear in the dataset. Level 1 = once, 2 = twice, etc.,)
* y axis = % reads (fraction of total reads belonging to each duplication category)


### **Overrepresented sequences table**
* Displays the sequences (at least 20 bp) that occur in more than 0.1% of the total number of sequences
* Aids in identifying contamination, such as vector or adapter sequences
* If the %GC content is off, this table can help identify the source
* If not listed as a known adapter or vector, it can help to BLAST the sequence to determine the identity
* Not needed here since we know the source of variation


