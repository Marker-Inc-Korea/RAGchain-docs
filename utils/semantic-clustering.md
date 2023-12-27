# SemanticClustering Class

This class is used to cluster the passages based on their semantic information.
First, we vectorize to embedding vector for representing each passages' semantic information.
Second, we cluster the embedding vectors by using various clustering algorithm.

There are no optimal clustering algorithm for all cases. So, you can try various clustering algorithm.

## Class Initialization

The class is initialized with two parameters:

- `embedding_function`: An instance of the `Embeddings` class. You can get `Embeddings` instance by using [`EmbeddingFactory`](./embedding.md) class easily.

- `clustering_algorithm`: A string that specifies the clustering algorithm to be used. The default value is `'kmeans'`. The supported algorithms are: 'affinity_propagation', 'agglomerative_clustering', 'birch', 'dbscan', 'kmeans', 'mean_shift', 'optics', and 'spectral_clustering'. All of these algorithms are from the `sklearn.cluster` module.


## Usage

To use the `SemanticClustering` class, you need to first create an instance of the `Embeddings` class and pass it to the `SemanticClustering` constructor along with the name of the desired clustering algorithm. 
Then, you can call the `cluster` method with a list of `Passage` objects to get the clusters.

```python
semantic_clustering = SemanticClustering(embedding_function=EmbeddingFactory('openai').get(), clustering_algorithm='kmeans')

# Cluster the passages
passages = [<your passages>]
clusters = semantic_clustering.cluster(passages, n_clustres=10)
```
