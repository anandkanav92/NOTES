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
This stuexperimental setup w
Since this study focus on comparing the overall performance of different GAN algorithms, it becomes challenging to keep the comparison fair without exploring every possibility in each dimension. Thus, the researchers make design choices to limit the dimensions while trying to keep the comparision fair and neutral.
- only one architecture - INFO GAN was used for all models. 
- Choice of hyper-parameters is limited by usi
 
 using hyperparameter optimisation (using random search)
        > Written with [StackEdit](https://stackedit.io/). 
<!--stackedit_data:
eyJoaXN0b3J5IjpbODM2MTE3OTYyLDE0NTE0MTk5OTksMTE3Mj
IwOTMyMSwxNTk3MTk0NjM0LDE3OTg4MjI4MjMsOTgxNzY5ODI3
LDg3MTkzODIxOSw3OTI1MDE2MTIsMjExNzcyOTA1NCwtMTY5Nj
cxNTczMiwxNzY4OTgyMjQyLDIwMDkyMTE2ODIsMTQyOTg2NjI2
NCwxMTI0NTU3NDMsLTE2MDEzMDA3MzcsLTY2NzA4NzUxLC00Nj
I4MDEwMzYsODI1OTI4MDIwLDY4NzgwODM5XX0=
-->