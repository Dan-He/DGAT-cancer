# DGAT-cancer
DGAT-cancer was a method for predicting cancer driver genes. It integrates the predicted pathogenicity of the somatic mutations (together with germline variants in the healthy population) with a topological network of gene expression in tumor tissues, and considering the expression levels in tumor and paracancerous tissues while employing 24 distinct features to predict novel cancer drivers.
## Algorithm
### 1.	Using Laplacian Score to select features
We used an unsupervised method, the Laplacian Score, to select features that have high power to preserve the local geometric structure of the features space. The detailed steps for the application of Laplacian Score in feature selection were as follows:
(1) A network ![](https://latex.codecogs.com/svg.image?\mathit{N}) was constructed to connect all m candidate genes (![](https://latex.codecogs.com/svg.image?\mathit{N}\in&space;\mathbb{R}^{\mathit{m}\times&space;\mathit{m}})). For each pair of genes, we calculated the Euclidean distance, ![](https://latex.codecogs.com/svg.image?\left|\mathit{x}_{i}-\mathit{x}_{j}&space;\right|) between their feature vectors (![](https://latex.codecogs.com/svg.image?\mathit{x}_{i}) is the feature vector of gene ![](https://latex.codecogs.com/svg.image?\mathit{i}), and ![](https://latex.codecogs.com/svg.image?\mathit{x}_{j}) is the feature vector of gene ![](https://latex.codecogs.com/svg.image?\mathit{j})). Based on the Euclidean distance, if gene ![](https://latex.codecogs.com/svg.image?\mathit{i}) is among the top ![](https://latex.codecogs.com/svg.image?\mathit{k}) (here we set ![](https://latex.codecogs.com/svg.image?k=\left&space;[&space;0.01\times&space;m&space;\right&space;])) of the nearest genes to gene ![](https://latex.codecogs.com/svg.image?j), or the gene ![](https://latex.codecogs.com/svg.image?j) is among the top ![](https://latex.codecogs.com/svg.image?k) of the nearest gene to the gene ![](https://latex.codecogs.com/svg.image?i) (![](https://latex.codecogs.com/svg.image?i\neq&space;j)), we set the connection between ![](https://latex.codecogs.com/svg.image?i) and ![](https://latex.codecogs.com/svg.image?j) as ![](https://latex.codecogs.com/svg.image?N_{ij}=1). Otherwise, ![](https://latex.codecogs.com/svg.image?N_{ij}=0). 




1.	Organize the data file as in cancer.list.Rdata. Gene symbols in row names and feature names in column names.
2.	Use laplacian_and_hotelling_box-box_transform.R. 
The data file was then put into the laplacian feature selection to find the most important features. Then the selected features would be transformed using Hotelling and Box-cox to generate weights of genes, which were used as sampled weights in Gibbs sampling.
3.	Use gibbs_sampling.R
The weighted score file generated in Step 2 was used as input to obtain a convergent probability distribution of candidate genes. The final selected frequencies were assigned as the posterior probabilities (PP) of candidate genes.
4.	Use random_permutation.R
The weighted score file generated in Step 2 was used as input to construct a null distribution of PP to obtain the likelihood of a given gene being a cancer driver gene. By counting the number of times that a random PP of a gene was larger than the real PP of the gene, an experience p-value was given. 
5.	The p-values were adjusted by Bonferroni correction and those genes with ![](https://latex.codecogs.com/svg.image?p_{adj})<0.01 were selected as being significant.

# Language
R (100%)
