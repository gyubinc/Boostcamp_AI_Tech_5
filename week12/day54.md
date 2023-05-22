# 1) Data-Centric AI
---

## 일상 속의 인공지능

* 추천 시스템

* 검색

* OCR

* 기계번역

* 영문법 교정기

* 문서 요약

* 비디오 요약

* 가상비서, AI 스피커

* 얼굴 인식

* 자율주행

* DeepBlue(인공지능 체스)

* Atari

* IBM Watson

* Exobrain

* Alpha Go

* AI X Art

* AI X Fashion

* AI X Biology

* AI X Game

* AI X Entertainment

* AI X Journalism

* AI X Dating, Friends

* AI X Creation

* AI X Creation

* AI X Music

* AI X Healthcare

* AI X Sports

* AI X Programming

* AI X Real-Time Translation

* AI X Ethics

* AI X Our Daily Life

<br/>

## Data-Centric AI

### AI System의 구성 요소

AI system = code(model/algorithm) + data

**Improving the Code vs Data**

| |Stell defect detection|Solar panel|Surface inspection|
|:---:|:---:|:---:|:---:|
|Baseline|76.2%|75.68%|85.05%|
|Model-centric|+0%|+0.04%|+0.00%|
|Data-centric|+16.9%|+3.06%|+0.4%|

**모델링을 통한 성능 향상이 아닌 데이터를 통한 성능 향상**

<br/>

# 2) Data-Centric AI - In the wild
---

## AI Service의 개발 사이클

**1. Project Setup**

* 프로젝트 정의

**2. Data Preparation**

* 데이터셋 준비

**3. Model Training**

* 모델 학습 및 디버깅

**4. Deploying**

* 설치 및 유지보수

### MLOps

### LLMOps

Large Language Model(LLM) Ops

### Model-Centric vs Data-Centric

| |Model-Centric view|Data-Centric view|
|---|---|---|
|데이터 수집 시 우선사항|최대한 많은 Data 수집|Data의 일관성|
|성능 향상 방법|새로운 Model Architecture 제안 Model의 구조 수정|Data의 질 향상|
| |Data를 고정하고, Model을 개선함|Model을 고정하고, Data를 개선함|

## Data-Centric AI의 정의

성능 향상을 위해 Data 관점에서 고민 = Hold the Code / Algorithms fixed

* ex) Data Management(새로운 Data 수집), Data Augmentation(데이터 증강), Data Filtering, Synthetic Data(합성 데이터), Label Consistency(라벨링 방법 체계화), Data Consistency, Data Tool(라벨링 Tool)

Model Modification 없이 어떻게 모델의 성능을 향상시킬 수 있을까?

* Data Quality Control, Data Augmentation 및 Synthetic Data를 통한 모델 성능 향상

* AI algorithms that understand data and use that information to improve models

* Curriculum learning, Active Learning 등

Data-Centric Evaluation

* 모델의 성능 평가 지표 개발, Data Measurement

## Data-Centric AI in Real-world

**Data-Flywheel**

서비스 과정에서 쌓이는 데이터를 모델 학습 데이터로 가공하여 추가 학습을 진행하는 선순환 생태계

**DMOps**

Data 제작에 대한 A-Z

**Data Development**

Schema Design - Collection - Annotation - Evaluation - Versioning

**Data Labeling Tool**

**ChatGPT improved GPT-3 by improving data quality**

ChatGPT was fine-tuned to:

* Minimize harmful, untruthful, or biased output

* Used human rankings of potential outputs to put lower-weighting on 'bad data'

## Data-Centric AI in Academia

학계에서 데이터를 다루기 힘든 이유

1) 좋은 데이터를 많이 모으기 힘들고, 데이터는 아직 미지의 영역이다

2) 라벨링 작업에 대한 명확한 정답이 없고 비용이 크다

* 좋은 데이터

* 일관성 있게 라벨링된 데이터

* 중요한 케이스가 포함된 데이터

* 예상치 못한 케이스까지 포함된 데이터

* 적절한 크기의 데이터

* 특이 경우를 발견하고 해당 샘플들을 모으며, 이를 포함한 라벨링 가이드를 만들어야 한다

3) High Quality Data가 필요하다(데이터의 양 < 데이터의 질)

4) 데이터의 균형이 맞아야 한다

5) 학계는 정해진 테스트셋 내에서 경쟁하는 방식이다

## Academia와 Industry(In teh wild)의 간극이 좁아지기 위한 시도들

### DataPerf

모델 위주의 학계와 데이터 위주의 Industry 사이의 간극을 줄인다

**목표**

ML 데이터 품질 향상을 위해 Data-Centric 파이프라인의 주요 단계를 벤치마크

데이터셋을 쉽고 반복 가능하게 유지 관리 및 평가

**DataPerf Design**

모델은 고정하고, 데이터셋만 개선하여 정확도를 향상시킬 수 있는 벤치마크 테스크 정의

## 벤치마크 타입

* Training Set Creation

* Test Set Creation

* Selection Algorithm

* Debugging Algorithm

* Slicing Algorithm

* Valuation Algorithm



