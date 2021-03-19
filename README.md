# Scalable-Construction-of-Compressed-Gene-sets-from-Single-cell-Data-Using-Active-Feature-Selection

Data
----------

To test the performance of the method in paper "Scalable Construction of Compressed Gene-sets from Single-cell Data Using Active Feature Selection", we applied our active feature selection method to extract minimal classifying gene sets for human PBMCs. Specifically, we applied the method to a data set from ["Massively parallel digital transcriptional profiling of single cells"](https://www.nature.com/articles/ncomms14049) that contains 10194 cells profiled via single-cell transcriptional profiling. We used Louvain clustering to identify T-cells, activated T/NK cells, B-cells, and  Monocytes). You can download the data [PBMCnorm_final.csv](https://www.dropbox.com/s/eqxtpnyooz3pnl9/PBMCnorm_final.csv?dl=0)

Preprocessing
----------

Parameters
----------

We select 100 genes totally and use 100 cells at each step. Hence the parameter num_feature=100 and num_samples=100.


Compare with Other Methods
----------

Our active SVM feature selection(ASFS) strategy iteratively selects cells and constructs a gene list while calculating the classification accuracy on the multi-task SVM classification task. On the PBMC data, the procedure constructs gene sets of increasing size that can reproduce cell type clusters and classify the 5 cell-types at greater than 85% accuracy down to as few as 15 genes. On this classification task, aSVM outperforms than other methods including conventional Sequential Feature Selection, conventional SVM, correlation coefficien, mutual information, Chi-square, and feature importance by decision tree.

Advantages of Our Methods
----------

A key benefit of the active learning strategy is that a relatively small fraction of the data set is analyzed, so that the procedure can generate these gene sets while only computing across 200-300 cells. At each iteration, a set number of mis-classified cells (n=100) are selected but the total number of cells used does not increase in increments of 100, since some cells are repeatedly mis-classified and are thus repeatedly used for each iteration.
In addition to enabling classification of the cell-types in the data set, the ASFS gene sets provide a low-dimensional space in which to analyze the data. When we reduced our analysis to consider only the top 100 genes selected by the ASFS algorithm, we can generate a low-dimensional representations of the cell population (t-SNE) that preserve important structural features of the data including the distinct cell-type clusters.

Result Figures
----------

![PBMC_organized_flipped](https://user-images.githubusercontent.com/32661461/111823639-26551100-8920-11eb-819f-0f36ad4e5518.png)

