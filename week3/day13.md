# 7) Recurrent Neural Networks
---

## Sequential Model

Naive sequence model

* 입력 dimension을 미리 알 수 없음

Autoregressive model

* Fix the past timespan

Markov model

* first-order autoregressive model

* joint distribution 용이

Latent Autoregressive model

* Hidden state 설정(summary of the past)

**Recurrent Neural Network**

short-term dependencies

* Vanishing / exploding gradient

## Long Short Term Memory

**Forget gate**

Decide which information to throw away

* sigmoid에 Input과 Hiddenstate를 통과

**Input gate**

Decide which information to store in the cell state

* 정규화를 거쳐 tanh, sigmoid를 지나고 곱해져서 Update함

**Output gate**

Make output using the updated cell state

* Cell state를 한번 더 조작해서 내보냄

## Gated Recurrent Unit

Simpler architecture (reset gate and update gate)

* Hidden state가 바로 Output으로 연결

# 8) Transformer
---

**Hard problem in sequential modeling**

Original space = [1,2,3,4,5,6,7]

* Trimmed sequence = [1,2,3,4,5]

* Omitted sequence = [1,2,4,7]

* Permuted sequence = [2,3,4,5,6,7]

## Transformer

the first sequence transduction model based entirely on attention

**Encoder**

n 개의 단어를 입력, Self-Attention 거치고 Feed Forward Neural Network 거침(하나의 Encoder)

* The Self-Attention in both encoder and decoder is the cornerstone of Transformer

**Encoder 학습과정**

Calculating Q, K, and V from X in a matrix form

1. represent each word with some embedding vectors(2번 과정으로)

2. Then, Transformer encodes each word to feature vectores with Self-Attention(각각의 vertor들은 서로 dependent)

3. Self attention은 한 단어당 Query, Key, Value의 3개 vector 생성

4. Suppose we are encoding the first word: "Thinking" given 'thinking' and 'machines'

5. score vector 생성(i번째 단어의 Query vector와 자신은 포함한 다른 모든 단어들의 Key vector를 내적, 즉 모두 곱해서 더한다)

6. Then, we compute the attention weights by scaling followed by softmax(key vector dimension의 root 값으로 나눔, 하이퍼 파라미터)

7. 그렇게 softmax를 취하면 특정 단어와 다른 각 단어와의 연관성이 비율로 나온다(dependency, attention rate)

8. The final encoding is done by the weighted sum of the value vectors(해당 값을 value에 곱해서 sum구한다)

* query vector와 key vector는 dimension이 일치해야 하지만 value vector는 상관 없다

9. 그렇게 encoding된 vector를 배출(z vector, value vector의 dimension과 동일)

**Matrix 관점**

X = 입력 데이터

Query vector: Q = X * Wq

Key vector: K = X * Wk

Value vector: V = X * Wv

Output Z vector: Z = softmax(Q x Kt / root(dimension of K)) x V

**MHA(Multi-headed attention)**

하나의 vector에 대해 Q, K, V 를 여러개 생성

* encoding vector z가 여러개 생성, 그걸 다시 가중치를 곱해 차원을 다시 맞춰줌

* 실제 구현에서는 기본 벡터를 쪼개서 차원을 미리 맞춰줌

**positional encoding**

위의 과정은 order에 independent 하기 때문에 입력에 position이 반영된 pre defined된 bias를 더해줌

**Decoder**

Transformer transfers K and V of the topmost encoder to the decoder

* 가장 상위 encoder의 Key와 Value를 Decoder에 넣어서 학습

In the decoder, the self-attention layer is only allowed to attend to earlier positions in the output sequence which is done by masking future positions before the softmax step

* 뒷 단어들을 미리 가려놓고 열어가면서 학습

**Vision Transformer**

Encoder를 활용해 이미지 학습에도 활용

**DALL-E**

문장이 주어지면 문장에 대한 이미지를 생성

* transformer의 decoder만 활용
