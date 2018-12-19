 # Introduction 
  The purpose of the study was to evaluate different GAN algorithms and determine the possible differences in the overall performance among these algorithms. Various GAN algorithms have been introduced recently \footnote{https://github.com/hindupuravinash/the-gan-zoo}, and a majority of them have managed to achieve notable results. The paper designed the experiments and  metrics to test prominent GAN algorithms on neutral grounds. The results showed that if trained for long enough, all these algorithms achieve similar performance level and no modified GAN algorithms consistently outperform the original GAN 
  
# Goals

The main goal of this study to provide a rich comparison of major GAN algorithms and identify which algorithms performs better(or worse)  than others. This study also focuses on presenting a methodology to compare different GAN algorithms fairly and without any bias.

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

<b><u>Opinion</u></b>
The main issue with comparing different gan algorithm is the lack of robust metrics. In this study, a good deal of consideration is given to metrics. The use of these common metrics for each model provided the neutral grounds required for the comparison. 
The architecture was limited to only INFO GAN for all experiments. However, the choice of architecture does play an important role in deciding the final performance value of the model. \footnote{http://papers.nips.cc/paper/7159-improved-training-of-wasserstein-gans.pdf} 
The experiments varying computational budget is one of the most important contribution of this study. As it is implicit knowledge that any stable model trained long enough will provide "good" results. But it was never thoroughly validated.

# Results

For wide range setup, high variance in FID metric was found for each model. There was no single model which was found to be significantly stable than others. While for narrow range setup, the results shown are quite mixed. There are some models which are found to be more sensitive to hyperparameters than others. Overall, FID values were reported much lower for wide range hyperparameter search.
The study computes precision, recall and F1 score over the toy dataset. It was found that NSGAN outperforms other models in terms of F1 scores.
The study shows the impact of increasing computational budget. With the increase in budget, the minimum FID of the model decreases while  precision and recall increases for majority of the models except BEGAN. 
Except for LSGAN, all other models were found to be robust to random initialization of weights. 

<b><u>Opinion</u></b>
The results are clearly explained and well formulated. It depicts the importance of hyperparameter tuning in training a model. 
# Conclusions
This study started with the goal of comparing different GAN algorithms on neutral grounds. The paper first introduced the evaluation metric and emperical evidence supporting the choice. In order to make the research feasible, researchers makes pragmatic choices about experimental design and results were obtained. The results shows that there is no model that dominates other models. It was found that by increasing the computation budget(or performing more hyperparameter optimisation) can improve the performance of the model. Conversely, with the low budget it is difficult to make any significant inference of the model's performance.
Further, the claims of some models outperforming the Original GAN model are not supported by the found empirical evidence. The study concludes that future research in GAN comparison should be done on neutral grounds.

<b><u>Opinion</u></b>
This study concludes that majority of recently introduced GAN algorithms are no better than original GAN. It questions the experimental techniques used by some of these papers and show that there is a need to compare GAN algorithms on neutral grounds. These   
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI0MjUwNzQ1Niw4Mzg1NTYyMjEsMTE5Mj
E1NDM1NSwtMTc5Njc3Mzg5MiwtMTUyNDE3MTgzMiw5ODc4NzYx
NywyMTMwMjAzNDU1LDY5MDEwMTgzOCwxMTQ4NTk2NDI5LC02ND
Q3MTE3NTksNTc2NDAzNTk0LC0yMTM3MzE1NjY3LC01ODk3OTE2
NjYsLTU4OTc5MTY2Niw1MzAwNzQ2OTksLTE5OTk3NTA4NDUsMT
k3NDAyMDEzLC0xMTM1MTgxMDc2LDE1OTQ5Mjg3MzQsLTEwNjE2
MjY2NDldfQ==
-->