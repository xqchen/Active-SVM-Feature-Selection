# Active feature selection in single-cell mRNA-seq data

To test the performance of the method in paper "Scalable Construction of Compressed Gene-sets from Single-cell Data Using Active Feature Selection", we applied our active feature selection method to extract minimal classifying gene sets for human PBMCs.

Run "main.ipynb" directly. 

Data
----------

We applied the method to a data set from ["Massively parallel digital transcriptional profiling of single cells"](https://www.nature.com/articles/ncomms14049) that contains 10194 cells profiled via single-cell transcriptional profiling. We used Louvain clustering to identify T-cells, activated T/NK cells, B-cells, and  Monocytes). You can download the data [PBMCnorm_final.csv](https://caltech.box.com/shared/static/wqvm0d9irzb7tneb16q01fnr4dt6cvl0.csv)

Preprocessing
----------

The data we would load in main.ipynb is already preprocessed. We only need to do 'l2'-norm along each cell to train SVM better and faster. 

For other datasets, preprocessing.ipynb should be good guidance for data preprocessing. It first normalizes the data by dividing the column sum (cells) then rescales and logs the data. If you want a smaller dataset, you could filter out genes by Poisson.

Parameters
----------

There are three hyper-parameters we need to set: balance, num_features, num_samples.

- balance(boolean) : balance the number of cells of each class or just randomly select cells at each loop
- num_features(int) : the total number of genes we want to select 
- num_samples(int) : the number of cells we would use at each loop


Compare with Other Methods
----------

Our active SVM feature selection(ASFS) strategy iteratively selects cells and constructs a gene list while calculating the classification accuracy on the multi-task SVM classification task. On the PBMC data, the procedure constructs gene sets of increasing size that can reproduce cell type clusters and classify the 5 cell-types at greater than 85% accuracy down to as few as 15 genes. On this classification task, aSVM outperforms than other methods including conventional Sequential Feature Selection, conventional SVM, correlation coefficien, mutual information, Chi-square, and feature importance by decision tree.

Advantages of Our Methods
----------

A key benefit of the active learning strategy is that is fast. The first reason is that a relatively small fraction of the data set is analyzed, so that the procedure can generate these gene sets while only computing across a small subset of cells. The other reason is that the program implement it in parallel using [parfor](https://pypi.org/project/parfor/) package. 

In addition to enabling classification of the cell-types in the data set, the ASFS gene sets provide a low-dimensional space in which to analyze the data. When we reduced our analysis to consider only the top 100 genes selected by the ASFS algorithm, we can generate a low-dimensional representations of the cell population (t-SNE) that preserve important structural features of the data including the distinct cell-type clusters.

Result Figures
----------

![PBMC_organized_flipped](https://user-images.githubusercontent.com/32661461/111823639-26551100-8920-11eb-819f-0f36ad4e5518.png)

