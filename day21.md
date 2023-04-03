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

14분까지 들음 encoder에서 attention이 처음 적용되는 부분 다시 듣고 정리



## Encoder-decoder architecture

## Attention mechanism

