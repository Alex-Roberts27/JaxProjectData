# Jackson Labs Winter 2026 BDISC cohort Project on Proteasome Derived Antimicrobial Defense Peptides (PDADP) in Immune Tissues

Bulk RNA-seq Mouse bone marrow dataset obtained fro Lin and colleagues 2021 (https://doi.org/10.1128/iai.00814-20). 
     GEO accesion number: GSE166522(https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE166522)

Protein data from Goldberg and colleagues 2025: https://www.nature.com/articles/s41586-025-08615-w#Abs1

Presentation here: [https://1drv.ms/p/c/d09893c430a34e2b/IQCuI_Lgmok4Q6rif4xR_wZFATZ3Fc9pwB6x46VcJNx_hcY?e=H4jm1Q
](https://docs.google.com/presentation/d/1zRQ5v92g9lMy2Um5BXbrCuwpzMStVxTcj4Y34F-IoSw/edit?usp=sharing)

Layout:
1. Pre-processed Bulk RNA-seq Data [Bone Marrow Bulk-seq Dataset_Lin et al 2021_GSE166522] represent raw RNA counts for transcripts (genes) in mice either infected with a S. Aureus bacteria, or controls. Samples come from Mice 3 days(3D) post experiment start (n=6) or 14 days(14D) post experiment start (n=6). FPKM represents normalized counts, provided from Lin et al., 2021, controlling for transcript length and GC bias. Raw counts were used for Deseq2 analysis to produce volcano plot; while remaining analyses were done with normalized counts.

2. PDADP protein list file [PDADP Protein_names_Goldberg et al 2025_rom A549 cells.xlsx], from Goldberg et al., 2025, was produced from proteomics analysis of small peptide secretions of cultured human A549 cells exposed to various bacterial agents. Peptide sequences were already alignd to precursor proteins and machine learning derived MAPP score indicates antimicrobial activity of each peptide.

3. Python code used to produce all data-based fiuges in presentation [JAX_2026_PDDP_immune_Maya,_Alex_&_Wimeth_Project.ipynb] is shown in colab file. Contents are described more thoroughly in workflow.

4. Intermediate files [Processed Files] created and utilized by python code to produce graphs, communicate between modules, and allow for visualization in excel and PRISM.

5. Workflow:

:: Initial Data Processing ::
    <br> 1. Clean PDADP protein list and convert to gene names which can be used to query transcriptomic data.</br>
           <br>a. First module is from blood PDADPs (test control), second is for A549 derived PDADPs (used for experimental figures).</br>
           <br>b. MAPP score was gated at >5 to identify PDADPs, per Goldberg et al., protocol. </br>
     <br> 2. Wrangle Bulk-RNAseq dataset into 1 csv.</br>
           <br>a. First module is to import dataset xlsx files.</br>
           <br>b. Merges files into 1 csv, with each sample raw count and fpkm being appended to dataframe. </br>
          
:: Gene vs. Sample Correlation Analysis:
      <br>3. Utilizing pyDeSeq2 to produce data for volcano plot. [DeSeq2 code from: https://github.com/mousepixels/sanbomics_scripts/blob/main/PyDeseq2_DE_tutorial.ipynb.]</br>
           <br>a. Module installs packages: pydeseq2, os, pickle, and numpy.</br>
           <br>b. Reorganizing dataframe to comply with volcano plot input format.</br>
           <br>c. Removes 0 values which cause DeSeq2 errors.</br>
           <br>d. Creating metadata file for DeSeq2 input.</br>
           <br>e. Mutliple modules run Deseq and obtains padj and log10(change) for genes of interest.</br>
      <br>4. Produces Volcano plot utilizing sanbomics.plots package.</br>
      <br>5. Produces bar plot using volcano plot analysis from DeSeq2 for both healthy and infected tissues.</br>
     
:: Gene vs. Gene Correlation Analysis
      <br>6. Conducts pairwise comparisons of all genes in RNAseq database, filtered for low variance genes.</br>
          <br> a. Utilizes seaborn package [https://seaborn.pydata.org/generated/seaborn.heatmap.html] to produce heatmap.</br>
           <br>b. Cluster heatmap with seaborn package [https://seaborn.pydata.org/generated/seaborn.clustermap.html] to identify PDADP gene clusters.</br>
           <br>c. Creates gene_matrix.csv at end of module for future analysis.</br>
      <br>7. Utilizes gene ontology analysis to identify possible functional similarities between coexpressed genes in different clusters.</br>
         <br>  a. Uses gseapy pakcage [https://github.com/zqfang/GSEApy] to conduct gene ontology.</br>
          <br> b. Maintains clustering with Scipy [https://docs.scipy.org/doc/scipy/reference/cluster.hierarchy.html] and creates heirarchical functional categories.</br>
          <br> c. Called gene ontology databases from JAX MGI [https://www.informatics.jax.org/function.shtml] </br>
     <br> 8. Uses skikit package to conduct principal component analysis on gene-gene correlations [https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html]</br>
       <br>    a. First module only shows PDADP genes.</br>
        <br>   b. Second module adds in antigen processing genes (APGs).</br>
     <br> 9. Adapts code from SGALELLA [https://www.kaggle.com/code/sgalella/correlation-heatmaps-with-hierarchical-clustering] and Prasad Ostwal [https://ostwalprasad.github.io/machine-learning/PCA-using-python.html] to create heatmap mapping correlation of PDADP and APGs in PCA. </br>
      <br>10. Utilizes sklearn.cluster to cluster and then assign cell types, adapting deconvolution protocol described here: [https://github.com/theislab/AutoGeneS/blob/master/deconv_example/bulkDeconvolution_using_singleCellReferenceProfiles.ipynb]</br>
          <br> - Cell types assigned from dictionary [https://panglaodb.se/] specifically designed for tissue specific analysis of mice.</br>

7. Presentation [JAX BDSiC_Antimicrobial Defense Peptides Presentation_final.pptx] show summary of findings with background and scientific interpretation.

8. Explanations of other files in this repo:
     1. rawcountdata.xlsx is a file of all the raw counts and their genes by samples, with normalized counts removed. Can be used in the same way like Genes_of_intrest file for this workflow. Was created manually through Excel, not by code.
     2. CreatingCleanRNADataset.ipynb is code for making cleaner RNA datasets and for data wrangling. Was not used in this project, but could be used with rawcountdata.xlsx to clean the file and make it easier to use with Deseq2 analysis.
     3. a549protein_names.xlsx is a file of protein names and gene ids for certain antimicrobial peptide precoursor proteins. This file was used to find our genes of intrest, by using the top 16 proteins by MAPP Score.
