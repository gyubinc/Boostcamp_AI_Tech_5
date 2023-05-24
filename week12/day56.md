# 4) 최신 국내 및 해외 NLP 데이터 소개
---

## 국내 NLP 데이터 

### 데이터 구축 주체에 따른 분류

국가 기관 주도

* 국립국어원, 우리말샘, NIA

기업 주도

* Naver, Kakao, Upstage, LG CNS 등

개인 및 학계 주도

<br/>

## 국가 기관 주도

**21세기 세종 계획**

1998~2007 약 2억 어절의 자료 구축, 공개

**KAIST Corpus**

1997~2005 Multilingual Corpus Dataset

**엑소브레인**

2013~2023, ETRI

일반분야 대상 - 전문분야 대상 - 심층질의응답

**모두의 말뭉치**

2016~ 누구나 개선 의견 제안 가능

**우리말샘**

2016~ Github를 통해 오픈 API도 함께 제공

**AI 허브**

2016~, NIA AI 통합 플랫폼

**뉴스 빅데이터**

2020, 한국언론진흥재단 뉴스 빅데이터 제공

**데이터 댐**

과기정통부 주도 - 디지털 뉴딜

**데이터 바우처사업**

과기정통부 주도 - 데이터 생태계 확대

<br/>

## 기업 주도

**KorQuAD 1.0 & 2.0**

2019, LG CNS

질문답변, 기계독해 데이터셋

**KLUE dataset**

2021~

Korean Language Understanding Evaluation

한국어 이해 능력 평가를 위한 벤치마크

**KorNLI**

2020, Kakao Brain

KorSTS

**KOBEST**

2022 한국어 이해능력 평가를 위한 벤치마크

<br/>

## 개인 및 학계 주도

**NSMC**

2016, Naver 영화에서 크롤링한 데이터 활용

**Korean Comment Corpus**

2020 온라인 뉴스 댓글 수집

**Korean Hate Speech - BEEP**

2020, 욕설데이터

**KorLex**

WordNet(워드넷) 동의어, 하의어를 그래프로 표현

시소러스 형식

**Korean WordNet**

**UWordMap**

Lexical semantics network

단어의 의미 분석, 중의성 해석

**USenseVector, UConceptVector, UTagger**

**한통이: 자연언어처리 기반 다국어 어휘대역 서비스**

**Korean CommonGen**

형태소 정보를 사용해 문장을 재구성

<br/>

## 해외 NLP benchmark

세 가지 분류

Natural Language Understanding(NLU)

* 형태소 분석, NER, QA, MRC

Natural Language Generation(NLG)

* DST, WMT, CNN/Daily, SamSum

NLU + NLG

* Persona, Blenderbot

### NLU

**자연어 추론(NLI)**

Stanford NLI

주어진 문장들의 관계를 구분

**개체명 인식(NER)**

CoNLL 2003

영어와 독일어로 구성되어 있는 NER dataset

**관계추출(Relation Extraction)**

TACRED

**기계번역(Machine Translation)**

WMT 데이터셋

**대화시스템(Dialogue System)**

Wizard-of-Oz

DSTC - Dialog System Technology Challenges

**문서요약(Text Summarization)**

CNN/Daily Mail

**기계독해(Machine Reading Comprehension)**

SQuAD, SQuAD 2.0

**GLUE Benchmark**

9개의 task

CoLA, SST-2, MRPC, STS-B, QQP, MNLI, QNLI, RTE, WNLI

**SuperGLUE Benchmark**

GLUE가 인간의 성능을 넘어서며 11개의 task로 구성

**Gem Benchmark**

영어 뿐 아니라 multilingual dataset도 포함

**MultiTask Benchmark**

**Big Benchmark**

200개 이상의 task를 수행하도록 하는 benchmark

Mig benchmark light 버전도 존재

<br/>

## Multilingual Benchmark

Timeline

LASER를 시작으로, META를 중점으로 발전

LASER, WMT, Flores ...

**LASER**

Language-Agnostic SEntence Representations

