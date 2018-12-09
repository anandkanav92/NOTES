

# Every paper summary

#### Important snapshots of all the papers :thought_balloon: 

## An Efficient Approach for Assessing Hyperparameter Importance 
[pdf](http://proceedings.mlr.press/v32/hutter14.pdf)
7th Dec 2018
#### Summary
- The paper tried to find the impact of each hyperparameter on the overall performance of the given model. It uses the perfromance data and fits random forest model to make decisions trees based on gathered data. These trees are used to calculate the importance of each hyperparameter in general setting using ANOVA framework.
- The key idea behind the algorithm is to exploit the fact that each of the regression trees in a given forest defines a partitioning P of the configuration space Θ, with piecewise constant predictions ci in each Pi ∈ P, and that the problem of computing sums over an arbitrary number of configura- tions thus reduces to the problem of identifying the ratio of configurations that fall into each partition.  

## Identifying Key Algorithm Parameters and Instance Features using Forward Selection

- This paper uses forward selection -  adding the hyperparameters one by one in the input set and observing the performance of the model. 
- It creates a ML model using performance data and predicts the performance using this model.
- Given a model f that takes k parameters and m instance features as input and predicts a performance value, we identify the best values for the k parameters by optimizing predictive performance according to the model. Specifically, we predict the performance of the partial parameter configuration x (instantiating k parameter values) on a problem instance with m selected instance features z as $$ f([x T , z T ] T ) $$  Likewise, we predict its P average performance across n instances with selected instance features z1, . . . , zn as $$ \sum_{i=0}^n  n_j= \frac{1}{n} * f([x^T , z_j^T]^T ) $$




<!--stackedit_data:
eyJoaXN0b3J5IjpbNTg1OTYyODkwLDYyNDY3OTc5MywtMTk2NT
E1NzM2NiwtMTgxMzQ2MDE3NiwtNTAwMTE1NDY1LC0yMjE1NjYy
ODJdfQ==
-->