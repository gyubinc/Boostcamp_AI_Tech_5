# 1) Intro to Natural Language Processing
---

**NLP major conference**

ACL, EMNLP, NAACL

## NLP Task

**Low level**

* Tokenization, stemming

**Word and phrase level**

* Named entity recognition(NER), part-of-speech(POS)tagging, noun-phrase chunking, dependency parsing, coreference resolution

**Sentence level**

* Sentiment analysis, machine translation

**Multi-sentence and paragraph level**

* Entailment prediction, question answering, dialog systems, summarization

**Text mining major conference**

KDD, The WebConf(formerly, WWW), WSDM, CIKM, ICWSM

## Text mining 

* Extract useful information and insights from text and document data

* Document clustering

* Highly related to computational socical science

**Information retrieval major conference**

SIGIR, WSDM, CIKM, RecSys

* Highly related to computational social science

**Trends of NLP**

기존 RNN -> self-attention 기반 모델

현재는 특정 task에 관계없이 transformer를 self-supervised training해 학습

## Bag-of-Words

**Step1**

Constructing the vocabulary containing unique words

**Step2**

Encoding unique words to one-hot vectors

* For any pair of words, the distance is root 2

* For any pair of words, cosine similarity is 0

* A sentence / document can be represented as the sum of one-hot vectors

**NaiveBayes Classifier**

문서 D를 C개의 클래스로 분류할 때

argmax(C)P(C|D) = argmax(C)P(D|C)P(C)로 변경

* P(D)는 상수이니 argmax에서 무시

* 특정 단어의 등장횟수가 0일 경우 확률값이 0이 되어버리므로 regularization 필요

<br/>

# 2) Word Embedding
---

Express a word as a vector

**Word2Vec**

1. 분리된 단어들을 사전의 dimension 만큼의 one-hot vector로 변경

2. sliding window 기법 (한 단어를 중심으로 앞 뒤로 나타난 단어, 입출력 쌍 구성)

* "I study math", window = 1일 경우 (I, study), (study, I), (study, math)...

3. 2 layer neural net 생성 (hidden layer의 차원은 hyper parameter)

* one-hot vector는 1의 값을 가지는 row와 column 끼리만의 연산이 이루어짐

* one-hot vector와 선형변환 matrix의 곱은 embedding layer라고 부르고 행렬곱을 수행하지 않고 해당 index에서 뽑아오는 방식으로 계산 수행

4. hidden layer를 거치고 softmax 사용

* ground truth에 해당하는 확률값과 유사하면 완성

5. 일반적으로 Input vector 가중치 W1을 최종 벡터로 사용

**Property of Word2Vec**

단어간 관계는 벡터 상의 연산으로 표현

Word Intrusion

* 여러 단어들이 주어졌을 때 가장 상이한 단어를 찾아주는 task

**Application of Word2Vec**

1. Word similarity

2. Machine translation

3. Part-of-speech(PoS) tagging

4. Named entity recognition(NER)

5. Sentiment analysis

6. Clustering

7. Semantic lexicon building

**GloVe: Global Vectors for Word Representation**

window 내 등장빈도를 사전에 계산

* Fast training

* small corpus에서도 잘 작동
