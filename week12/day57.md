# 8) Recent Work in Data-Centric NLP
---

## Data Augmentation

"Iterative Back-Translation for Neural Machine Tranlsation"

* Back-Translation loop을 2차례 반복하는 것

"How Effective is Task-Agnostic Data Augmentation for Pretrained Transformers?"

* BERT와 같은 모델에서는 기존의 BT, EDA 등의 효과가 적음을 보여줌

"ChatAug: Leveraging ChatGPT for Text Data Augmentation"

* ChatGPT를 통한 Data Augmentation

## Data Filtering

병렬 말뭉치 필터링(Parallel Corpus Filtering)

Rule Based, Statistic Based, NMT Based

대부분의 Filtering은 Rule-based로 걸러진다(매우 중요)

* WMT, WAT

## Synthetic Data

PromptBase

* 효과적인 Generative AI 사용을 위한 Prompt를 사고 파는 웹 사이트

"Pre-train, Prompt, and Predict: A Systematic Survey of Prompting Methods in Natural Language Processing"

언어모델에게 입력으로 주어지는 템플릿 글을 프롬프트라고 함

최근 NLP 모델에서는 Model Fine-tuning과 더불어 Prompt Runing이 필요해짐

"http://pretrain.nlpedia.ai"

"Prompt Programming for Large Language Models: Beyond the Few-shot Paradigm"

**Meataprompt**

Prompt를 생성하기 위한 Prompt

**합성 데이터**

음성인식 후처리기 연구를 위한 합성 데이터

## Data Measurement

"Measuring Annotator Agreement Generally across Complex Structured, Multi-object, and Free-text annotation Tasks"

IAA의 Metric 중 Krippendorff's Alpha는 복잡한 태스크에 적용이 어려움

* 적절한 distance function을 고르기 어렵다는 점과 결과 해석에 명확한 기준이 없다는 문제가 있음

* 새로운 IAA measure KS 제시

"Everyone's Voice Matters: Quantifying Annotation Disagreement Using Demographic Information"

인구통계학적 정보를 바탕으로 주석 작업자간의 불일치 정도 예측기를 학습함

### 이 외 Data-Centric AI 주제들

* Label Errors

* Data-centric Evaluation of ML Models

* Class Imbalance, Outliers, and Distribution Shift

* Data Privacy and Security

* Training Strategies

### Cross Lingual Transfer Learning

"Exploring the Data Efficiency of Cross-Lingual Post-Training in Pretrained Language Models"

다른 언어로 학습된 Language Model을 사용할 수 없을까?

* Adaptation layer를 추가

* Post-training 후 Fine-tuning

<br/>

# 9) Future of Data-Centric NLP
---

## Multi-Model AI

여러 가지 다른 유형의 데이터(텍스트, 이미지, 비디오)를 함께 처리하여 더 정확하고 효과적인 모델을 구축하는 기술

Real-world에서는 Uni-Modal 데이터만으로는 충분한 정보를 얻을 수 없는 경우가 많음

### Mathematical/Arithmetic Reasoning

GSM8K

CLEVR-Math

### Multi-Modal 대화 데이터셋

DialogCC

MMDialog

VE(Visual Entailment)

VQA v2.0

VQG(Visual Question Generation)

TextVQA

OK-VQA

Visual Dialog

VCR(Visual Commonsense Reasoning)

Winoground

TextCaps

FFHQ-Text

### Video

SumMe

MSR-VTT

VidLN

**Multi-Modal = AI를 더 사람처럼**

## Neuro-Symbolic AI

Symbolic AI와 Neural network를 결합하여 새로운 종류의 AI 모델을 만드는 연구 분야

논리적 추론 + 통계적 패턴 학습

치열한 논쟁(LLM vs Neuro-Symbolic)

모델의 크기가 늘면 해결될 것이다 vs 논리적 추론이 필요하다

Knoledge graph + LLM

Reasoning + Learning(순서에 따라 작동 방식 다양함)

## Reinforcement Learning with Human Feedback

RL의 기본 아이디어는 agent가 자신이 행동하는 environment와의 상호 작용을 통해 학습한다는 것

agent = LM(policy = LM의 parameter)

* RL에서 agent는 학습하려는 모델

* RL에서 policy는 모델이 어떻게 행동할지 결정하는 알고리즘

environment = LM의 input, 즉 prompt

* RL에서 environment는 agent의 주변 환경을 의미

action = token 생성 및 sequence 생성

* RL에서 action은 agent가 할 수 있는 행동

reward = LM의 Output

* RL에서 reward는 agent가 한 action에 따라, environment에 따라 주는 보상

인간의 피드백을 성능의 척도로 사용하고, 그 피드백을 loss로 사용하는 것

작동방식

Pre-train language model(LM 확보)

Gathering data and training a reward model

Fine-tune language model with reinforcement learning

## GPT-4

LLM + Multimodal + RLHF

* Creativity(Reasoning 능력의 향상)

* Visual Input(Multimodal)

* Longer Context

ChatGPT < GPT-4

논문 요약(이미지 그 자체를)

만화 이해

Chart 추론(결과 해석)

"GPT-4 Technical Report"