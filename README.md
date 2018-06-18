# Batch correction with mutual nearest neighbours

## Overview

This repository contains the code for the paper **Correcting batch effects in single-cell RNA sequencing data by matching mutual nearest neighbours** by [Haghverdi _et al._ (2018)](https://doi.org/10.1038/nbt.4091).

**Note:** Further updates and development of the analysis and simulation code will take place at https://github.com/MarioniLab/FurtherMNN2018.
If you have general questions regarding the code (i.e., not specifically involving the manuscript), please post your issues at the above repository instead.

## Regenerating the figures

1. To generate the simulation figure in the main text, first run the source file `simulateBatches.R`, then run the source file `FourPlots_sim.R` in the Simulations folder.

2. To generate the simulation figure in the supplement (identical composition of cell types), first run the source file `easysimulateBatches.R`, then run the source file `FourPlots_easysim.R` in the Simulations folder.

3. To generate the haematopoietic data figures in the main text, first run the source file `preparedata.R`, then  run the source file `FourPlots_haem.R` in the Haematopoiesis folder.

4. Then, to generate the haematopoietic data figures in the supplement, run the source file `PCAs.R` in the Haematopoiesis folder.

5. First download gene expression data from the four public data sets (Gene X Cell matrices, meta data and highly variable gene lists) by running the bash script `DownloadData.sh`.  This will download a zipped file, which contains the raw counts matrices for GSE86473.  The remaining data sets are downloaded directly in the data processsing scripts for the appropriate studies (denoted by GEO/ArrayExpress accession number detailed in the manuscript).

6. To run the data processing and normalization, move to this repository directory and execute the script `normalizePancreas.R` (via Source(), or interactively).  To calculate the highly variable genes, execute (or source) the script `findHighlyVariableGenes.R`, and to assign cell type labels according to the approaches described for each study, run the script `assignCellTypeLabels.R`.

7. To generate any of the pancreas data sets results, you have to run the source file `PancreasProcessingCorrection.R` in the Pancreas folder first. You will need to create a directory called 'results', into which all figures and batch corrected data will be saved.

8. To correct the batch effects and generate t-SNE plots and the Silhouette boxplots for the pancreas data sets (Fig 4 and Supplementary Figure 5), run the source file `PancreasCorrectionComparison.R` in the Pancreas folder.  This will also generate the pancreas PCA plots and the entropy of mixings boxplots in the supplement (Suppl. Fig.5).

9. To compare performance of MNN with locally variable batch effects versus a global batch effect settings (Suppl.Fig. 6), run the source file `local_global_batchvect.R` in the Pancrease folder.

10. Differential expression testing figures can be generated by running the R markdown document, `PancreasDE_analysis.Rmd` , contained in the PancreasDE directory.  The static version of the R notebook is also available as a html document that can be opened with any internet browser.

11. The scripts to download and normalize the 10X droplet data can be found in `Droplet/`, specifically `pbmc_normalisation.R` for the 68,000 PBMCs and `tcell_4K_normalisation.R` for the 4,000 T cells.  Please note that trying to normalise 68,000 cells on your local machine will require a lot of resources (memory and CPU), it is recommended that the scripts in the `Droplet/` are executed on an appropriate high performance computing cluster.  The scripts to perform tSNE and cluster assignment using community detection on the uncorrected data can be performed by running `uncorrected_68k_tSNE.R`, `assign_cell_types_68kPBMC.R`.  To perform the equivalent tasks to generate the panels of Figure 5, run `combine_10X.R`, `pbmc68k_tSNE.R`, `PBMC_68k_plotting.R`, `assign_cell_types_68kPBMC_corrected.R` and `Corrected_PBMC_68K_assignCellLabels.R`
