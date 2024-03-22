# Data acquire and analyze methods in SapBase

We collected the resequencing data, RNA-seq data and smRNA-seq data of Sapindaceae species from the SRA database and sRNAanno database (Chen et al. 2021).&#x20;

For resequencing data, all reads were mapped to the corresponding Sapindaceae reference genomes using BWA (Li and Durbin 2009). Samtools (Li et al. 2009) was then used to sort the mapped reads according to genomic coordinates. Reads from different Illumina lanes were merged using 'samtools merge'. Subsequently, duplicates were removed with Picard (https://github.com/broadinstitute/picard), and then the GATK (Poplin et al. 2017) was employed to call individual-specific gvcf files. Finally, we performed joint calling of SNPs by GenotypeGVCFs. Following the quality control of SNPs with bcftools (Danecek et al. 2021), the SNPs underwent stringent filtering using GATK VariantFiltration (DP < 300 || DP > 3000 || QD < 2.0 || FS > 60.0 || MQ < 40.0 || MQRankSum < −12.5 || ReadPosRankSum < −8.0), and finally obtain high-quality VCF files.&#x20;

For RNA-seq data, following initial quality control with FastQC (Andrews 2010) and adapter removal by Fastp (Chen 2023), all reads were mapped to the corresponding reference genome using STAR (Dobin et al. 2013). Finally, the expression level of transcripts was normalized into Transcripts Per Million (TPM) by StringTie (Pertea et al. 2015).&#x20;

For smRNA-seq data, we used sRNAminer (Li et al. 2023) to remove adapters. Clean reads of at least 15-nt in length were retained for further analysis. Potential small RNA and PHAS loci were then identified using sRNAminer with default parameters.
