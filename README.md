# Jackson Labs BDISC Project Antimicrobial Peptides

GSM files from: https://journals.asm.org/doi/10.1128/iai.00814-20 (Paper),
https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE166522 (Data).

Protein data from: https://www.nature.com/articles/s41586-025-08615-w#Abs1

Presentation here: [https://1drv.ms/p/c/d09893c430a34e2b/IQCuI_Lgmok4Q6rif4xR_wZFATZ3Fc9pwB6x46VcJNx_hcY?e=H4jm1Q
](https://docs.google.com/presentation/d/1zRQ5v92g9lMy2Um5BXbrCuwpzMStVxTcj4Y34F-IoSw/edit?usp=sharing)
Layout:
1. GSM files represent raw RNA counts for genes in mice either infected with a bacteria, or controls. Samples come from Mice 3 days post experiment start (3D) or 14 days post experiment start (14D). FPKM represents normalized counts. Normalized counts are included in files, but can't be used for Deseq 2 analysis.
2. Options with those files:
     1. Clean files and merge them into one file with code to run DESeq2 analysis for making plots.

     1. We didn't do this; instead we were exploring specific genes, which are in Genes_of_intrest.csv file.
     2. Our workflow was using Genes_of_intrest in deseq2 analysis for creating a heatmap and t-test statistics with code in Heatmap&T-Test.ipynb file. Also created a volcano plot for showing t-test results. DeSeq2 code from: https://github.com/mousepixels/sanbomics_scripts/blob/main/PyDeseq2_DE_tutorial.ipynb.
     3. Then, used GSM files for making a volcano plot of genes to compare expression between infected samples and control samples, and find genes with significant differences in expression. Code for that is in this file:
     4. Then, used GSM files for creating Gene-Gene analysis of genes in infected vs control samples. After that, we did a gene ontology exploration and Principal Component Analysis. Code for those diagrams is here:
  
3. Explanations of other files in this repo:
     1. rawcountdata.xlsx is a file of all the raw counts and their genes by samples, with normalized counts removed. Can be used in the same way like Genes_of_intrest file for this workflow. Was created manually through Excel, not by code.
     2. CreatingCleanRNADataset.ipynb is code for making cleaner RNA datasets and for data wrangling. Was not used in this project, but could be used with rawcountdata.xlsx to clean the file and make it easier to use with Deseq2 analysis.
     3. a549protein_names.xlsx is a file of protein names and gene ids for certain antimicrobial peptide precoursor proteins. This file was used to find our genes of intrest, by using the top 16 proteins by MAPP Score.
