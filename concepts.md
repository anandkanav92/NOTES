
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
		- 	The values are predicted using Markov Chain Monte Carlo (MCMC) inference. Procedure: keep track of best performance so far(Threshhold). y starts from $-\infinite$ and keep updating after regular intervals. y is the predicted final performance after $e_{max)$. on termination it returns validation error 1-expected accuracy. Else if predicted performance is greater than current best, it keeps on running.
	-`results`
		- on cifar 10 fully connected layer, it inmproves the speed by the factor of 2. using bayesian optimisation, SMAC,TPE. total 52 hyperparameters. $10(NHP)+6(Layers)*7(LHP)=52HP$
- another paper with similar concept but using bayesian neural networks instead of these functions as basis.
- Freeze-thaw Bayesian optimization 
	- Bag of 10 possible hp configs. You run m iterations and project the results. each projections will have parameters like mean, variance. This is used to refit the gaussian process over the performance function. 
	- from this set, based on the result, throw away the least performing m observations and initialise new random configs instead. repeat.
	- `cons` makes assumptions about accuracy curve, gaussian (so does everyone else right)
- `non-stochastic best-arm identification problem` https://arxiv.org/pdf/1502.07943.pdf
	- `what is successive halving algorithm`
		- add the algorithm image
		- it considers the fix size of iterations, and after fixed number of lever pulls it eliminates half of the worst performing ones. 
		- the number of iterations are based on the initial budget and the size of the inital set of hyperparameters.  ($r = \frac{B}{S*log_2(n)}$) 
		- end output is the best performing configuration singleton set of hyperparameters
	- `cons`
		- Major con is the number of configurations vs budget trade off. The user has to decide before hand whether to assign more budget to each configuration or to include many configurations but each with small budget. Assigning small -> premature termination of good configurations and large -> poor configurations running for long time and exploiting resources.
- `Hyperband` - http://www.jmlr.org/papers/volume18/16-558/16-558.pdf
	- `why`
		- number of configuration vs budget trade off. Also, bayesian optimization seems to surpass random search but by a small margin.   
	- `What?`
		- Rather than treating the given HPO problem as configuration selection, it treats it as configuration evaluation problem. 
		- It selects configurations at random and use successive halving algorithm for early stopping of these algorithms that do not show any promise. 
		- It solved the problem of specifying configurations vs budget algorithm by dividing the problem into several combinations of successive halving.
		- Shown to improve over random search and black box bayesian optimisations and takes only a constant time more when compared to vanilla random configuration.
		- doesn't use covariance between HPs and Loss function. 
 - `cons` It uses random search and thus can be further improved using existing knowledge to select new configurations. There comes BOHB. 
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMxOTMxNDM0NSwtMjAzNzY0NjYyLDE1OD
cxNjA5MDAsLTY2NDAwODc0MSw3NzU4OTUyNSwtOTY0NzYzNTMw
LC04MDYxNDY1MjIsMTQ4Mzg0MjM5MiwtMTIyNjI3MTU5MCw3OT
kxODgwNzMsMTk1MTkxOTkwLDE2NjU2MTU3ODMsMTg1NTc0Mjkx
OSwtNTQyNDMwNjk0LC0xMTY0OTkyMTksMTAyNTA1OTYyOSw5Nj
A5Nzk3LC0xOTY4MjcyNTgzLDE4ODM4Mzc5OTksLTQxNzU5OTYw
XX0=
-->