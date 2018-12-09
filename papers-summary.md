

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

## Efficient Parameter Importance Analysis via Ablation with Surrogates

- The ablation analysis takes the source (default) configuration and the target configuration obtained either by automated or manual methods. It find the difference between these two configuration and records the performance changes for each configuration.
- We now describe ablation analysis on a high level.
Given a parameterised algorithm A with n configurable pa- rameters defining a configuration space Θ, along with a source configuration θsource and target configuration θtarget (e.g., a user-defined default configuration and one obtained using automated configuration), and a performance met- ric m (e.g., running time or solution quality), ablation analysis first computes the parameter setting differences Δ(θsource,θtarget) between the source and target configura- tions. Next, given a set Π of benchmark instances, an abla- tion path θsource,θ1,θ2,...,θtarget is iteratively constructed. In each iteration i with previous ablation path configura- tion θi−1, we consider all remaining parameter changes δ ∈ Δ(θi−1,θtarget) and apply the change to the previous ablation path configuration θi−1 [δ]. Each parameter change δ is a modification of one parameter from its value in θi−1 to its value in θtarget, along with any other parameter modifica- tions that may be necessary due to conditionality constraints in Θ. The next configuration on the ablation path θi is the candidate θi−1 [δ] with the best performance m on the set Π. This performance may be directly measured by performing runs ofA, or approximated for efficiency reasons. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbNDk0NDQ5MjM4LDM1NTk0ODQ3OCwtMTc0OD
k5Njg3OSw1ODU5NjI4OTAsNjI0Njc5NzkzLC0xOTY1MTU3MzY2
LC0xODEzNDYwMTc2LC01MDAxMTU0NjUsLTIyMTU2NjI4Ml19
-->