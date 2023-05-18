# 9) Generative Models 1
---

## Introduction

**Generation**

if we sample x ~ p(x), x should look like a dog

**Density estimation**

p(x) shuld be high if x looks like a dog, and low otherwise(explicit models)

**Basic Discrete Distributions**

1. Bernoulli distribution: (biased) coin flip

2. Categorical distribution: (biased) m-sided dice

**number of parameters**

(r,g,b) ~ p(R,G,B)

* Number of cases: 256 x 256 x 256

* Number of parameters: 256 x 256 x 256 - 1

## Independence

28 x 28 binary mnist dataset

* Number of cases: 2 x 2 x ... x 2 = 2^n

* Number of parameters: 2^n -1

**structure Through Independence**

if X1, ... ,Xn are independent, P(X1, ..., Xn) = P(X1)P(X2)...P(Xn)

* Number of cases: 2^n

* Number of parameters: n

* 2^n entries can be described by just n numbers

<br/>

**Conditional Independence**

1. Chain rule p(x1, ...xn) = p(x1)p(x2|x1)p(x3|x1,x2)...

* Parameters: 1 + 2 + ... 2^(n-1) = 2^n -1

2. Bayes' rule p(x|y) = p(x,y)/p(y) = p(y|x)p(x)/p(y)

3. Conditional independence z라는 random variable이 주어졌을 때 x,y가 independent하다면 p(x|y,z) = p(x|z)

* parameters: 2n -1

* By leveraging Markov assumption, exponential reduction on the number of parameters

* AR model은 conditional independency 사용

## Autoregressive Models

직전 data에만 영향을 받아 순차적으로 정의되는 모델

* ordering(한 줄로 피는 과정) 필요

**NADE**

Neural Autoregressive Density Estimator

* explicit model that can compute the density of the given inputs

* 각각의 conditional distribution의 곱으로 표현해서 joint distribution 계산

* continuous distribution은 Mixture of Gaussian distribution 사용

## Summary of Autoregressive Models

1. Easy to sampling

2. Easy to compute probability

3. Easy to be extended to continuous

# 10) Generative Models 2
---

## Maximul likelihood learning

Given a training set of examples, best-approximating density model from model family를 찾는 과정

**how to evaluate the goodness**

**KL-divergence**

근사적으로 두 확률분포 상 거리를 표현

* symmetric property(A,B 사이의거리와 B,A사이의 거리가 동일) 불만족

* KL-divergence 최소화 = expected log-likelihood 최대화

empirical log-likelihood를 통해 접근

* Moncte carlo estimate의 분산이 높아지는 단점

**Empirical Risk Minimization(ERM)**

overfitting의 문제

* hypothesis space를 줄여서 generalization 향상

* underfitting 문제에 취약

**그 외 평가지표**

* KL-divergence - Variational Autoencoder(VAE)

* Jensen-Shannon divergence - Generative Adversarial Network(GAN)

* Wasserstein distance - Wasserstein Autoencoder(WAE) or Adversarial Autoencoder(AAE)

## Latent Variable Models

autoencoder는 generative model이 아니다!

**Variational Autoencoder**

Variational Inference(VI)

* goal of VI: optimize the variational distribution that best matches the posterior distribution

* 특히, true posterior 사이의 KL-divergence를 최소화하는 variational distribution 찾기

likelihood = ELBO(계산가능) + Variational Gap(계산불가)

ELBO를 늘리면 Variational Gap을 줄일 수 있다

ELBO is tractable quantity이므로 Maximum likelihood가 증가하며 같이 증가시키려고함

**ELBO(Evidence Lower Bound**)

=reconstruction Term - Prior Fitting Term

* intractable model(hard to evaluate likelihood)

* prior fitting term이 미분가능해야하므로, hard to use diverse latent prior distributions

* colsed-form for the prior fitting term이 있는 isotropic Gaussian 을 이용한다

Reconstruction Term

* minimizes the reconstruction loss of an auto-encoder

Prior Fitting Term

* enforces the latent distribution to be similar to the prior distribution

## Generative Adversarial Networks(GAN)

two player minimax game between generator and discriminator

## Diffusion Models

noise로부터 image를 만드는 것

* progressively generate images from noise

**Forward(diffusion) process**

progressively injects noise to an image

**Reverse process**

denoise the perturbed image back to a clean image