
# Are all GANs created equal? 
[pdf](https://arxiv.org/pdf/1711.10337.pdf) 12$^{th}$ Dec 2018
## Introduction
## Metric
- Inception score 
	- It offers a way to quantiatively evaluate the quality of samples generated using GAN. 
	- It has two criterias, saliency and diversity, that the distribution obtained has low entropy i.e samples contain meaningful objects and the samples vary enough to cover all majority of the classes. Saliency is expressed as $p(y|x)$ (think of it as single high score and rest very low). While Diversity, $p(x)$ is overall distribution of the classes across sampled data. (well balanced training set)
	- Finally, inception score is defined as $$ IS(x) = e^{E_x[KL(p(y|x) || p(y)]}$$
	- Kullback-Leibler distance(KL distance)
		- Given two distributions, KL distance find the better fit. 
		- One is observed while other is the approximated version of the distribution. It is not the distance metric because it isn't symmetric.
		- Expressed as, $D_{KL} (Observ
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk2ODE0NTUwMywtNTA5OTI4NzgzLDkzMj
I0NTExOSwtMTU3MjMwMTIyNywtMjcxNTM2NTE2XX0=
-->