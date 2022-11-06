# DGAT-cancer
1. Organize the data file as in cancer.list.Rdata. Gene symbols in rownames and feature names in colnames.
2. laplacian_and_hotelling_box-box_transform.R. 
   The data file then put into the laplacian feature selection to find the most important features. Then the selected features would be transformed using Hotelling and Box-cox to generate weights of genes, which were used as sampled weight in Gibbs sampling.
3. gibbs _sampling.R
   The weighted score file generated in Step 2 was used as input to obtain a convergent probability distribution of candidate genes. 
4. random_permutation.R
   The weighted score file generated in Step 2 was used as input to constructed a null distribution of PP in order to obtain the likelihood of a given gene being a cancer driver gene.
5. 
