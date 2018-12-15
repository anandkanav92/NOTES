# Models 

## GAN

### Why generative modelling?
- To predict future i.e all the scenarios and could be used in reinforcement learning.
- Semi supervised learning to predict missing data
- Mutli modal outputs - for applications with multiple possible outputs.
- realistic generation tasks, generating images or audio waveforms.
![gan-architechture](gan.png)

### What is GAN?
- (GAN) has shown great results in many generative tasks to replicate the real-world rich content such as images, human language, and music.
- It is inspired by game theory: two models, a generator and a critic, are competing with each other while making each other stronger at the same time.
- A discriminator  DD  estimates the probability of a given sample coming from the real dataset. It works as a critic and is optimized to tell the fake samples from the real ones. 
- A generator  GG  outputs synthetic samples given a noise variable input  z(z  brings in potential output diversity). It is trained to capture the real data distribution so that its generative samples can be as real as possible, or in other words, can trick the discriminator to offer a high probability.
- Basically we try to maximise D's decisions over real data by maximizing $E_{x~p_r(x)}[logD(x)]$ and over fake data, $E_{z~p_z(z)}[log(1-D(z))]$
- Final loss function, $$ min_G max_D L(D,G) = E_x~p_r(x)[logD(x)] + E_{z~p_z(z)}[log(1-D(z))]$$
$$ = E_x~p_r(x)[logD(x)] + E_{x~p_g(x)}[log(1-D(x))]$$
- Taking derivative of this loss function and equation to 0, we get the optimal value where this loss function is minimum i.e D*(x) is optimal when $x = \frac{p_r(x)}{p_r(x)+p_g(x)}$ which is equal to $\frac{1}{2}$.

### Training problems

#### Nash problem
-	It's difficult to find a nash equilibrium point using a gradient based training procedure in a non cooperative game.
-	Because of the opposite signs of loss functions for each Neural network, it causes oscillations.

#### Disjoint in lower dimensions
- All the dimensions are found to be artificially high as they tend to concentrate in a lower dimension manifold. 
- $p_r$ and $p_g$ are disjont in low dimensions that means discriminator can achieve 100% results.
#### Vanishing gradient
- If the discriminator behaves badly, the generator does not have accurate feedback and the loss function cannot represent the reality.
- If the discriminator does a great job, the gradient of the loss function drops down to close to zero and the learning becomes super slow or even jammed.
#### Mode collapse
- the generator may collapse to a setting where it always produces same outputs
#### no good eval metric

### How to improve the training? 
#### Feature Matching

Feature matching suggests to optimize the discriminator to inspect whether the generator’s output matches expected statistics of the real samples. In such a scenario, the new loss function is defined as  ‖𝔼x∼prf(x)−𝔼z∼pz(z)f(G(z))‖22‖Ex∼prf(x)−Ez∼pz(z)f(G(z))‖22, where  f(x)f(x)  can be any computation of statistics of features, such as mean or median.

#### Minibatch Discrimination

With minibatch discrimination, the discriminator is able to digest the relationship between training data points in one batch, instead of processing each point independently.

In one minibatch, we approximate the closeness between every pair of samples,  c(xi,xj)c(xi,xj), and get the overall summary of one data point by summing up how close it is to other samples in the same batch,  o(xi)=∑jc(xi,xj)o(xi)=∑jc(xi,xj). Then  o(xi)o(xi)  is explicitly added to the input of the model.

#### Historical Averaging

For both models, add  ‖Θ−1t∑ti=1Θi‖2‖Θ−1t∑i=1tΘi‖2  into the loss function, where  ΘΘ  is the model parameter and  ΘiΘi  is how the parameter is configured at the past training time  ii. This addition piece penalizes the training speed when  ΘΘ  is changing too dramatically in time.

#### One-sided Label Smoothing

When feeding the discriminator, instead of providing 1 and 0 labels, use soften values such as 0.9 and 0.1. It is shown to reduce the networks’ vulnerability.

#### Virtual Batch Normalization

Each data sample is normalized based on a fixed batch (_“reference batch”_) of data rather than within its minibatch. The reference batch is chosen once at the beginning and stays the same through the training.

#### Adding Noises

Based on the discussion in the  [previous section](https://lilianweng.github.io/lil-log/2017/08/20/from-GAN-to-WGAN.html#low-dimensional-supports), we now know  prpr  and  pgpg  are disjoint in a high dimensional space and it causes the problem of vanishing gradient. To artificially “spread out” the distribution and to create higher chances for two probability distributions to have overlaps, one solution is to add continuous noises onto the inputs of the discriminator  DD.

#### Use Better Metric of Distribution Similarity

The loss function of the vanilla GAN measures the JS divergence between the distributions of  prpr  and  pgpg. This metric fails to provide a meaningful value when two distributions are disjoint

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIwNTU1NjUwMSwyNzYzMjQ2OTgsMjI1MD
k2ODQsLTE4NjE5MzMzOTgsODkzMzg1OTA3LC0xMTgzNTM4Nzg1
LC0yMDM2MzQyNTExLDE5NDAxOTkwNjIsMTAxMjA2NTI3MiwtMT
M2MjYwNTkxOSwyMTIyMjA5MzIyLC0xNDk2OTg0NzM1LDIxMzY3
Mzg1NV19
-->