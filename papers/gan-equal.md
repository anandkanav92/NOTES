
# Are all GANs created equal? 
[pdf](https://arxiv.org/pdf/1711.10337.pdf) 12$^{th}$ Dec 2018
## Introduction
## Metric
- Inception score 
	- It offers a way to quantiatively evaluate the quality of samples generated using GAN. Inception network classify the generated images and predict the label for it. This reflects the quality of the image.
	- It has two criterias, saliency and diversity, that the distribution obtained has low entropy i.e samples contain meaningful objects and the samples vary enough to cover all majority of the classes. Saliency is expressed as $p(y|x)$ (think of it as single high score and rest very low). While Diversity, $p(x)$ is overall distribution of the classes across sampled data. (well balanced training set)
	- Finally, inception score is defined as $$ IS(x) = e^{E_x[KL(p(y|x) || p(y)]}$$
	- Kullback-Leibler distance(KL distance)
		- Given two distributions, KL distance find the better fit. 
		- One is observed while other is the approximated version of the distribution. It is not the distance metric because it isn't symmetric.
		- Expressed as, $D_{KL} (Observed || Approximated) = E[log p(x) - log q(x)]$
- Fréchet Inception Distance(FID)
	- Features are extracted from an intermediate layer of Inception Net. The data is fit on multivariate gaussian distribution and FDI is calculated b/w generated data and real data using $$ FID(x,g) = ||muh
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4Mjg0ODI3NzcsLTEyNzExNzc4NiwtMz
c5MTU1OTExLC01MDk5Mjg3ODMsOTMyMjQ1MTE5LC0xNTcyMzAx
MjI3LC0yNzE1MzY1MTZdfQ==
-->