 # Paper review - GAN 
  The purpose of the study was to evaluate different GAN algorithms and determine the possible differences in the overall performance among these algorithms. Various GAN algorithms have been introduced recently \footnote{https://github.com/hindupuravinash/the-gan-zoo}, and a majority of them have managed to achieve notable results. The paper designed the experiments and common metrics to test prominent GAN algorithms on neutral grounds. The results showed that if trained for long enough, all these algorithms achieve similar performance level and no modified GAN algorithms consistently outperform the non-saturating GAN(Vanilla GAN). 
  # write about metrics used 

   # write about experiments 
   The researchers thoroughly explain the experiment design choices. The architecture, taken from INFO GAN, is used for all algorithms since none of these algorithms were designed to specifically work with this architecture. As it is infeasible to explore complete domains of each hyperparameter, authors limit it by following two approaches. First, hyperparameters are optimized for each data set (using random search) and other 
   
   # write about results 
   # write about conclusions 
   # write about limitations 
   # write about future work 
        
Article Summary
Problem

What affect does an 8-week instructional period have on the sight-reading skills on a beginning choir singer, and how does technology as well as previous experience affect the skills obtained during the instruction?

# Goals

The main goal of this study to provide a rich comparison of major GAN algorithms and identify which algorithms performs better(or worse)  than others. 

# Specific Research Questions

1. Which of the many GAN algorithm outperform others(If any)?
2. Is FID robust  to be used as  a metric to evaluate different   GAN algorithms?
3. Does the performance of a model vary with change in computational budget?
4. Is there is a significant difference in the performance of model when extensive hyperparameter tuning is performed?
5. Are models robust to initial weights?

# Hypothesis
There is no mention of direct hypothesis in this study. It focus more on seeking answers to implicit questions rather than having  preconcieved notions about it.
# Design
The authors use FID (Fréchet Inception Distance), precision, recall and F1 score to evaluate the models. Metrics like log-likelihood, inception score are discussed but the research claims FID is the best fit and robust to handle the task in hand, supported by empirical evidence.
The paper approximates the values of precision, recall and F1 score for each model using data manifolds. The study uses an intuitive way to calculate these metric efficiently. A new dataset is created(Toy dataset) with known probability distribution and squared euclidean distance is used to find the resemblance between generated and true samples. If all different types of images are generated, the recall is high. And precision is high when distance between generated images and training images is low. 
Further, this study evaluate each model using two major experimental setups. The  difference lies in the choice of hyper-parameters. First, referred as wide one-shot setup, identifies 100 samples of hyper-parameters using random search where as the other setup, termed as narrow two shot setups, uses 50 samples of hyperparameter selected manually using the results of wide one shot setup over single Dataset(FASHION-MNIST).    
Other design decisions  explained in the study includes the choice of  datasets(4 datasets from simple to medium complexity), choice of the architecture( INFO-GAN same for each model), random seed to make the initial weights in architecture random and computational budget. The budget is represented in terms of number of hyperparameters samples available  for the model.

# Results

For wide range setup, high variance in FID metric was found for each model. There was no single model which was found to be significantly stable than others. While for narrow range setup, the results shown are quite mixed. There are some models which are found to be more sensitive to hyperparameters than others. Overall, FID values were reported much lower for wide range hyperparameter search.
The study computes precision, recall and F1 score over the toy dataset. It was found that many
The study shows the impact of increasing computational budget. With the increase in budget, the minimum FID of the model decreases while  precision and recall increases for majority of the models except BEGAN. 
Except for LSGAN, all other models were found to be robust to random initialization of weights. 


The study tests the senstivity of the metric, FID, to mode dropping and encoding network used by the model,over four given datasets. The authors divide the dataset into two sets, train and test partitions, and calculate FID score between  test set and sampled train set. The sensitivity to mode dropping is estimated by gradually increasing the number of classes in the test set ranging from 1 to 10.

A number of other experiments were done to evaluate the importance of initial weights in generator and discriminator neural network



Since this study focus on comparing the overall performance of different GAN algorithms, it becomes challenging to keep the comparison fair without exploring every possibility in each dimension. Thus, the researchers make design choices to limit the dimensions while trying to keep the comparision fair and neutral.
- only one architecture - INFO GAN was used for all models. 
- Choice of hyper-parameters is limited by usi
 
 using hyperparameter optimisation (using random search)
        > Written with [StackEdit](https://stackedit.io/). 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU0NTMwNzMzNCwxNDI5OTQ5NjcwLDIxMT
cwMzY4ODgsLTYyOTgxNDMxNywxNDMxMTc2MDMwLDE2NzEzMTMy
MjcsLTU5Njk2ODg2LC04NDU3NjcwMDksLTU3ODQ3NDU1OCwxOT
IyMTk3NzM3LC04MzQ1MDUyNjMsNjczMTc3NTUxLC0xMDMyNDc0
MzAxLDU4MjUyMTYyNSwzNzg4OTA2MjksNDA4NzMzOTY0LDE0NT
E0MTk5OTksMTE3MjIwOTMyMSwxNTk3MTk0NjM0LDE3OTg4MjI4
MjNdfQ==
-->