최초의 대량의 mluti-language 연구

50 language 제안 - 200개로 확장

**Flores**

**WikiMatrix**

학습데이터 85 languages

**M2M-100**

2200개의 언어쌍

**CCMatrix**

576개의 언어쌍

**Flores-101**

**NLLB 200**

No Language Left Behind

low resource language를 포함

정보 접근성 상승, 디지털 격차 해소를 꾀함

<br/>

## Summary

### 국내 NLP 데이터 구축

과거 국가기관 위주의 데이터 구축에서, 개인과 기업이 주도하여 만든 다양한 데이터들

### 해외 NLP benchmark

Natural Language Understanding & Natural Language Generation

### Multilingual NLP

점점 다양안 언어로, Low Resource Language들까지도 커버하는 NLP

<br/>

# 5) NLP 분야의 특이한 Task 및 Data 소개
---

## Hate Speech & Offensive Language 관련 Task 및 Data

### Hate speech

인종, 성적 지향, 종교, 출신 국가, 성별 등 인적 특성에 따라 비하, 공격하는 언어

**Hate speech detection**

혐오 발언 및 공격적 표현을 탐지, 분류

**HateXplain**

A Benchmark Dataset for Explainable Hate Speech Detection

annotation

* 3-class classification: hate/offensive/normal

* target community

* rationale: post의 레이블링을 결정하는 일부분

### Counter Speech Generation

Detecting을 넘어서 적극적인 방식으로 반박/대응

**ProsocialDialog**

비윤리적, 문제적, 편향적 상황을 다루는 대화에 대한 대응 데이터

### Sarcasm Detection

풍자적 의미나 반어법적 말을 감지하고 인식하는 것

고객 응대 챗봇에서 사용 가능

**iSarcasm**

반어법에 대한 분류 / 대체 표현까지 제공

## Deception 관련 Task 및 Data

### Fake News Detection

가짜뉴스에 대한 분류 task

**LIAR**

### Fact Checking

인터넷 상에서 유포되는 정보의 진실성을 확인하는 작업

**FEVER**

사실, evidence text 데이터

## Machin Translation 관련 Task 및 Data

### WMT Shared Task

### Quality Estimation

기계번역의 품질을 예측하는 것

* 얼마나 자연스럽고 정확한지

**관련 기술**

Sentence-level QE

Word-level QE

MQM word-level QE

**QUAK**

Word-level QE 데이터셋

### Automatic Post Editing(APE)

기계번역의 결과물을 자동으로 수정

문법, 단어 선택, 의미 전달, 일관성 등

방법론

* 문장 구조, 어휘, 문법 등 분석

* 이전 번역 결과를 고려하여 수정

**SubEdits**

### Chat Translation

## Dialogue 관련 Task 및 Data

### Persona-grounded Dialogue

사용자의 성격을 고려하여 대화를 함

맥락, 개인적인 특성을 고려하여 응답

**PersonaChat**

Persona description을 annotation하여 대화

**BSBT**

BotsTalk

### Persuasive Dialogue

상대방을 설득하기 위한 대화

광고, 마케팅, 정치, 교육 등에 활용

**Persuasion for Good**

건강목표를 달성하는 task

환경보호에 대한 task

### Dialogue Summarization

대화 기록이나 대화 데이터를 요약하는 것

long-term memory 향상에도 활용

**DialogSum & SAMSum**

### Knowledge-grounded Dialogue

외부 지식을 별도로 활용하여 대화하는 기술

factual knowledge 부여

**Wizard Of Wikipedia**

**Wizard Of Internet**

### Dialogue for Characters

풍부한 컨텍스트 정보를 제공해 스토리 내 캐릭터에 대한 dialogue agent 생성

**Harry Potter Dialogue(HPD)**

### Empathetic Dialogue

상대방의 감정을 고려하고 이를 공감하는 대답을 생성

**EmpatheticDialogues(ED)**

**DailyDialog**

## 기타 Task 및 Data

### ImageNet-X

컴퓨터 비전 분야에서 대표적인 데이터셋 중 하나인 ImageNet을 확장

