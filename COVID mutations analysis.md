# COVID mutations analysis

## Summary
We analyzed the variants within  patients (intra-host diversity) in combination with the variants in the *covid* population. Thus, we had *two* levels of variability. Within and between patients. The goal of the analysis was to understand the within-patient variability. The following sub-questions were tackled: (i) can we trust the within patient variability; (ii) How should the frequency of the within-patient variability be modeled; (iii) Can we infer selective forces by combining the within-patient and between-patient variability?

Briefly, the results show that  the within-patients frequencies are noisy and characterized by large variance. Also, at least, low frequency variants cannot be trusted and they may often be artifacts. Finally, by combining the within-patient and between-patient variability we may infer mutations that may be under selection forces even though they are - still - in low frequency. 

## Methods
### Data

**Greek samples**: NGS samples from the Greek cohort were obtained by following the **paragon** protocol. The primer set comprises the following locations. 

The BED file is located here:
[The **paragon** BED file](SARSCoV2.paragon.bed)

  Primer-sets are important because in the analysis the part of the short reads that corresponds to the primer locations were soft-clipped. Thus, they didn't participate in the SNP calling analysis. 

### Data Location

All analysis is located in the folder `/home/pavlos/covid_analysis_pavlos`. The directory is actually hosted in the msc-server (ip: 139.91.75.56, directory:/home/pavlos/covid). This directory is mapped to `rantaplan`, in the folder `covid_analysis_pavlos`, and in `zoya`, in the folder `/home/pavlos/covid_analysis_pavlos`. 

The *signal-pipeline* has been performed within the directory `covid-19-signal`. There, we can see the following directories:

*  `resources`: contains different files necessary for the analysis such as the primer sets. We have put there the **paragon** primer sets. By default, the directory contains (in the folder 'primer_schemes') the artic_v3 and the liverpool primer scheme. 

* Note: in our primer scheme (the paragon), described in the file `SARSCoV2.paragon.bed`, I have substracted 1bp from the beginning of the left end of the left primer. This is because the primer masking was not performed correctly during the `ivar` process. 

* `data`: The data directory contains mainly fasta and gff3 files necessary for the analysis. The `ls` command, returns the following files:

  ```{text}
  pavlos@curie:~/covid/covid-19-signal/data$ ls
  composite_human_viral_reference.fna      composite_human_viral_reference.fna.sa  MN908947.3.gbk
  composite_human_viral_reference.fna.amb  GRC38_no_alt_analysis_set.fna           MN908947.3.gff3
  composite_human_viral_reference.fna.ann  Kraken2                                 NexteraPE-PE.fa
  composite_human_viral_reference.fna.bwt  MN908947.3.fasta
  composite_human_viral_reference.fna.pac  MN908947.3.fasta.fai
  ```

* `/home/pavlos/covid/covid-19-signal/tal_results_dir`: contains all the results. The results are organized in folders, one per sample, for the signal pipeline. Furthermore, we have created some additional folders, the `pair_alignments`, the `snp_consistency` and the `depth` and `consensus` which contain some specific analysis as we  will describe later in the text. 

