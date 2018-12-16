
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
		- If you’re trying to find approximations for a complex (intractable) distribution 𝑝(𝑥)by a (tractable) approximate distribution 𝑞(𝑥) you want to be absolutely sure that any 𝑥 that would be very improbable to be drawn from 𝑝(𝑥) would also be very improbable to be drawn from 𝑞(𝑥). That KL have this property is easily shown: there’s a 𝑞(𝑥)𝑙𝑜𝑔[𝑞(𝑥)/𝑝(𝑥)] in the integrand. When 𝑞(𝑥) is small but 𝑝(𝑥) is not, that’s ok. But when 𝑝(𝑥) is small, this grows very rapidly if 𝑞(𝑥) isn’t also small. So, if you’re choosing 𝑞(𝑥)to minimize 𝐾𝐿[𝑞;𝑝], it’s very improbable that 𝑞(𝑥) will assign a lot of mass on regions where 𝑝(𝑥)p(x) is near zero.
		- If p(x) has x point where the distribution is very low, the impact of q(x) is minimized if it is larger. Similary, points where q(x) has low probability, it doesn't impact the overall distance from learning.
- Fréchet Inception Distance(FID)
	- Features are extracted from an intermediate layer of Inception Net. The data is fit on multivariate gaussian distribution and FDI is calculated b/w generated data and real data using $$ FID(x,g) = ||mean_x - mean_g||^2 + Tr(\sum_x + \sum_g - 2(\sum_x \sum_g)^\frac{1}{2})$$
	- results show robust nature of FDI, can detect intra class mode dropping i.e model that generates only one image per class can score high IS but not FID.
	- Inability to detect overfitting
- Precision, Recall and F1
	- If the generated images look very similar to real images on avg, high precision. $$ P_{recision} = \frac{tp}{tp+fp}$$
	- If the model can generate any sample found in the training set, high recall. $$ R_{ecall} = \frac{tp}{tp+fn}$$
	- Harmonic mean of precision and recall = F1 score. $$ F1 = 2 \frac{P R}{P+R}$$ 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTExNTY0ODkyLDE2NjI1MDM1MDMsMTIzOD
g3NjUwMiwxNDgxMzI1MDU3LC05OTAyMzUzMzIsLTE4Mjg0ODI3
NzcsLTEyNzExNzc4NiwtMzc5MTU1OTExLC01MDk5Mjg3ODMsOT
MyMjQ1MTE5LC0xNTcyMzAxMjI3LC0yNzE1MzY1MTZdfQ==
-->