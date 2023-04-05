# 6) Beam Search and BLEU score
---

## Beam Search

**Greedy decoding**

매 time step마다 하나의 단어를 사용해서 decoding하는 방식

* 이미 잘못 output을 배출했을 때 돌아갈 수 없는 문제 발생

**Exhaustive search**

P(y|x) = P(y1|x)P(y2|y1,x)...라고 하면 P(y|x)을 최대화하기 위해 Greedy는 매 step마다 최대를 따지지만
Exhaustive search는 전체적인 joint probability를 최대화

* 계산 복잡도가 너무 높음

**Beam search**

**절충안**

매 time step마다 하나의 k 개의 candidate 만을 고려하여 partial translation(hypothesis라고 부름)

* 일반적으로 k = 5~10

매 time step마다 score = logP_LM(y1, y...,yt|x)를 최대화

Beam search는 global optimal 보장하지 않으나 효율적임

Beach search decoding 에서는 서로 다른 hypothesis가 END token을 내는 시점이 다를 수 있음

END token이 완성된 hypothesis는 complete 되었다고 말하며 이를 옆에 두고 다른 가설들도 beam search 마저 진행

Beam search는 timestep T를 사전에 설정해 해당 step에서 멈추거나, n개의 hypothesis가 생기면 중지

**Finishing up**

completed hypotheses를 모두 보며 highest score를 가진 hypothesis 선택

* 단점: log 확률이 더해지는 형태이므로 문장의 길이가 길수록 score가 작아진다, 따라서 전체 단어의 길이로 score를 나눠 normalize 해준다.

## BLEU score

**기존의 단점**

'I love you'라는 문장을 'Oh I love you'라고 inference했다고 하면 해당 문장은 큰 차이가 없으나 모든 time step의 단어가 틀렸다는 결과가 나온다

* 생성된 문장을 각 단어가 아닌 ground truth 문장 전체와 비교해야할 필요가 있음

## Example

Reference: Half of my heart is in Havana ooh na na

Predicted: Half as my heart is in Obama ooh na

**precision(정밀도)**

precision = correct words / length of prediction = 7/8 = 78%

**recall(재현율)**

recall = correct words / length of reference = 7/10 = 70%

**F-measure**

precision과 recall의 조화평균(산술, 기하평균보다 상대적으로 작은 값에 치중)

F-measure = (precision x recall) / (1/2(precision + recall)) = 73.78%

* 이러한 성능 체크 방식들은 순서를 반영하지 않기 때문에 문법적으로 완전히 잘못된 문장도 100%가 나올 수 있음

**BLUE score**

BiLingual Evaluation Understudy

<br/>

N-gram overlap을 통해 score 계산, recall을 무시하고 precision만을 계산(실제 받아들일 떄의 체감은 precision에 해당한다)

* N-gram 개수만큼의 precision 값의 기하평균 계산

* recall의 최대값인 min(1, prediction길이/reference길이)을 곱해 recall을 아예 무시하진 않음

* 1-gram, 2-gram...를 곱하고 개수만큼 중근씌운 후 Brevity penalty(min값)을 곱해 계산

<br/>

## 7) Transformer 1
---
Attention is all you need

* No more RNN or CNN modules

**RNN의 단점**

attention의 기본 구조를 사용하더라도 RNN을 사용하면 Long term dependency 해결이 불가하다

## Bi-Directional RNNs

Forward RNN, Backward RNN을 사용해서 RNN의 진행을 양방향으로 설정

각각의 RNN의 특정 input에 해당하는 hidden vector는 두 방향 각각에서 만들어진 hidden state vector를 concat한 형태

## self-attention module

기존의 attention의 경우 encoder의 hidden state vector와 Decoder의 hidden state vector의 내적을 통해 score를 계산하고자 했으나 self-attention의 경우 encoder, decoder가 나뉘지 않고 스스로에게 내적함

## Query, Key, Value

Query의 경우 내적을 통해 유사도를 구할 때 중심이 되는 vector
 
Key의 경우 곱해지는 vector에 해당한다.

특정 step의 단어에 대한 Query와 전체 Key의 곱을 Softmax를 통과시키고 그 값을 Value vector에 곱함

기본적으로 자기 자신을 내적할 경우 값이 너무 커질 수 있으므로 key와 query를 분리한다고 보면 됨

그렇게 해서 Value 들의 가중평균하면 그것이 encoding vector

* 결과적으로 한번에 matrix의 형태로 값을 집어넣기 때문에 각각 step을 진행하는 것이 아니고 matrix 끼리의 곱으로 Q, K, V 표현 가능

self attention module을 통과하면 time step의 gap이 없음

* Long-Term Dependency 해결

## Scaled Dot-Product Attention

Inputs: a query q and a set of key-value (k, v) pairs to an outputㅣ

Query, key, value and output is all vectors

Output is qeighted sum of values

Weight of each value is computed by an inner product of query and corresponding key

Query, key는 계산을 위해 차원의 크기가 같아야 함, value의 dimension은 상관 없음

**장점**

Query의 경우 한번에 1개의 query만 계산하는 것이 아니라 각각의 query를 row로 연결한 Query matrix을 이용해 한번에 Key matrix와 곱한 후 Row-wise softmax를 취하고 이를 Value matrix에 곱하면 한번에 계산할 수 있음

* softmax를 거치면 column이 아닌 각각의 row의 합이 1임

**root(dk)로 나누는 이유**

내적 값은 scalar지만 실제적으로 query와 key vector의 차원의 크기에 따라 벡터가 d 차원이라면 d개 만큼의 항이 발생한다. 각 항이 독립이고 평균이 0이고 분산이 1이라고 가정했을 때 전체 분산은 d가 된다. 따라서 분산을 1로 유지하기 위해 정규화를 진행하는 것임

