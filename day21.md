# 5) Seq2Seq
---

## Seq2Seq with attention

**Seq2Seq Model**

RNN 구조 중 many-to-many에 해당

입력 sequence of words를 모두 읽은 후 다음에 출력 sequence of words를 생성 및 예측

* encoder와 decoder로 구성

Encoder의 마지막 time step을 통과한 후 생성된 hidden state vector는 Decoder의 previous hidden vector로 작용하고 Decoder의 첫번째 input은 start of sentence <SOS> token으로 입력한다

* 종료는 end of sentence <EOS> token

## Attention

**Attention의 탄생이유**

'I go home'을 '나는 집에 간다' 라고 번역한다고 생각해보면 기존의 Seq2Seq 구조는 마지막 time step을 통과한 hidden state vector를 Decoder로 넘겨주므로 가장 먼저 생성해야 하는 '나는'과 이에 대응하는 'I'사이의 거리가 멀어져 시작조차 힘든 long term dependency 문제가 발생한다.

<br>

따라서 이러한 문제를 해결하기 위해 encoder에서 각각 time step을 지날 때마다 생성된 모든 hidden state vector를 활용해보자는 것이 목적

**방식**

Encoder 매 time step마다 발생하는 hidden state vector와 마지막 hidden state와 <SOS> token을 입력한 Decoder 사이의 내적인 Attention score를 각각 구하고 Softmax를 통과한 Attention vector을 이용해 Attention output 출력

입력 : Encoder state vector 전부와 Decoder state vector 하나

출력 : ENcoder state vector에 가중 평균된 벡터 하나

**예측**

그렇게 나온 Attention output과 Decoder RNN을 거친 vector 하나를 Concat한 후 Decoder의 특정 time step의 단어 예측

**다음 step**

마찬가지로 2번쨰 time step의 Decoder vector를 Encoder vector와 내적 후 softmax 계산해 가중치를 적용해서 Attention output과 Decoder의 context vector 주어져서 다음 단어 예측

**핵심**

attention score를 softmax 시킨 attention vector의 값이 결과적으로 각 입력 파트들 중 현재 time step에서 가장 중점적으로 봐야하는 vector가 무엇인지 알려주는 역할을 함

Decoder의 RNN은 Encoder의 hidden state와 내적하는 역할과 attention output과 concat하는 역할을 수행하는 벡터 2개를 각각 훈련, 역전파 해야함

**훈련**

전 단어를 잘못 예측했다고 하더라도 학습을 위해 원래 정답을 다음 time step의 입력으로 넣어줌(ground truth를 입력으로 넣어줌)

이것을 Teacher forcing이라고 함

**Inference**

전 단어를 그대로 다음 time step의 input으로 넣음

**단점**

teacher forcing은 학습 과정을 효율적으로 만들어주지만 inference 과정에서는 input을 다음 step에 넣으므로 실제 모델이 동잘하는 과정과는 상이하기 떄문에 이러한 문제를 해결하기 위해 적절히 섞는 학습법도 존재함

## Different Attention Mechanisms

**Attention score 유사도 계산 방식**

1. 기본 dot product

일반적인 내적

2. General product

간단한 내적의 형태로 존재하던 유사도를 구하는 방식을 사이에 두 벡터의 크기에 맞는 matrix를 넣어 두 벡터 간 모든 element를 고려해 연결해주는 내적을 general dot product라고 하며 이 matrix 내 모든 요소들은 학습 가능한 parameter로 설정할 수 있다.

3. concat product

기본 CNN 처럼 Encoder hidden vector와 Decoder hidden vector를 concat(단순 연결) 후 가중치 Matrix와 곱한 후 tanh를 통과시키고 다시 선형변환을 통해 계산

(선형변환은 최종적으로 scalar 값으로 만들어줘야 하므로 matrix가 아닌 vector를 곱해서 생성)

## Attention의 장점

1. Decoder의 매 time step마다 Encoder의 어떤 부분에 집중해야할지 학습할 수 있게 되면서 Seq2Seq에 적용되며 기계번역(NMT) 성능 증가

2. Information bottleneck problem(Encoder의 마지막 vector만 사용)해결

3. Decoder를 지나 Encoder로 가는 것이 아닌 Concat된 부분에 나뉘어 Attention output으로도 역전파를 진행하며 학습의 관점에서 Gradient vanishing 문제 해결

4. attention distribution을 분석하며 어떠한 단어가 서로 연결되었는지 해석가능성 제공

* allignment를 스스로 학습