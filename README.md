# Clustering Lab: Hierarchical and DBSCAN on the Wine Dataset

## Purpose of the Lab
This lab was completed to explore two unsupervised machine learning techniques, **Agglomerative Hierarchical Clustering** and **DBSCAN**, using the Wine dataset from `sklearn`. The main goal was to understand how clustering algorithms group similar observations without using labels during training, and how parameter choices affect the final cluster structure.

The lab also focused on:
- preparing and standardizing real dataset features before clustering,
- visualizing clusters using PCA-based scatter plots,
- interpreting a dendrogram for hierarchical clustering,
- evaluating clustering quality using **Silhouette Score**, **Homogeneity Score**, and **Completeness Score**, and
- comparing the strengths and limitations of both algorithms based on actual results.

## Key Insights from the Results and Visualizations
### 1. Hierarchical Clustering produced meaningful groups
Hierarchical clustering gave the strongest result in this lab. After testing different values of `n_clusters`, the final model was built using **3 clusters**, which made sense because the Wine dataset contains three known wine classes.

The cluster counts from the final hierarchical model were:
- Cluster 0: **58 samples**
- Cluster 1: **56 samples**
- Cluster 2: **64 samples**

The evaluation results for Hierarchical Clustering were:
- **Silhouette Score:** 0.2774
- **Homogeneity Score:** 0.7904
- **Completeness Score:** 0.7825

These values showed that the hierarchical approach captured the dataset structure reasonably well. The PCA scatter plots also showed visible grouping patterns, and the dendrogram helped confirm that the data had a natural multi-level structure.

### 2. The dendrogram was useful for interpreting structure
One of the most useful visualizations in the lab was the dendrogram. It showed how individual data points were merged into larger groups step by step. Larger vertical jumps in the dendrogram suggested clearer separation between groups, which supported choosing a cluster count around **3**.

### 3. DBSCAN was highly sensitive to parameter choice
DBSCAN behaved very differently from hierarchical clustering. Multiple combinations of `eps` and `min_samples` were tested to observe how density-based clustering changes as the parameters change.

For the final selected DBSCAN model (`eps=1.2`, `min_samples=5`), the result was:
- **Number of clusters:** 0
- **Number of noise points:** 178

That means the model classified **every single point as noise**. Because DBSCAN did not form more than one valid cluster in the final setting, the silhouette score was **not applicable**.

The evaluation results for the final DBSCAN run were:
- **Silhouette Score:** Not applicable
- **Homogeneity Score:** 0.0
- **Completeness Score:** 1.0

This outcome showed that DBSCAN can be difficult to tune, especially when the density structure of the data is not very clear under the chosen parameters.

### 4. Visualizations made the comparison easier to understand
The scatter plots were important because they made the difference between the two clustering methods easy to see. Hierarchical clustering created visible groupings in the 2D PCA projection, while DBSCAN’s final result showed that the selected density settings were too strict for the dataset and ended up treating all observations as outliers.

## Challenges Faced and Decisions Made During the Lab
### 1. Choosing the number of clusters for Hierarchical Clustering
A key decision in hierarchical clustering was selecting the right value of `n_clusters`. Instead of assuming one value immediately, several values were tested first. The dendrogram and the known structure of the Wine dataset both helped support the decision to use **3 clusters** for the final model.

### 2. Selecting DBSCAN parameters was the hardest part
The biggest challenge in the lab was tuning DBSCAN. Unlike hierarchical clustering, DBSCAN does not require the number of clusters in advance, but it depends heavily on the values of `eps` and `min_samples`. Small changes in these parameters can completely change the result.

In this notebook, several parameter combinations were explored before settling on a final example for evaluation. The final chosen values ended up being too strict, which resulted in all observations being labeled as noise. Even though that result was weak, it was still useful because it demonstrated how sensitive DBSCAN is to parameter selection.

### 3. PCA was used for visualization
Because the Wine dataset has many features, direct plotting would have been difficult. PCA was used to reduce the standardized data to two principal components for visual interpretation. This made the cluster plots readable while still preserving a meaningful amount of the original variance.

### 4. Honest interpretation was more important than forcing a “good” result
One important decision during the lab was to report the clustering results honestly rather than adjusting the write-up to make both algorithms appear equally successful. The notebook shows that Hierarchical Clustering worked better for this dataset, while DBSCAN struggled under the selected settings. That comparison is actually one of the most valuable lessons from the lab.

## Overall Takeaway
This lab showed that clustering performance depends not only on the dataset, but also on how well the algorithm matches the structure of that data. **Hierarchical Clustering** was the better fit for the Wine dataset because it formed clear, balanced groups and provided interpretable visual structure through the dendrogram. **DBSCAN** was still valuable to test, but its final outcome showed that density-based methods can be very sensitive to parameter choices and may fail if the parameters are not well matched to the data.