* `/home/pavlos/covid/scripts`: Here we have saved the scripts, mainly R and perl, for the analyses. The `ls` command gives the following output:

  ```{text}
  ## usage: ./align_sequences.pl - | -sam <INPUT FILE> -goodAl <OUTPUT FILE> -alignments <OUTPUT FILE> -stats <OUTPUT FILE> -misal <OUTPUT FILE>
  ## performs needleman-wunsch pairwise alignment. It is used to discover whether pair-reads match together or they are characterized by mismatches or indels. A strange thing in the data is that despite paired reads should start/end at the same location, they often don't do so. Probably because larger fragments were obtained in the first place. Also there are several mismatches. 
  
  align_sequences.pl
  ---------------------------------------------------------------------------------------
  ## Given some positions on the genome, this script just goes into the mpileup file to count what nucleotides were found at certain positions. It is used to study whether certain variants found to be polymorphic within individuals from Greece, are also polymorphic in other locations (especially those that the variants do not segregate in the population (e.g. Brazil))
  
  analyze_mpileup.R
  ---------------------------------------------------------------------------------------
  ## It reads the gisaid alignment and a list of interesting positions (in our case, these are the polymorphic positions in our samples from the Talianidis lab). Then, given the positions it maps the positions back to the reference genome *in the alignment* to find the new positions in the aligment (maybe these are different due to the '-' character') and it reports:
  - per continent
  - per country 
  The states that are found in these genomic locations. 
  This script was used to find out whether the within-individuals polymorphic positions are also polymorphic in different populations around the globe
  
  continents_info_gisaid.R
  ---------------------------------------------------------------------------------------
  ## To script to exei grapsei h Maria
  ## TODO ... description
  double_covered_regions.r
  ---------------------------------------------------------------------------------------
  ## scripts from the UCSC to convert fa to Tab and VCF format respectively
  faToTab
  faToVcf
  ---------------------------------------------------------------------------------------
  ## Creates a bed file with amplicons instead of primers
  ./get_amplicons_from_primers.pl -in <PRIMER FILE>
  As input, it uses the bed file for the primers (paragon file). The output looks like that:
  NC_045512.2     29482   29574   340     nCoV-2019_2     +
  NC_045512.2     29570   29666   341     nCoV-2019_1     +
  NC_045512.2     29655   29751   342     nCoV-2019_2     +
  NC_045512.2     29731   29844   343     nCoV-2019_1     +
  
  get_amplicons_from_primers.pl
  ---------------------------------------------------------------------------------------
  ## Creates a bed file with amplicons instead of primers
  ./get_amplicons_from_primers.pl -in <PRIMER FILE>
  As input, it uses the bed file for the primers (paragon file). The output looks like that:
  NC_045512.2     29482   29574   340     nCoV-2019_2     +
  NC_045512.2     29570   29666   341     nCoV-2019_1     +
  NC_045512.2     29655   29751   342     nCoV-2019_2     +
  NC_045512.2     29731   29844   343     nCoV-2019_1     +
  
  get_amplicons_from_primers.pl
  ---------------------------------------------------------------------------------------
  ## A: keep snp positions from ivar.tsv                                          
  # saved at: '/home/maria/covid_analysis_pavlos/gisaid/our_SNPpos.txt'
  #B: make matrix of snps from all samples:
  #PINAKAS ME ROWS=POSITIONS, COLS=SAMPLES kai VALUES=ALT_FREQ
  #C: same pinakas as B, containing a column for the gisaid samples as well
  # all (onoma)                                                                                                                       
  our_snpPOS.r
  ---------------------------------------------------------------------------------------
  ## it plots the coverage and the number of primers per position. Primers may overlap so in some regions, there are two amplicons that are present and therefore the coverage is greater. 
  
  plot_depth.R
  ---------------------------------------------------------------------------------------
  ## it plots the coverage and the number of primers per position. Primers may overlap so in some regions, there are two amplicons that are present and therefore the coverage is greater. 
  
  plot.R
  ---------------------------------------------------------------------------------------
  ## TODO
  ##  It prints the number of mismatches and gaps of the paired end reads.
  plot_stats_tsvs.R
  ---------------------------------------------------------------------------------------
  ## TODO
  
  plot_tsvs.R
  ---------------------------------------------------------------------------------------
  ## TODO check if this is correct
  Prints out the number of mismatches and gaps from the paired end reads.
  
  posListScore2.pl
  ---------------------------------------------------------------------------------------
  ## samme as posListScore2.pl
  
  posListScore3.pl
  ---------------------------------------------------------------------------------------
  ## samme as posListScore2.pl
  
  posListScore.pl
  ---------------------------------------------------------------------------------------
  ## converts the tab format from paragon to bed format
  ./primTabtoBed.pl -in <FILE>\n\n
  
  primTabtoBed.pl
  ---------------------------------------------------------------------------------------
  # PERIGRAFI:                                                                             # kaloume to IVAR gia ta BAMS tou kathe amplicon                                         # kanoume merge ta BAMS apo ta diadoxika amplicon kai kaloume to IVAR                     ## First run the script split_all_bams.r (it's in the scripts folder) to split the bams of each sample                              
  ## into separate bam files, one for each amplicon                                         ## go to the ~/covid_analysis_pavlos/covid-19-signal/tal_results_dir/snp_consistency and type 'Rscript split_all_bams.r'            
  ## then each folder will contain SAM files                                               ## activate the conda environment                                                         ## ACTIVATE CONDA OUTSIDE THE SCRIPT                                                     ## conda activate /home/maria/SNAKE_COVID/conda/5258de7f                                 ## 1. go to the ~/covid_analysis_pavlos/covid-19-signal/tal_results_dir/snp_consistency directory  
  
  runIvarForSample.sh
  ---------------------------------------------------------------------------------------
  ## It runs ivar after producing the mpileup file
  runIvar.sh
  ---------------------------------------------------------------------------------------
  ## # Xwrizoume ta BAM arxeia kathe deigmatos                                             # se mini SAMs pou to kathe ena periexei ta reads pou proerxontai apo ena amplicon       #input: */core/*_viral_reference.mapping.primertrimmed.sorted.bam                         #output dir: covid_analysis_pavlos/covid-19-signal/tal_results_dir/snp_consistency       ### NOTE: edw exw kalesei to consistencyCheck.pl (9/2/2021)                               ### to opoio metaonomastike kai egine store sto: scripts/splitBAM_to_amplicons.pl   
  
  split_all_bams.r
  ---------------------------------------------------------------------------------------
  ## "It checks the amplicon overlap regions to study whether amlplicons from different primers give consistent results\n./s\
  amtools view -h BAM | consistencyCheck.pl -bed <FILE WITH PRIMERS INFO *> -snp <SNP FILE>\n\n\t* CHROM LEFT_PRIMER_START RIGHT_PRIM\
  ER_END\n\n"
  
  splitBAM_to_amplicons.pl
  ---------------------------------------------------------------------------------------
  ## prints out the p-values for the test: The variants in the current position do not depend on the major state on the next positon, based on the HyperGeometric distribution
  
  transition_prob3.R
  ---------------------------------------------------------------------------------------
  ## it finds out whether there is a bias on the type of mutations (2nd more frequent base per site) given the state in the next position. This version is for the gisaid data
  
  transition_prob_gisaid.R
  ---------------------------------------------------------------------------------------
  ## TODO
  variant_consistency_statistics.R
  
  ```

  

* `/home/pavlos/covid_analysis_pavlos/gisaid`: contains gisaid data and some subsets of it (brazilian samples). The version of the gisaid data is the 0312 (March 12th, 2021)


### The signal pipeline
The signal pipeline is described nicely on the log files generated when the signal pipeline was executed.
The signal pipeline is described in this file: [The signal pipeline](2021-01-28T194932.692546.snakemake.log). 

#### Within patients variability

The within-patient-variability was estimated by the typical process of mapping short-read to the reference genome and following the **SIGNAL** pipeline.  For the Greek samples used in the analysis, we follow the exact SIGNAL pipeline to identify as accurately as possible the mutations present in the samples as well as their frequency. For the Brazilian samples we followed a simpler pipeline, in which only mapping (bwa) and `samtools mpileup` was used, since we were interested only in the bases that are mapped at certain locations.  

#### Between patients divergence
The between-patient-variability was measured by data from the *GISAID* website. We used the 0312 version (i.e. March 12th, 2021). Data are already aligned 
