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
- 
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk0MDE5OTA2MiwxMDEyMDY1MjcyLC0xMz
YyNjA1OTE5LDIxMjIyMDkzMjIsLTE0OTY5ODQ3MzUsMjEzNjcz
ODU1XX0=
-->