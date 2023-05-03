# 1) 인공지능과 자연어 처리
---

<br/>

## 1-1) 인공지능의 탄생과 자연어처리
---

**인공지능**

인간의 지능이 가지는 학습, 추리, 적응, 논증 따위의 기능을 갖춘 컴퓨터 시스템

<br/>

**콜로서스 컴퓨터**

프로그래밍이 가능한 세계 최초의 전자식 컴퓨터

* 1500개의 진공관으로 구성

<br/>

**이미테이션 게임**

튜링테스트, 기계에 지능이 있는지를 판별하고자 하는 실험

* 인간이 보기에 인간 같은 것을 인간에 준하는 지능으로 정의

<br/>

**AI 황금기(1956-1974)**

General purpose AI를 만들기 위해 자연어 연구가 폭발적으로 관심받음

* 최초의 심리 상담챗봇 ELIZA(1966)

<br/>

### 인간의 자연어 처리

대화의 단계

1. 화자는 자연어 형태로 객체를 인코딩

2. 메세지의 전송

3. 청자는 자연어를 객체로 디코딩

### 컴퓨터의 자연어 처리

대화의 단계

1. Encoder는 벡터 형태로 자연어를 인코딩

2. 메세지의 전송

3. Decoder는 벡터를 자연어로 디코딩

<br/>

### 다양한 자연어처리 application

의미 분석기, 구문 분석기, 감성 분석기, 형태소 분석기, 개체명 인식기...

* 대부분의 자연어처리는 '분류'의 문제

**특징 추출과 분류**

분류를 위해 데이터를 수학적으로 표현

* 특징(Feature)를 기준으로, 분류 대상을 그래프 위에 표현 가능

* 과거에는 사람이 직접 특징을 파악해서 분류

* '기계학습'의 핵심은 특징을 컴퓨터가 스스로 찾고 스스로 분류하도록 학습하는 것

### Word2Vec

가장 단순한 표현

one-hot encoding -> Sparse representation

단어 벡터가 sparse해서 단어가 가지는 '의미'를 벡터 공간에 표현 불가능

Word2Vec = 한 단어의 주변 단어들을 통해, 그 단어의 의미를 파악(Skip-gram)

* 벡터 공간에 나열된다는 것은 벡터 연산도 가능하다는 것

**장점**

* 단어간의 유사도 측정에 용이

* 단어간의 관계 파악에 용이

* 벡터 연산을 통한 추론이 가능(한국-서울+도쿄 = ?)

**단점**

단어의 subword information 무시

* Out of vocabulary(OOV)에서 적용 불가능

<br/>

### FastText

한국어는 다양한 용언 형태를 가짐

Word2Vec의 경우, 각각이 서로 다른 언어로 인식됨

* 알고리즘은 word2Vec과 유사하나, n-gram 방식으로 학습

* 2-gram = 'apple' = {ap, pp, pl, le}을 독립된 vocab으로 인식

* n-gram으로 단어를 분리한 후, 모든 n-gram vector를 합산한 후 평균을 통해 단어 벡터를 획득

* 오탈자, OOV, 등장 횟수가 적은 학습 단어에 대해서 강세

<br/>

### 단어 임베딩 방식의 한계점

Word2Vec, FastText모두 동형어, 다의어 등에 대해서 embedding 성능이 좋지 않음

* 문맥 고려 X

<br/>

## 1-2) 딥러닝 기반의 자연어처리와 언어모델
---

**모델**

일기예보 모델, 데이터 모델, 비즈니스 모델, 물리 모델, 분자 모델...

* 자연 법칙을 컴퓨터로 모사함으로써 시뮬레이션이 가능

* 이전 state를 기반으로 미래의 state 예측

* 모델 학습 = 미래의 state를 올바르게 예측하는 방식으로 학습

<br/>

**언어모델**

'자연어'의 법칙을 컴퓨터로 모사한 모델

* 주어진 단어들로부터 그 다음에 등장할 단어의 확률을 예측

* 문맥을 잘 계산해야 함

<br/>

**Markov 기반의 언어모델**

I 다음에 like가 나올 확률, don't가 나올 확률을 계산해 해당 확률을 최대로 하도록 네트워크를 학습

<br/>

**RNN 기반의 언어모델**

RNN은 히든 노드가 방향을 가진 엣지로 연결돼 순환구조를 이룸

* 이전 state 정보가 다음 state를 예측하는데 사용됨, 시계열 데이터 처리에 특화

* 마지막 출력은 앞선 단어들의 '문맥'을 고려해서 만들어진 최종 출력 vector -> Context vector

* Context vector 값에 classification layer를 붙이면 문장 분류를 위한 신경망 모델

* 일대다, 다대일, 다대다

<br/>

**Seq2Seq**

Encoder layer와 Decoder layer로 구성

Encoder layer: RNN 구조를 통해 Context vector를 획득

Decoder layer: 획득된 Context vector를 입력으로 출력을 예측

<br/>

**RNN 구조의 문제점**

입력 sequence의 길이가 매우 긴 경우, 처음에 나온 token에 대한 정보가 희석

고정된 context vector 사이즈로 인해 긴 sequence에 대한 정보를 함축하기 어려ㅑ움

모든 token이 영향을 미치니, 중요하지 않은 token도 영향을 줌

-> Attention의 탄생

<br/>

**Attention**

인간의 정보처리와 마찬가지로, 중요한 feature를 더욱 중요하게 고려하는 것이 모티브

문맥에 따라 동적으로 할당되는 encode의 Attention weight로 인한 dynamic context vector를 획득

* 기존 Seq2Seq의 encoder, decoder 성능을 비약적으로 향상시킴

* 하지만 여전히 RNN이 순차적으로 연산이 이뤄짐에 따라 연산속도가 느림

<br/>

**Self-Attention**

<br/>

**Transformer**

하나의 네트워크 내에 encoder와 decoder가 합쳐짐

<br/>

# 2) 자연어의 전처리
---

**전처리**

원시 데이터(raw data)를 기계 학습 모델이 학습하는데 적합하게 만드는 프로세스

학습에 사용될 데이터를 수집, 가공하는 모든 프로세스

* Task의 성능을 가장 확실하게 올릴 수 있는 방법

<br/>

**Python string 관련 함수**

대소문자의 변환
```
* upper

* lower

* capitalize

* title

* swapcase
```
편집, 치환
```
* strip

* rstrip

* lstrip

* replace(a,b)
```
분리, 결합
```
* split() #공백기준 분리

* split('\t') #탭 기준 분리

* ''.join(s) #list s에 대하여 공백을 두고 결합

* lines.splitlines #라인 단위로 분리
```
구성 문자열 판별
```
* isdigit

* isalpha

* isalnum

* islower

* isupper

* isspace

* startswith('hi')

* endswith('hi')
```
검색
```
* count('hi') #문자열 내 'hi' 출현 빈도

* find('hi') #문자열 내 'hi'가 처음 출현한 위치, 없으면 -1

* find('hi', 3) #문자열의 index 3번부터 hi 출현 위치 검색

* rfind('hi') #오른쪽부터 hi처음 출현한 위치 리턴

* index('hi') #find와 같지만 없을 경우 예외발생

* rindex('hi') #rfind와 같지만 없을 경우 예외발생
```

### 토큰화

주어진 데이터를 토큰이라 불리는 단위로 나누는 작업

### 문장 토큰화

문장 분리

### 한국어 토큰화

다양한 형태로 분리 가능

