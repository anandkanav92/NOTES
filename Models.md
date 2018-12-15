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
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODkzMzg1OTA3LC0xMTgzNTM4Nzg1LC0yMD
M2MzQyNTExLDE5NDAxOTkwNjIsMTAxMjA2NTI3MiwtMTM2MjYw
NTkxOSwyMTIyMjA5MzIyLC0xNDk2OTg0NzM1LDIxMzY3Mzg1NV
19
-->