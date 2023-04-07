# 9) Self-supervised Pre-training Models
---

## Recent Trends

Transformer에서 제시한 self-attention block은 NLP 분야에서 우수한 성능을 내고 있음  

요즘은 그러한 block을 훨씬 더 많이 쌓은 후 대규모 학습 데이터로 self-supervised learning 후 transfer learning

* BERT, GPT-3, XLNet, ALBERT, RoBERTa, Reformer, T5, ELECTRA...

한계점

greedy decoding(한번에 1개씩 생성)에서 벗어나지 못함

## GPT-1

다양한 special token들을 사용

self-attention block 12개 사용

감성분석 - EOS 대신 Extract 토큰 사용하여 해당 문장이 긍정인지 부정인지 분류 가능

Entailment(논리적 내포관계 추론) - 다수의 문장을 받을 때 SOS - 문장 1 - Delimeter 토큰 - 문장 2 - Extract 토큰의 구조로 입력 해 관계 추론 가능

## transfer learning

마지막 layer를 없애고 새로운 학습을 위한 초기화된 추가적인 layer 하나를 덧붙임

이미 학습된 layer에는 learning rate를 매우 낮춰 거의 변경되지 않도록 하며 fine-tuning함

## BERT

Pre-training of Deep Bidirectional Transformers for Language Understanding

ELMo는 LSTM 기반이었음

**Motivation**

GPT-1 같은 경우 standard한 language model의 방식으로 pre-train 진행(한 단어 한 단어 다음 단어로 넘어가며 학습)

* 뒷 단어에 대한 정보가 없으므로 전체적인 문맥을 보기 어려움

**Masked Language Model(MLM)**

일정한 확률로 맞춰야하는 각 단어를 MASK로 치환

* 전체 단어 중 k = 15% 정도를 치환

* Too little masking: Too expensive to train

* Too much masking: Not enough to capture context

* 15% 중 80%는 MASK라는 토큰으로 치환, 10%는 random word로 치환, 10%는 원래 그대로 사용

**Next Sentence Prediction**

GPT-1이 extraction 토큰을 맨 뒤에 넣었다면 BERT는 CLS 토큰을 문장의 맨 앞에 넣어서 사용, 문장 간의 구분은 SEP 토큰으로 구분해서 문장 2가 문장 1 뒤에 나올 문제가 맞는지 확인하는 학습, masking도 위와 동일하게 사용해서 MASK 자리 예측, CLS 토큰은 binary classification(두 문장이 인접 / 비인접 체크)

* 인접 = IsNext, 비인접 = NotNext

## BERT Summary

1. Model Architecture

모델 구조 자체는 transformer에서 제안된 self-attention block을 그대로 사용

L = self-attention block

H = 각 self-attention block에서 유지하는 encoding vector의 차원 수

A = 각 layer별로 정의되는 attention head의 숫자

* BERT BASE: L = 12, H = 768, A = 12

* BERT LARGE: L = 24, H = 1024, A = 16

2. Inpute Representation

* WordPiece embeddings(30,000 WordPiece)

* Learned positional embedding

* CLS - Classification embedding

* SEP - Packed sentence embedding

* Segment Embedding

Segment Embedding은 문장이 SEP로 연결되다 보니 다른 문장끼리 연결된 positional embedding만 존재하니, 현재가 몇번째 문장인지에 대한 embedding vector도 더해줌

3. Pre-training Tasks

masking된 단어를 예측해내는 task, 두 인접 문장이 유사한지 분류하는 task 2개로 구성

* Masked LM

* Next Sentence Prediction

## GPT와의 차이점

GPT같은 경우 masked self-attention을 사용(뒤에 오는 단어를 미리 볼 수 없음), BERT같은 경우 입력에 mask를 넣고 실제는 transformer의 self-attention과 같음

## Fine-tuning Process

* sentence Pair(논리적 모순 관계): CLS 토큰에 대한 encoding vector를 통해 예측

* question answering

* tagging task: 각각의 CLS 토큰을 포함해 각각의 vector들을 동일한 공통의 output layer에 통과해 최종 prediction

## BERT vs GPT-1

**Training-data size**

GPT - 800M words

BERT - 2,500M words

**special token**

BERT - SEP, CLS, segment embedding token 존재

**Batch size**

GPT - 32,000 words

BERT - 128,000 words

**Task-specific fine-tuning**

GPT - learning rate가 fine-tuning에서도 동일

BERT - task-specific fine-tuning learning rate

**GLUE Benchmark**

여러 task에 대한 data set

## Machine Reading Comprehension(MRC), Question Answering

문장을 주고 해당 문장을 독해해서 특정한 질문에 대해 기계 독해기반으로 응답하는 task

Fully connected layer를 통과시켜 각 word별로 scalar 값을 구하고 답에 해당하는 word가 어떤 scalar 값부터 시작할 지 찾고 다른 Fully connected layer를 통과해서 word의 끝 scalar 값을 구하도록 해 정답을 내뱉음

**SQuAD data**

문단 - 질의응답으로 구성된 data

* ELECTRA, ALBERT, ROBERTA 등이 순위권

SQuAD 2.0부터는 No Answer도 예측하는 task가 생겨 처음 문단을 받았을 때 정답이 있을지 없을지부터 체크함

**On SWAG**

특정 문장 뒤에 여러 가능한 경우가 있을 때 여러 선택지들 중 이어질 문장 하나를 고르는 task

* 각각 뒤에 문장을 concat하여 BERT로 인코딩 후 fully connected layer를 통과시켜 output layer의 scalar값을 모두 구한 후 각기 얻은 scalar값을 softmax에 입력으로 주어 ground truth 확률을 학습

**Ablation Study**

layer를 깊게 쌓고 parameter를 늘리면 여러 down-stream task에 대한 성능등이 점점 좋아진다.

Improvements have not asymptoted