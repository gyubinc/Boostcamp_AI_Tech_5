# 3) BERT 언어모델 소개
---

## 발전

Seq2Seq -> Attention + Seq2Seq -> Transformer

## 모델 소개

**Autoencoder**

Encoder는 이미지를 Compressend Data로 표현한 후 Decoder가 복구

**BERT**

MASKING을 통해 그러한 과정을 본인 스스로가 나오도록 학습

**GPT-1**

Transformer Decoder만 사용

**GPT-2**

원본 이미지를 특정한 Sequence를 가지고 자른 후 모델은 그 뒤를 예측하는 형태

## BERT-base 모델 구조도

Input Layer : [CLS] Sentence 1 [SEP] Sentence 2

Layer : 12개의 All-to-all layer

**학습 코퍼스 데이터**

BooksCorpus(800M words)

English Wikipedia(2,500M words)

30,000 token vocabulary

**tokenizing**

WordPiece tokenizing

<br/>

**NLP 실험**

GLUE datasets(MNLI, QQP, QNLI, SST-2, CoLA, STS-B, MRPC, RTE, WNLI)

SQuAD v1.1

CoNLL 2003

SWAG

* 단일 문장 분류, 두 문장 관계 분류, 문장 토큰 분류, 기계 독해 정답 분류

<br/>

## BERT 모델의 응용

**단일 문장 분류**

1. 감성 분석

2. 관계 추출

**두 문장 관계 분류**

1. 의미 비교

**문장 토큰 분류**

1. 개체명 분석

**기계 독해 정답 분류**

1. 기계 독해

## 한국어 BERT 모델

**Etri-KoBERT**

기존의 WordPiece 방식이 아닌 형태소를 선 분리 후 WordPiece를 적용해 한국어 성능향상(Morpheme-aware Subword Tokenization)

**Advanced BERT model**

Entity tag를 통해 성능 향상


