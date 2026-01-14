# JaxProjectData
Data Files For Our Final BDISC Project

GSM files from: https://journals.asm.org/doi/10.1128/iai.00814-20 (Paper),
https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE166522 (Data).

GSM files represent genes and their RNA counts from infected and control mice. Samples come from Mice 3 days post experiment start (3D) or 14 days post experiment start (14D). FPKM represents normalized counts.

Protein data from: https://www.nature.com/articles/s41586-025-08615-w#Abs1

Presentation here: 

Layout:
1. GSM files represent raw RNA counts for genes in mice infected with a bacteria. Normalized counts are included in files, but can't be used for Deseq 2 analysis.
2. Options with those files:
     1. Clean files and merge them into one file with code to run DESeq2 analysis for making plots.

     1. We didn't do this; instead were exploring specific genes, which are in Genes_of_intrest.csv file.
     2. Our workflow was using Genes_of_intrest in deseq2 analysis for creating a heatmap and t-test statistics with code in Heatmap&T-Test.ipynb file. Also created a volcano plot for showing t-test results. DeSeq2 code from: https://github.com/mousepixels/sanbomics_scripts/blob/main/PyDeseq2_DE_tutorial.ipynb.
     3. Then, used Genes_of_intrest for making a volcano plot of genes to compare expression between infected samples and control samples and find genes with significant differences in expression. Code for that is in this file:
     4. Then, used Genes_of_intrest file for creating Gene-Gene analysis of genes in infected vs control samples. After that, we did a gene ontology exploration 
  
3. Explanations of other files in this repo:
  1. rawcountdata.xlsx is a file of all the raw counts and their genes by samples, with normalized counts removed. Can be used in the same way like Genes_of_intrest file for this workflow. Was created manually through Excel, not by code.
  2. CreatingCleanRNADataset.ipynb is code for making cleaner RNA datasets and for data wrangling. Was not used in this project, but could be used with rawcountdata.xlsx to clean the file and make it easier to use with Deseq2 analysis.  
