# 3) Basics of Recurrent Neural Network
---

**Basic structure**

**How to calculate the hidden state of RNNs**

* sequnece of vectors에 recurrence formula를 every time step마다 적용

* ht_1: old hidden-state vector

* xt: input vector at some time step

* ht: new hidden-state vector

* fw: RNN function with parameters W

* yt: output vector at time step t

* 가중치는 모든 time step에서 동일하다

**ht = fw(ht-1, xt)**

$$h_t = tanh(W_{hh}h_{t-1} + W_{xh}x_t$$

$$y_t = W{hy}h_t$$

x_t = 3차원, ht-1 = 2차원이라고 가정했을 때, input은 그 둘을 이어 붙인 5x1 차원이 되고 가중치 w는 2x5차원으로 만들어지며 그 결과값 ht는 2차원이 된다.

결과적으로 W는 2x3 차원의 Wxh, 2x2 차원의 Whh를 이어붙인 형태

## Types of RNNs

1. one-to-one

Standard Neural Networks

2. ont-to-many

Image Captioning

3. many-to-one

Sentiment Classification(Sequence of text를 입력)

4. many-to-many

Machine Translation, Video classification on frame level

## Character-level Language Model

Example: 'hello'

Vocabulary: [h,e,l,o]

* h = [1,0,0,0], e = [0,1,0,0] ...

sample training sequence: 'hello'

Input = h, e, l, l

prediction = e, l, l, o

## Backpropagation through time(BPTT)

전 과정의 loss를 한번에 처리하면 GPU resource가 부족할 수 있으므로 truncation을 통해 나눠 제한된 sequence 만큼씩 backpropagation하며 학습 진행

## Vanishing/Exploding Gradient Problem in RNN

매 step마다 matrix를 계속 곱하면 gradient vanishing or exploding 발생

* 가중치 같은 경우 똑같은 matrix가 계속해서 곱해짐
