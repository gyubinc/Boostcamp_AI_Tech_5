# 8) Transformer 2
---

## Multi-Head Attention

self-attention을 조금 더 유연하게 확장

동일한 V, K, Q 벡터에 대해 병렬적으로 선형변환 후 여러 attention을 적용

여러개의 encoding vector가 만들어지면 해당 vector를 concat하여 사용

* 서로 다른 정보들을 병렬적으로 저장

그렇게 concat한 vector의 차원은 value vector의 차원 x head의 개수로 만들어짐

concat 후 linear operation을 적용해 원하는 dimension으로 만들어 최종 output 생성

**계산복잡도**

n: sequence length

d: dimension of representation

k: kernel size of convolutions

r: size of the neighborhood in restricted self-attention

|Layer Type|Complexity per Layer|Sequential Operations|Maximum Path Length|
|:---:|:---:|:---:|:---:|
|Self-Attention|O(n^2*d)|O(1)|O(1)|
|Recurrent|O(n*d^2)|O(n)|O(n)|
|Convolutional|O(k*n*d^2)|O(1)|O(logk(n))|
|Self-Attention(restricted)|O(r*n*d)|O(1)|O(n/r)|

GPU를 병렬적으로 사용할 수만 있다면 Q,K가 n x d dimension일 때 QKt의 계산 복잡도 O(n^2 x d)는 O(1)으로 가능하지만

RNN의 경우 time step마다 재귀적으로 계속 계산해야 하므로 O(n)이 그대로 필요하다

그러나 d는 hyper parameter지만 n은 지정할 수 없는 sequential length이므로 메모리 용량 관점에서 self-attention은 메모리를 더 많이 요구함

## Transformer: Block-Based Model

transformer는 Multi-Head Attention을 핵심 모듈로 하여 이와 덧붙여 후처리를 진행해 하나의 모듈 구성

multi-head attention을 통과한 후 residual connection add & layer normalization을 진행하고 이후 Feed forward 통과(fully connected layer), 다시 residual connection인 add & layer normalization 수행

**Add(residual connection)**

깊은 layer의 NN을 만들 때 gradient vanishing 문제 해결 및 학습 안정화 방식

'I study math' 라는 문장을 Multi-head attention에 입력할 때,

만약 'I'가 [1,-4]이고 attention vector가 [2,3]이라면 residual connection은 둘을 더해 [3,-1]로 변환

최종 만들고자하는 vector와 입력 벡터간의 차이가 attention vector가 되도록 학습

encoding vector와 output vector의 차원이 일치해야 add 가능

* 그렇기 때문에 multi head attention의 마지막 단계에서 concat 후 선형변환해서 차원을 맞춰주는거임

**Layer Normalization**

다수의 sample 들을 평균 0, 분산 1로 만들어주는 기법

* normalization 기법: Batch Norm, Layer Norm, Instance Norm, Group Norm...

그렇게 설정 후 affine transformation(ax+b)에 넣어 원하는 값의 분포인 평균 b, 분산 a^2의 노드를 가지도록 변경

이와 같은 과정을 거쳐 원하는 평균, 분산을 가질 수 있음

* 학습 안정화, 성능 향상

**블럭**

그렇게 이루어진 (Multi-head attention)-(Add & Normalization)-(Feed Forward)-(Add&Normalization)이 하나의 블럭이 됨

**이전까지의 문제**

한 block을 지나면 결과적으로 한 단어 - Attention vector 끼리 연결되다보니 position이 고려되지 않음

**Positional Encoding**

특정 순서에 따라 해당 자리에 특정 상수값이 들어간 vector값을 입력벡터에 더해주는 형태의 encoding

sinusoidal function을 통해 positional encoding

**Warm-up Learning Rate Scheduler**

learning rate = $d_{model}^{-0.5} * min(num_step^{-0.5}, num_step*warmupsteps^{-1.5})$

## Encoder 과정 정리

Input: 입력 단어들

1. 단어들을 각각 Embedding vector로 encoding

2. 해당 벡터들에 Position vector 더하기

3. Multi-Head Attention

4. Add & Norm

5. Feed Forward

6. Add & Normalization

7. 해당 블럭을 N개 병렬적으로 쌓아서 블럭에 입력

Output: 각각의 단어들에 해당하는 Encoding vector

## Decoder

Input: <시작토큰>, 입력 단어들

1. 우선 Encoder 과정에서의 1번~4번까지 수행

2. 그렇게 만들어진 vector를 다시 Multi-head attention의 Query로 입력

3. 해당 attention에 Value와 Key는 Encodoer를 지나간 vector

4. 그 후는 다시 4번~6번 반복(add 과정에서는 2번에 입력한 Query를 Add 과정에서 사용)

5. Linear layer

6. softmax

7. probabilities

8. Ground truth와 loss를 구해 역전파

## Masked self-attention

학습 당시에 batch processing을 위해서 정답 input을 모두 입력하긴 하지만 실제 학습에는 뒤의 input을 사용하면 안됨

* 이 때 input부터 넣지 않는 것이 아니라 넣어서 key, query를 우선 구한 후 뒷 부분의 query를 지워버리는 형태로 학습함

* 그 때 normalizing 과정에서는 지워지지 않은 값들끼리 normalizing되므로 첫번째 토큰의 query 값은 1이 됨


