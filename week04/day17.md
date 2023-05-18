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

4. Named entity recognition(NER)# Viz 3) Visualization Text
---

## 3-1) Text

Visual representation으로 줄 수 없는 설명

* 오해를 방지

* Text를 과하게 사용한다면 오히려 이해를 방해

## Anatomy of a Figure(Text ver.)

**Title**

가장 큰 주제를 설명

**Label**

축에 해당하는 데이터 정보를 제공

**Tick Label**

축에 눈금을 사용해 스케일 정보를 추가

**Legend**

한 그래프에서 2개 이상의 서로 다른 데이터를 분류하기 위한 보조 정보(범례)

**Annotatiokn(Text)**

그 외 시각화에 대한 설명 추가

## 3-2) Color

위치와 색은 가장 효과적인 채널 구분

* 위치는 시각화 방법에 따라 결정

* 색은 우리가 직접 고른다

* 가장 중요한 점은 화려함이 아닌 전달력

**색이 가지는 의미**

* 높은 온도는 빨강, 낮은 온도는 파랑

* 카카오는 노랑, 네이버는 초록

* 정당의 색

* 이미 사용하는 색에는 이유가 있다.

## COlor Palette의 종류

1. 범주형(Categorical)

Discrete, Qualitative 등의 이름

* 독립된 색상으로 구성되어 범주형 변수에 사용

* 최대 10개의 색상까지 사용

* 색의 차이로 구분하는 것이 특징

One color: 전체적인 분포를 보기에 유용

Categorical: 이산적인 개별 값에 적합

Diverge, Sequential: 같은 값에 대해서도 다른 가중치

2. 연속형(Sequential)

정렬된 값을 가지는 순서형, 연속형 변수에 사용

* 연속적인 색상을 사용하여 갚을 보현

* 어두운 배경에서 밝은 색, 밝은 배경에서 어두운 색이 큰 값을 표현

* 색상은 단일색조

* 균일한 색상변화가 중요

* ex) github commit log

3. 발산형(Diverge)

연속형과 유사하지만 중앙을 기준으로 발산

* 상반된 값, 서로 다른 2개를 표현하는 데 적합

* 양 끝으로 갈수록 색이 진해짐

* 중앙의 색은 양쪽 점에 편향되지 않음(꼭 무채색일 필요는 x)

* ex) 지지율 표현, 0도를 기준으로 온도표현

## 강조, 그리고 색상 대비

데이터에서 다름을 보이기 위해 Highlighting 가능

강조 방법 중, 색상 대비(Color Contrast) 사용

* 명도 대비: 밝은 색과 어두운 색을 배치하면 밝은 색은 더 밝게, 어두운 색은 더 어둡게 보임(회색검정)

* 색상 대비: 가까운 색은 차이가 더 크게 보임(파랑보라, 빨강보라)

* 채도 대비: 채도의 차이, 채도가 더 높아보임(회색 주황)

* 보색 대비: 정반대 색상을 사용하면 더 선명(빨강초록)

**색각 이상**

* 삼원색 중 특정 색을 감지 못하면 색맹

* 부분적 인지 이상이 있다면 색약

* 색 인지가 중요한 분야(과학/연구)에 있어서 고려 필수

## 3-3) Facet

화면 상에 View를 분할 및 추가해 다양한 관점 전달

* 같은 데이터셋을 서로 다른 인코딩을 통해 다른 인사이트

* 같은 방법으로 동시에 여러 feature보기

* 부분 집합을 세세하게 보여주기

## Figure와 Axes

Figure는 큰 틀, Ax는 각 플롯이 들어가는 공간

* Figure는 언제나 1개, 플롯은 N개

## N x M subplots

**가장 쉬운 방법**

1. plt.subplot()

2. plt.figure() + fig.add_subplot()

3. plot.subplots

**쉽게 조정할 수 있는 요소**

1. figuresize

2. dpi

3. sharex, sharey

4. squeeze

5. aspect

**Grid spec**

그리드 형태의 subplots

기존 subplots로 4 x 4로 만들 수 있음

여기서 다른 사이즈를 만든다면?

1. Slicing 사용

numpy로 만든다면

첫번쨰: axes[0, :3]

두번째: axes[1:, :3]

세번째: axes[3, :]

fig.add_grid_spec()

2. x, y, dx, dy를 사용

fig.subplot2gird()

**내부에 그리기**

Ax 내부에 서브플롯을 추가하는 방법

* 미니맵, 외부정부 등 표현

* ax.inset_axes()

그리드를 사용하지 않고 사이드에 추가

* 방향의 통계정보 제공

* 제목 등의 텍스트 추가 가능

* make_axes_locatable(ax)

5. Sentiment analysis

6. Clustering

7. Semantic lexicon building

**GloVe: Global Vectors for Word Representation**

window 내 등장빈도를 사전에 계산

* Fast training

* small corpus에서도 잘 작동
