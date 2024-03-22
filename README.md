---
cover: .gitbook/assets/1.jpg
coverY: 161.21309823677583
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 😄 SapBase (Sapinaceae Genomic DataBase)

## Why Sapbase?

[<mark style="color:green;">**SapBase**</mark>](http://www.sapindaceae.com/) aims to serve as a central genomic datahub and a powerful analytic platform for scientific research on Sapindaceae species and comparative studies with other plants.

Currently, SapBase hosts genomic resources for seven Sapindaceae species, including 16 full genome sequences, >400 sets of resequencing genomic data (4.82 TB), 919 RNAseq data (10.3 TB) from 49 projects, and 501 sRNA loci from the sRNAanno database. In total, there are 514,422 genes (893,747 transcripts), with 501,479 of them having functional annotations. 4,577 functional domains are annotated from 392,123 genes. SapBase also predicts 79,862,416 interaction relations between 145,248 proteins. 89,025 synteny blocks between every two Sapindaece species were identified covering 134,016 genes. Besides, 486 gene co-expression modules were singled out by the integrative analyses of these omics data.

SapBase is constructed and maintained by **XIALAB** from the College of Horticulture at South China Agricultural University.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Sapbase provides a large number of user-friendly and easy-to-use analysis tools for online analysis of massive omics data of Sapindaceae species. Here we provide detailed instructions for each tool, including an introduction to input files and output results. In fact, a link to the help documentation is provided on the page of each tool, and users can click directly to view it.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## Overview of data collection and analysis methods in sapbase

We collected the resequencing data, RNA-seq data and smRNA-seq data of Sapindaceae species from the SRA database and sRNAanno database (Chen et al. 2021).&#x20;

For resequencing data, all reads were mapped to the corresponding Sapindaceae reference genomes using BWA (Li and Durbin 2009). Samtools (Li et al. 2009) was then used to sort the mapped reads according to genomic coordinates. Reads from different Illumina lanes were merged using 'samtools merge'. Subsequently, duplicates were removed with Picard (https://github.com/broadinstitute/picard), and then the GATK (Poplin et al. 2017) was employed to call individual-specific gvcf files. Finally, we performed joint calling of SNPs by GenotypeGVCFs. Following the quality control of SNPs with bcftools (Danecek et al. 2021), the SNPs underwent stringent filtering using GATK VariantFiltration (DP < 300 || DP > 3000 || QD < 2.0 || FS > 60.0 || MQ < 40.0 || MQRankSum < −12.5 || ReadPosRankSum < −8.0), and finally obtain high-quality VCF files.&#x20;

For RNA-seq data, following initial quality control with FastQC (Andrews 2010) and adapter removal by Fastp (Chen 2023), all reads were mapped to the corresponding reference genome using STAR (Dobin et al. 2013). Finally, the expression level of transcripts was normalized into Transcripts Per Million (TPM) by StringTie (Pertea et al. 2015).&#x20;

For smRNA-seq data, we used sRNAminer (Li et al. 2023) to remove adapters. Clean reads of at least 15-nt in length were retained for further analysis. Potential small RNA and PHAS loci were then identified using sRNAminer with default parameters.