### Question Generation

주어진 지문과 목표 답변에 따라 유효하고 유창한 질문을 생성하는 것

QA 시스템에서 중요한 구성요소, 교육분야에서 활용

### Document-level Relation Extraction

문서 전체에서 개체(entity)에 대한 속성(attribute)과 관계(relation)을 예측하는 RE를 확장

KG(Knowledge Graph)를 구축하는 핵심 구성 요소

**DocRED**

## 한국어 관련 Task 및 Data

**고전어 데이터셋**

Ancient Korean Neural Machine Translation

조선왕조 실록/ 일성록 기반 한자 벤치마크 데이터셋

승정원일기 번역

**케어콜 데이터셋**

독거노인 대상 일상 심리케어 데이터셋

**혐오발언 탐지 데이터셋**

APEACH

KOLD

**쓰기 평가 데이터셋**

한국어 학습자 쓰기 평가의 자동점수 구간 분류

**문법 교정 데이터셋**

K-NCT(오류 유형 분류한 데이터셋)

<br/>

# 6) Data-Centric을 통해 재해석하는 History of NLP
---

## 1. 규칙 기반 NLP

전문가의 시대

Rule에 맞게 처리하는 시스템

자연언어 문장 - 형태소 분석 - 구문 분석 - 의미 분석 - 담화 분석 - 분석 결과

## 2. 통계 기반 NLP

모두의 시대

대량의 텍스트 데이터로 통계를 내어 단어를 표현

Sparsity Problemn으로 한계 도달

Statistical Machine Translation

* 구 Parallel Corpus의 allignment를 학습

학습 단위에 따라 발전

Word based SMT - Phrase - Hierarchical Phrase - Prereordering - Syntax

## 3. Machine Learning 및 Deep Learning 기반 NLP

전문가 + 모두 공존의 시대

ML -> DL로 넘어가며 Feature extraction 과정이 사라짐

Neural Machine Translation

Language Model = 지식표현 체계

## 4. Pre-train & Fine-tuning 기반 NLP

대중이 만든 데이터(Pre-train) + 전문가가 만든 데이터(Fine-tune)

task-specific fine-tuning

**벤치마크의 등장**

영향력

Transformer의 등장 이후로 NLP 연구의 메인 트렌드가 됨

## 5. Neural Symbolic NLP

전문가의 시대

전문가의 데이터를 전면 활용

상식정보, 추론 능력 등 딥러닝 모델의 한계를 보완하기 위해

* Knowledge Base Question Answering

## 6. Large Language Models

모두의 시대 - 무의식적 데이터 생성

대규모 언어 모델

국내 및 국외 다양한 기업이 자신만의 LLM 개발

**Foundation Models**

* 방대한 양으로 학습해 다양한 task를 수행할 수 있는 LLM

* adaptation은 fine-tuning이 아닌 In-context Learning

* LoRA

* In-context Few-Shot Learning & Prompt learning

## 7. Human FeedBack Data 기반 NLP

모두의 시대 - 의식적 데이터 생성(피드백)

ChatGPT

피드백을 반영하는 Reinforcement Learning

강화학습 기반 생성방식

검색의 새로운 패러다임

* 검색 주도권이 인간에게 넘어옴

**Prompt Engineering**

새로운 직군의 등장 = Data의 중요성

* 비판적 사고력

## Summary

규칙기반 NLP -> Human FeedBack NLP

전문가의 데이터 의존 시대 -> 모두의 의식적 데이터 생성 시대

<br/>

# 7) Data-Centric NLP 응용 분야
---

## Without Model Modification

Model Modification 없이 어떻게 모델의 성능을 향상시킬 수 있을까?

Subword Tokenization, Data Augmentation, Data Filtering, Synthetic Data, Training Strategies

### Subword Tokenization

토큰화

주어진 말뭉치를 토큰으로 나누는 작업

* 토큰의 정의에 따라 달라짐

서브워드 토큰화

주어민 말뭉치를 서브워드 단위로 나누는 작업

