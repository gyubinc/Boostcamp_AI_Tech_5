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