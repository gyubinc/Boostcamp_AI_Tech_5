# 10) Other Self-supervised Pre-training Models
---

## GPT-2

Just a really big transformer LM(다음 단어 예측)

40GB of text to train

* dataset의 quality가 높은 데이터

* reddit에서 karma가 높은 글 가져옴

can perform down-stream tasks in a zero-shot setting

* 모든 문장은 Q & A의 형태로 표현가능

* 감성 분석은 이 문장에 대해 긍/부정은 어떤가요? 같은 질문으로 변환해서 그 대답을 예측하는 형태임

**전처리**

Byte pair encoding(BPE)

**Modification**

* Layer normalization의 단계가 아래나 위로 수정

* layer가 위로 갈수록 initialize되는 parameter 값을 index에 반비례하여 작게 설정

**Question Answering**

Use CoQA(Conversation question answering dataset)

* 55 F1 score를 추가 데이터 없이 달성

* Fine-tuned BERT 89 F1 performance

**Summarization**

TL:DR 이라는 단어를 줌(Too long, didn't read)

그러면 요약이 가능해짐

**Translation**

문장을 쓰고 맨 뒤에 in French와 같이 붙여주면 번역 가능

<br/>

## GPT-3

Language Models are Few-shot Learners

비교할 수 없을 정도록 더 많은 파라미터 설정

96 attention layers, Batch size of 3.2M

* Prompt: the prefix given to te model

* Zero-shot: Predict the answer given only a natural language description of the task

* One-shot: See a single example of the task in addition to the task description

* Few-shot: See a few examples of the task

Zero-shot performance improves steadily with model size

Few-shot performance increases more rapidly

<br/>

## ALBERT

A Lite BERT for Self-supervised Learning of Language Representations

**Obstacles**

* Memory Limitation

* Training Speed

**Solutions**

1. Factorized Embedding Parameterization

Embedding layer의 dimension을 줄이는 기법

Hidden-state dimension이 4차원이라면 word embedding dimension을 4차원으로 바로 맞추는 것이 아니라 word embedding dimension을 적게 설정하고 선형변환을 통해 차원을 맞춰 준다

V: Vocabulary size

H: Hidden-state dimension

E: Word embedding dimension

BERT: V x H

ALBERT: (V x E) * (E x H)

<br/>

2. Cross-layer Parameter Sharing

**BERT 모델에서 학습하는 파라미터의 크기**

embedding vector를 Q, K, V로 변화시켜주는 가중치 matrix Wq, Wk, Wv가 layer의 개수만큼 존재, 마지막으로 각각 layer별로 만들어지는 Z matrix를 concat한 벡터를 z matrix 하나의 크기로 줄여주는 가중치 matrix Wo 존재 이러한 과정이 self-attention block의 개수만큼 존재

**ALBERT의 실험**

서로다른 self-attention block에 존재하는 선형변환 matrix 들을 share 하려고 시도

Shared-FFN: Only sharing feed-forward network parameters across layers(마지막 Wo)

Shared-attention: Only sharing attention parameters across layers(Wk, Wq, Wv)

All-shared: Both of them

<br/>

3. Sentence Order Prediction

Next Sentence Prediction pretraining task in BERT is too easy (BERT의 2가지 학습방법 중 masked LM만 학습하자)

Predict the ordering of two consecutive segments of text(두 문장의 순서를 맞추기로 학습해보자 Positive/Negative)

SP(Sentence Prediction)에 따라 나누었을 때

None / NSP(No Sentence Prediction) / SOP(Sentence Order Prediction)

SOP가 가장 좋은 성능을 보여주었다

**GLUE Results**

BERT / RoBERTa에 비해 ALBERT가 좋은 성능을 보여줌

<br/>

## ELECTRA

Efficiently Learning an Encoder that Classifies Token Replacements Accurately

Learn to distinguish real input tokens from plausible but synthetically generated replacements

* Pre-training text encoders as discriminators rather than generators

* Discriminator is the main networks for pre-training

* Generative Adversarial Network(GAN)에서 사용한 idea에서 사용한 자연어 처리의 pre-training 방식

* Generator가 아닌 Discriminator를 pre-train하는 방식

## Example

'the chef cooked the meal' 이라는 문장을

'MASK chef MASK the meal' 로 변경 후 

Generator(BERT와 같이 typically a small MLM)을 통과 시켜 복원한

'the chef ate the meal' 을 다시 Discriminator(ELECTRA)를 통과 시켜

'ate'가 replaced word라는 것을 맞춰내는 학습 방식

이 떄 pre-trained model은 Generator인 Bert 등이 아닌 Discriminator인 ELECTRA임

**성능**

Replaced token detection pre-training vs masked language model pre-training

Outperforms MLM-based methods such as BERT given the same model size, data, and compute

**Light-weight Models**

고성량 GPU 없이, 휴대폰 등으로도 사용 가능한 모델

**DistillBERT**

teacher / student model을 통해 학습

triple loss(distillation loss) over the soft target probabilities

**TinyBERT**

teacher / student model을 통해 학습

DistillBERT와는 다르게 attention matrix, hidden state vector 까지도 유사하게 학습(DistillBERT는 결과물만 맞춰보며 학습)

거대한 teacher 모델과는 차원이 다르기 때문에 fully connected layer 하나를 두어 teacher에서의 matrix를 넘겨서 모방함

## 최신 연구 흐름

Fusing Knowledge graph into Language Model

## example

두 가지 질문 '꽃을 심기 위해 땅을 팠다' 와 '집을 짓기 위해 땅을 팠다' 라는 문장을 각각 입력받았을 때 '어떤 도구로 땅을 팠을까' 라고 Question을 보내면 각각의 상황에 맞게 다른 대답을 내놓을 수 있는가(상식 또는 외부 지식을 Knowledge Graph라고 함)

**ERNIE**

Enhanced Language Representation with Informative Entities

**KagNET**

Knowledge-Aware Graph Networks for Commonsense Reasoning