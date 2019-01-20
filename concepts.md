
# Every Concept explained

#### Important concepts :thought_balloon: 

##### 7th December 2018

# ANOVA
- Anova is statistical concept used to gather the relationships between multiple groups. 
- It uses F ratio to either accept or reject the hypothesis that all the different groups have same mean and do not vary from each other beyond a certain threshhold.
$$ Fscore = \frac{SSB*1/DOF}{SSW*1/DOF} $$
where, SSB = sum of squares difference between the groups and SSW = sum of squares difference within the group.
- DOF is calculated by checking number of unknown variables - 1 (because we know mean and hence easy to find the last value of the group)

# Forward Selection
- Forward selection is a type of stepwise regression which begins with an empty model and adds in variables one by one. In each forward step, you add the one variable that gives the single best improvement to your model.
- Forward selection typically begins with only an intercept. One tests the various variables that may be relevant, and the ‘best’ variable — where best is determined by some pre-determined criteria– is added to the model.

- As the model continues to improve (per that same criteria) we continue the process, adding in one variable at a time and testing at each step. Once the model no longer improves with adding more variables, the process stops.

- The criterion used to determine which variable goes in when are varied. You could be attempting to find the lowest score under cross validation, the lowest p-value, or any of a number of other tests or measures of accuracy.

- Since stepwise regression tends toward over-fitting, it is usually good to have strict criteria for adding in any variables. (Overfitting happens when we put in more variables than is actually good for the model; it typically shows a very close, neat fit of the data used in regression, but the model will be far off from additional data points and not good for interpolation).

# Spearmans correlation
- Less strict than pearsons correlation. 
- Pearsons only for linear but spearsons check monotonic rlationship b/w two variables.
- need to rank the data before calculating.
![spearsons](images/spearman.png)

# MLE vs MAP
`https://wiseodd.github.io/techblog/2017/01/01/mle-vs-map/`

# Multi-Fidelity
`Why`
- with the onset of complex algorithms and huge datasets, it has become expensive to compute black box evaluation(since they need to run complete training)
- Training exceeds several hours or even days.
`How`
- search for good configurations on smaller subset of data
- learning model distribution to predict early stopping: http://aad.informatik.uni-freiburg.de/papers/15-IJCAI-Extrapolation_of_Learning_Curves.pdf
	- `why`
		-	The bayesian optimization algorithm has been found to work better than human experts but at the cost of more resources. One key reason is human can detect if the model will perform poorly after gew SGD steps and thus terminate it before complete evaluation.
	- `what`
		-  Thus, this method use learning curve models to predict the performanc of model few iterations and if the predicted performance is smaller than the current best, it stops the evaluation.
	- `how`
		- It records the performance of the model at resular intervals $y_1,y_2...y_n$. These points are used to predict the final performance of the model after many intervals. 
		- It uses set of parametric functions(11) combined linearly to give a single model. Each different model i is associated with a weight $w_i$ and additive gaussian noise $N(0,\sigma^2)$
		- 	The values are predicted using Markov Chain Monte Carlo (MCMC) inference. 
- Freeze-thaw Bayesian optimization - optional
- 
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI5NzUwNzA2MywxODU1NzQyOTE5LC01ND
I0MzA2OTQsLTExNjQ5OTIxOSwxMDI1MDU5NjI5LDk2MDk3OTcs
LTE5NjgyNzI1ODMsMTg4MzgzNzk5OSwtNDE3NTk5NjAsLTM4MT
M3NTYyNSw1NDg1OTkzMjksODgyNzU4NTUyXX0=
-->