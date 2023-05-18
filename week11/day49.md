# week 11 

## 대회 3주차

### Task: Multi-sentence Test


|문제 및 가설|우리가 가지고 있는 정보들 중 추론 문장의 word, type이 기본 학습에는 사용되지 않고 있으며학습 과정에서 모델이 학습하는 문장에 더 많은 정보가 담겨 있을수록 추론 정확도가 향상될 것이다.또한, 기계가 학습할 수 있도록 인간의 언어를 추가 텍스트의 형태로 덧붙인다면 성능이 증가할 것이다.|
|---|---|
| 적용한 상세 내용 | Typed entity marker(punct) + ‘obj는 suj의 type이다. 이 때, 이 둘의 관계는?’‘이 때, 이 둘의 관계는?’ 이라는 문장은 텍스트 증강에 초점을 맞춰 성능 가능성 파악을 위해 가볍게 추가해 본 문장이므로 다양한 형태로 실험 가능 |
| 적용한 내용에 대한 근거 | 1. 기존 [An improved Baseline for Sentence-level RE>]논문 내 베스트 성능을 보여준 Typed entity marker 그대로 적용 + 2. [GPT Understands, Too, 2021] 논문의 continuous space(내용을 인간이 직접 작성하는 discrete space와는 상반되는 개념) 기반 P-tuning 활용, [Context Aware Named Entity Recognition and Relation Extraction, 2022] 논문의 주변 text를 활용하였을 때 RE task performance가 증가하는 점에서 착안해 우리가 가진 continuous space 상의 entity 정보(word,type)를 prompt에 추가하여 학습 시도 |
| 평가 | 제출성능 : 73.22(현재 베스트 74.30은 diversity 평가를 위해 기존 모델과 voting한 결과, 앙상블은 입력된 각 모델의 diversity가 보장될수록 성능이 향상되기 때문에 71점을 가진 기존 모델 2개와의 hard voting 이후에도 성능이 향상된 것으로 보아해당 학습 과정은 기존의 모델과 diversity를 가진다는 것을 보장할 수 있음) |
| 추가 의견 및 실험 계획 여부 | 이 실험은 샘플 실험으로 확실히 성능은 확인 됐으니 구체화하여 근거 1과 2를 구분하여 별도의 항목에서 재실험 필요, 후에 두 실험의 결과를 합친 재실험도 필요 |
| wandb URL | https://wandb.ai/gyubin5009/KLUE-RE?workspace=user-yeppi315 |

<br/>

##  모델 상세 스펙

- Model args
    
    ```python
    MODEL_NAME = "klue/roberta-large"
    
    training_args = TrainingArguments(
        output_dir='./results',          # output directory
        save_total_limit=3,              # number of total save model.
        save_steps=500,                 # model saving step.
        num_train_epochs= 4,              # total number of training epochs
        learning_rate=1e-5,               # learning_rate
        per_device_train_batch_size=16,  # batch size per device during training
        per_device_eval_batch_size=16,   # batch size for evaluation
        warmup_steps=500,                # number of warmup steps for learning rate scheduler
        weight_decay=0.01,               # strength of weight decay
        logging_dir='./logs',            # directory for storing logs
        logging_steps=100,              # log saving step.
        evaluation_strategy='steps', # evaluation strategy to adopt during training
                                     # `no`: No evaluation during training.
                                     # `steps`: Evaluate every `eval_steps`.
                                     # `epoch`: Evaluate every end of epoch.
        eval_steps = 1000,            # evaluation step.
        load_best_model_at_end = True
      )
    ```



## ⚪ 실험 상세 내용 - 시각화 자료

| No. | Type | Example | micro_f1_score |
| --- | --- | --- | --- |
| 1 | 이 문장에서 {obj_word}는 {sbj_word}의 {trans[obj_type]}이다. 이 때, 이 둘의 관계는 | 이 문장에서 SM C&C는 전현무의 단체이다. 이 때, 이 둘의 관계는1 | 86.37(val) 73.39(test) |
| 2 | 이 문장에서 {obj_word}는 {sbj_word}의 {trans[obj_type]}[{obj_type}]이다. 이 때, 이 둘의 관계는 | 이 문장에서 SM C&C는 전현무의 단체[ORG]이다. 이 때, 이 둘의 관계는 |  |
| 3 | 이 문장에서 {sbj_word}는 {obj_word}의 {trans[sbj_type]}이다. 이 때, 이 둘의 관계는 | 이 문장에서 전현무는 SM C&C의 사람이다. 이 때, 이 둘의 관계는2 | 86.45(val) 73.02(test) |
| 4 | 이 문장에서 {sbj_word}는 {obj_word}의 {trans[sbj_type]}[{sbj_type}]이다. 이 때, 이 둘의 관계는 | 이 문장에서 전현무는 SM C&C의 사람[PER]이다. 이 때, 이 둘의 관계는3 | 86.06(val) 72.57(test) |
| 5 | 이 문장에서 {obj_word}는 {sbj_word}의 {trans[obj_type]}이다. | 이 문장에서 SM C&C는 전현무의 단체이다. |  |
| 6 | x | 아무것도 적용 x (type entity marker만 사용)5 | 85.76(val) |
| 7 | 이 문장에서 {obj_word}와 {sub_word}의 관계는? | 이 문장에서 SM S&C와 전현무의 관계는?4 | 86.03(val) 71.13(test) |
| 8 | '이 문장에서 {obj_word}는 {trans[sbj_type]}인 {sbj_word}의 {trans[obj_type]}이다. {obj_word}와 {sbj_word}의 관계는?’ | 6 |  |
