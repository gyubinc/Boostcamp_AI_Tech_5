# 과제

**Custom Model 제작**

```python
# 사용 클래스 및 메소드
```

# 4)AutoGrad & Optimizer
---

**논문을 구현해보자**

**수많은 반복의 연속**

**Layer = Block**

## torch.nn.Module

딥러닝을 구성하는 Layer의 base class

* Input, Output, Forward, Backward(autograd) 정의

* 학습의 대상이 되는 parameter(tensor, weight) 정의

## nn.Parameter

Tensor 객체의 상속 객체

* nn.Module 내에 attribute가 될 때는 required_grad = True로 지정되어 학습 대상이 되는 Tensor

* 우리가 직접 지정할 일은 잘 없음<br/>대부분의 layer에는 weights 값들이 지정되어 있음

* low level 의 API

## Backward

Layer에 있는 Parameter들의 이분을 수행

* Forward의 결과값(model의 output = 예측치)과 실제값간의 차이(loss)에 대해 미분을 수행

* 해당 값으로 Parameter 업데이트

```python
criterion = torch.nn.MSELoss()
optimizer = torch.optim.SGD(model.parameters(), lr = learningRate)

for epoch in range(epochs):
    #이전의 gradient 초기화
    optimizer.zero_grad()

    #예측값 계산
    outputs = model(inputs)

    #예측값과 실제값과의 차이 loss 계산
    loss = criterion(outputs, labels)
    print(loss)

    #loss에 대해 backward 진행
    loss.backward()

    #지정된 learning rate만큼 update
    optimizer.step()
```

**Backward from the scratch**

실제 backward는 Module 단계에서 직접 지정 가능

* Module에서 backward와 optimizer오버라이딩

* 사용자가 직접 미분 수식을 써야하는 부담<br/>쓸 일은 없으나 순서는 이해할 필요 있음

# 7)PyTorch Dataset

데이터 전개

1. data 수집

2. Dataset class에서 init, len, getitem 설정

3. transforms 전처리 (ToTensor, CenterCrop)

4. DataLoader 에서 묶어서 피딩(batch, shuffle)

5. Model 입력

## Dataset 클래스

데이터 입력 형태를 정의하는 클래스

* 데이터를 입력하는 방식의 표준화

* Image, Text, Audio 등에 따른 다른 입력정의

**관련 모듈**

```python
torch.utils.data: 데이터셋의 표준 정의, 데이터셋 부르고 자르고 섞는데 쓰는 도구들
torchvision.dataset: Dataset을 상속하는 이미지 데이터셋의 모음
torchtext.dataset: Dataset을 상속하는 텍스트 데이터셋의 모음
torchvision.transforms: 여러 가지 변환 필터(totensor, resize, crop, brightness..)
torchvision.utils: 이미지 데이터 저장 및 시각화
```


**사용법**

```python
import torch
from torch.utils.data import Dataset

class CustomDataset(Dataset):
    #초기 데이터 설정방법 지정
    def __init__(self, text, labels):
        self.labels = labels
        self.data = text
    
    #데이터의 전체 길이
    def __len__(self):
        return len(self.labels)

    #index 값을 주었을 때 반환되는 데이터의 형태(X, y)
    def __getitem__(self, idx):
        label = self.labels[idx]
        text = self.data[idx]
        sample = {"Text": text, "Class": label}
        return sample
```

**유의점**

* 데이터 형태에 따라 각 함수를 다르게 정의(NLP, 오디오...)

* 모든 것을 데이터 생성 시점에 처리할 필요는 없음<br/>: image의 Tensor 변화는 학습에 필요한 시점에 변환

* 데이터 셋에 대한 표준화된 처리방법 제공 필요<br/>-> 후속 연구자 또는 동료에게는 빛과 같은 존재

* 최근에는 HuggingFace 등 표준화된 라이브러리 사용

## DataLoader 클래스

Data의 Batch를 생성해주는 클래스

* 학습직전(GPU fedd전) 데이터의 변환을 책임

* Tensor로 변환 + Batch 처리가 메인 업무

* 병력적인 데이터 전처리 코드의 고민 필요

**사용법**

```python
# Dataset 생성
text = ['Happy', 'Amazing', 'Sad', 'Unhappy', 'Glum']
labels = ['Positive', 'Positive', 'Negative', 'Negative', 'Negative']
MyDataset = CustomDataset(text, labels)

#DataLoader Generator
MyDataLoader = DataLoader(MyDataset, batch_size = 2, shuffle = True)
next(iter(MyDataLoader))
# {'Text': ['Glum', 'Sad'], 'Class': ['Negative', 'Negative']}

MyDataLoader = DataLoader(MyDataset, batch_size = 2, shuffle = True)
for dataset in MyDataLoader:
    print(dataset)
# {'Text': ['Glum', 'Unhappy'], 'Class': ['Negative', 'Negative']}
# {'Text': ['Sad', 'Amazing'], 'Class': ['Negative', 'Positive']}
# {'Text': ['Happy'], 'Class': ['Positive']}
# 하나의 EPIC
```

**DataLoader Parameter**

```python
DataLoader(dataset, batch_size=1, shuffle=False, sampler=None,batch_sampler=None, num_workers=0, collate_fn=None,pin_memory=False, drop_last=False, timeout=0,worker_init_fn=None, *, prefetch_factor=2, persistent_workers=False)

'''
collate_fn: [[D, L],[D, L]...] 형태의 데이터를 [D, D,...] [L, L, ...] 형태로 변경
글자수가 다른 text데이터의 경우 padding이 필요한데 collate_fn에 padding 정의할 때 사용
'''
```

## Casestudy

데이터 다운로드부터 loader까지 직접 구현해보기

* NotMNIST 데이터의 다운로드 자동화 도전

```python
'''
버전 충돌시 코드

#Error)
OMP: Error #15: Initializing libiomp5md.dll, but found libiomp5md.dll already initialized.
'''

#Code)
import os
os.environ['KMP_DUPLICATE_LIB_OK']='True'
```
