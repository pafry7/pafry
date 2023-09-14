---
title: Record linkage
---

>https://recordlinkage.readthedocs.io/en/latest/about.html#introduction

>https://uwaterloo.ca/networks-lab/blog/pre-processing-recordlinkage

Linking together information from many records, that are believed to belong to the same entity.

## Steps
#### 1. Preprocessing

This step involves transforming messy data into a usable format by cleaning and standardising it.

```
# Removes unwanted tokens, whitespace and brackets
recordlinkage.preprocessing.clean()
```

#### 2. Indexing

In this stage, we create pairs of records (candidate links) while excluding obvious non-matches. This can also be used for duplicate detection.


|Method|Description|Advantages|Limitations|
|---|---|---|---|
|0. **Full Index**|Keeps all possible links as candidate links.|Convenient when performance isn't an issue.|Highly inefficient with large data sets.|
|1. **Block Index**|Retains only links that are exactly equal on specified values as candidate links.|Extremely effective for high-quality, structured data.|Does not allow approximate matching.|
|2. **Sorted Neighbourhood Index**|Ranks rows by some value and creates candidate links between rows with nearby values.|Useful for making approximate matches.|More conceptually difficult.|
|3. **Random Index**|Generates a random set of candidate links.|Useful for developing your data integration workflow on a subset of candidate links or creating training data for unsupervised learning models.|Not recommended for your final data integration workflow.|

Source: https://uwaterloo.ca/networks-lab/blog/indexing-candidate-links-recordlinkage

```
# A window size of 1 returns the blocking index
recordlinkage.index.SortedNeighbourhood(on="column_name",window=1)
```

#### 3. Comparing

Comparing record pairs with provided methods:
- `compare_vectorized` - comparing of values with custom function.
- `exact` - comparing exactly. Similarity is 1 in case of agreement and 0 otherwise.
- `string` - comparing with string algorithm. Computing partial similarity between string values with selected algorithm: `jaro`, `jarowinkler`, `levensthein`, `damerau_levensthein`, `qgram`, `cosine`. Similarity is 1 in case of agreement and 0 in case of complete disagreement. You can pass threshold - comparison value higher than threshold will be considered as agreement
- `numeric` - comparing with numeric algorithm. Computing partial similarity between numeric values with selected algorithm: `step`, `linear`, `exp`, `gauss`, `squared`.
- `geo` - comparing with geo algorithm. Computing the partial similarity between WHS84 coordinate values with selected algorithm: `step`, `linear`, `exp`, `gauss`, `squared`.
- `date` - comparing with date algorithm.

```
# Custom methods may provide better results
compare.compare(normed_lcss, "Affiliation", "name", name="lcss")   compare.compare(normed_fuzzy_lcss, "Affiliation", "name", name="fuzzy_lcss")
```

#### 4. Classification
Process of classifying record pairs into matches, non-matches and possible matches. 

Three ways of classifying:
1. Threshold-based - sum of all comparison scores and setting arbitrarily a threshold
2. Supervised learning - models trained based on data provided by a user.
3. Unsupervised learning

Metrics used for evaluating the classification:
1. Precision
	$P = \frac{T_p}{T_p+F_p}$
 where 
 $T_p$ - number of true positives
 $F_p$ - number of false positives
1. Recall 
	$R = \frac{T_p}{T_p+F_n}$
 where 
 $T_p$ - number of true positives
 $F_n$ - number of false negatives
3. F-measure - a combination precision and recall

 Learn more: [Precision-Recall Metrics](https://mlu-explain.github.io/precision-recall/)

#### Example

For an illustrative example, check out this [Colab Notebook](https://colab.research.google.com/drive/10Cena0BuzNw-LwmoDlmkwBx1jXmq2yua?usp=sharing).

#### Next steps

Future steps may include training the model, as well as saving and loading it for further use.