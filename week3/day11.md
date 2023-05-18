# 1) Historical Review
---

**good deep learner**

1. Implementation skills

2. Math Skills

3. Knowing a lot of recent Papers

**Introduction**

**Artificial Inteligence**

* Mimic human intelligence

**Machine Learning**

* Data-driven approach

**Deep Learning**

* Neural netowrks

## Key Components of Eep Learning

새로운 연구를 아래 4가지를 기준으로 본다

1. The **data** that the model can learn from

2. The **model** how to transform the data

3. The **loss** function that quantifies the badness of the model<br/>

4. The **algorithm** to adjust the parameters to minimize the loss

**Data**

Data depend on the type of the problem to solve

* Classification, Semantic Segmentation, Detection, Pose Estimation, Visual QnA...

**Model**

AlexNet, GoogleNet, ResNet, DenseNet, LSTM, Deep AutoEncoders, GAN...

**loss**

The loss function is a proxy of what we want to achieve

* Regression Task : MSE

* Classification Task : CE

* Probabilistic Task : MLE

**algorithm**

일반적으로 1차미분한 정보를 활용

**그 외**

Dropout, Early stopping, k-fold validation, weight decay, Batch normalization, MixUp, Ensemble, Bayesian Optimization

## Historical Review

2012 - AlexNet

2013 - DQN

2014 - Encoder / Decoder, Adam

2015 - GAN, ResNet

2017 - Transformer

2018 - Bert

2019 - Big Language Models(GPT-X)

2020 - Self-Supervise Learning

# 2) Neural Networks & Multi-Layer Perceptron
---

Neural networks are function approximators that stack affine transformations followed by nonlinear transformations

**Linear Neural Networks**

Data: *D* = ${(x_i, y_i)}^{N}_{i=1}$

Model: $\hat{y} = wx + b$

Loss: $loss = \frac{1}{N}\displaystyle\sum_{i=1}^{N}(y_i - \hat{y_i})^2$

1. Compute the partial derivatives w.r.t the optimization variables

2. iteratively update the optimization veriables<br/>적절한 step size를 잡는 것이 핵심

**Linear Neural Networks**

affine transform

y = $W^{T}x+b$

* 행렬은 두 개의 벡터 사이의 선형변환을 표현하는 방법으로 해석가능(x -> y)

## We need nonlinearity!

단순한 선형결합의 반복은 하나의 선형결합과 같다

* activation function의 필요성

**Activation functions**

* Relu 

* Sigmoid

* Hyperbolic Tangent

**Multi-Layer Perceptron**

2 layer 이상을 가진 다층 perceptron 구조

**Loss function**

* Regression Task : MSE

* Classification Task : CE

* Probabilistic Task : MLE

# 3) Optimization
---

## Gradient Descent

1차 편미분을 통해 local minimum을 탐색하는 알고리즘

## Important Concepts in Optimization

**Generalization**

How well the learned model will behave on unseen data.

* Generalization gap = |training error - test error|

**Underfitting vs Overfitting**

**Cross validation**

model validation technique for assessing how the model will generalize to an independent (test) data set.

**Bias and Variance Tradeoff**

* Variance : 출력이 얼마나 일관적인가

* Bias : 평균이 True target에서 얼마나 먼가

* minimizing cost는 bias^2, variance, noise의 부분으로 나뉜다

**Bootstrapping**

Any test or metric that uses random sampling with replacement

**Bagging vs. Boosting**

**Bagging(Bootstrapping aggregating)**

* Multiple models are being trained with bootstrapping

* ex. Base classifiers are fitted on random subset where individual predictions are aggregated

**Boosting**

* it focuses on those specific training samples that are hard to classify

* A strong model is built by combining weak learners in sequence where each learner learns from the mistakes of the previous weak learner.

## Practival Gradient Descent Methods

**Stochastic gradient descent**

Update with the gradient computed from a single sample

**Mini-batch gradient descent**

Update with the gradient computed from a subset of data

**Batch gradient descent**

Update with the gradient computed from the whole data

**Batch-size Matters**

* Batch size가 클 경우 Sharp minimum에 도달

* Btch size가 작을 경우 Flat minimum에 도달

**Gradient Descent Methods**

* Stochastic gradient descent

$W_{t+1} <-  W_{t} - \eta g_t$

$\eta = learning rate$

$g_t = Gradient$

* Momentum

이전 gradient 정보에 관성을 부여

$a_{t+1} <- \beta a_t + g_t$

$W_{t+1} <- W_{t} - \eta g_t$

$\beta = momentum$

$a_{t+1} = accumulation$

* Nesterov accelerated gradient

Lookahead gradient를 활용해 한번 이동 후 해당 점에서의 gradient를 반영해 이동

* Adagrad

gradient가 많이 변했는지 적게 변했는지에 대한 값 Sum of gradient squares(G)를 저장하여 반비례한 이동

G가 계속 커짐

* Adadelta

G에 특정 window size만을 반영

Exponential moving average를 통해 update

**There is learning rate in Adadelta**

* RMSprop

step size를 곱해준 기법

* Adam

leverages both past gradients and squared gradients

## Regularization

**Early stopping**

validation loss를 기반으로 early stopping

**Parameter norm penalty**

parameter의 제곱합을 줄여 function space의 smoothness 증가

**Data augmentation**

More data are always welcomed

* 주의: 6을 뒤집으면 label이 9로 바뀌니 불가능

**Noise robustness**

random noise를 inputs or weights에 추가

**Label smoothing**

Decision boundary를 흐리게 설정

CutMix, Mixup, Cutout...

**Dropout**

randomly set some neurons to zero

**Batch normalization**

parameters의 분포를 정규분포로 변환