* OOV(Out of Vocabulary), 희귀단어, 신조어 등의 문제 해소 가능

Softmax의 결과는 vocabulary의 사이즈의 크기에 좌우된다

**BPE(Byte Pair Encoding)**

가장 빈도수가 높은 유니그램 쌍을 하나의 유니그램으로 통합

bottom-up 방식의 접근

한국어는 교착어이므로 단어가 형태소(어간, 접사)로 구성됨

형태소 기반 서브워드 토큰화가 유리함

### Data Augmentation

원본 데이터를 변환하거나 새로운 데이터를 추가하여 데이터의 수를 늘리는 기법

오버피팅 방지에 도움이 됨

**Rule-Based**

사전 정의된 변형방식을 적용

* Easy Data Augmentation(EDA, SR, RI, RS, RD 방식)

* Unsupervised Data Augmentation(UDA)

**Example Interpolation**

MixUP을 적용하여 둘 이상의 실제 예시로부터 입력값과 레이블을 보간

* Mixed Sample Data Augmentation(MSDA)

**Model-Based**

Seq2seq이나 언어모델을 사용

* Back-Translation(BT)

* Fine-Tuning GPT for Paraphrasing

### Data Filtering

Data Filtering vs. Data Cleaning

데이터 필터링은 제거를 통해 실제 데이터 양이 줄어 듦

데이터 클리닝은 데이터 전처리와 비슷한 개념

(불용어 처리, Stemming, Lemmatization)

병렬 말뭉치(Parallel Corpus)

두 개 언어 이상의 번역된 문서를 모은 말뭉치

* 위키백과

* OPUS, AI Hub

병렬 말뭉치 필터링(PCF, Parallel Corpus Filtering)

* 언어 감지 필터(원하는 언어인지 확인)

* 수용 가능성 필터(수용 가능할 정도로 유사한지 확인)

* 도메인 필터(Out-of-domain 이 아닌지 확인)

### Synthetic Data

합성 데이터

통계적, 전산학적 기법으로 생성한 데이터

* GPT-3를 통한 데이터 생성

한국어 맞춤법 교정 연구를 위한 합성 데이터

Deletion, Insertion, Substition를 통해 잘못된 문장 생성하여 학습에 사용

### Training Strategies

커리큘럼 학습

쉬운 내용부터 어려운 내용으로 단계적으로 모델을 학습하는 ML 기법

## Data Measurement

Inter-Annotator Agreement(IAA)

2명 이상의 어노테이터가 생성한 레이블리 얼마나 일관성 있는지에 관한 지표

데이터 품질과 관련 있음

**주요 Metric**

* Cohen's Kappa, 2명의 작업자의 레이블 일치도에 따라 분리

* Fleiss' Kappa, 3명 이상의 레이블 일치도에 따라 분리

* Krippendorff's Alpha, 빈 값이 있어도 average를 통해 추정

## HCI

좋은 데이터란?

일관성 있게 라벨링된 데이터

중요한 케이스를 포함한 데이터

예상치 못한 케이스까지 포함한 데이터

적절한 사이즈의 데이터

**Data Cascade**

AI/ML 분야에서 데이터 품질의 중요성 과소평가

좋은 데이터의 라이프 사이클

* Motivation, Composition, Collection

* Pre-processing, Cleaning, Labeling

* Uses, Distribution, Maintenance

체크리스트

* 전처리, 클리닝, 라벨링 단계

* Raw data 별도 저장

* 사용한 SW가 있다면 공개했는가?

이외 체크리스트

* Meta data가 얼마나 informative한가

* 정당한 보상, 불필요한 비용 지불 x

* Versioning 체계

* 저장 폴더 구조가 직관적이고 clean한가

### Model based Data-Centric AI

DMOps와 같은 체계적인 Process

레이블 일관성을 고려하여, 주관이 들어가지 않도록 설정된 가이드라인

쉽고 효율적인 데이터 제작 Tool

Model의 결과를 방향성으로 지속적인 클렌징 과정을 거친 데이터

