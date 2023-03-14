# 1) Introduction to Pytorch
---

## Pytorch

딥러닝 전 과정에서 쓰이는 가장 기본이 되는 프레임워크

**Pytorch(facebook) vs Tensorflow(google)**

**Keras**

wrapper(껍데기), High level API

* Tensorflow는 Static graph (Define and run)

* Pytorch는 Dynamic computation graph (자동미분시 실행 시점에서 그래프 정의)

**Computational Graph**

연산의 과정을 그래프로 표현

* Define and Run (Tensorflow)
그래프를 먼저 정의 -> 실행시점에 데이터 feed

* Define by Run (Pytorch)
실행을 하면서 그래프를 생성하는 방식

**tensorflow**

Production, Cloud, Multi-GPU, scalability(확장성) 에 장점

**Pytorch**

디버깅 유용, 논문 작성시 좋음, 배우기 쉬움, 우상향

* Define by Run(즉시 확인 가능) => Pythonic code

* GPU support, Good API and community

**Pytorch 장점**

* Numpy + AutoGrad + Function

* Numpy 구조를 가지는 Tensor 객체로 array 표현

* 자동미분을 지원하며 DL 연산을 지원

* 다양한 형태의 DL을 지원하는 함수와 모델을 지원함

* Dataset, Multi-GPU, Data augmentation... 등 지원


# 2) Pytorch Basics
---

## Pytorch Operations

**Tensor**

다차원 Arrays를 표현하는 Pytorch 클래스

* 사실상 numpy의 ndarray와 동일

* Tensor를 생성하는 함수도 거의 동일

```python
#numpy - ndarray
import numpy as np

n_array = np.arange(10).reshape(2,5)
print(n_array)
print("ndim :", n_array.ndim, "shape :", n_array.shape)


#pytorch- tensor
import torch

t_array = torch.FloatTensor(n_array)
print(t_array)
print("ndim :", t_array.ndim, "shape :", t_array.shape)
```

Tensor 생성은 list나 ndarray를 사용 가능

```python
#data to tensor
data = [[3,5], [10,5]]
x_data = torch.tensor(data)
x_data


#ndarray to tensor
nd_array_ex = np.array(data)
tensor_array = torch.from_numpy(nd_array_ex)
tensor_array
```

**Tensor data types**

기본적으로 numpy와 동일

* GPU 사용 가능성은 다름

```python
data = [[3,5,20],[10,5,50],[1,5,10]]
x_data = torch.tensor(data)

x_data[1:]

x_data[:2, 1:]

x_data.flatten()

torch.ones_like(x_data)

x_data.numpy()

x_data.shape

x_data.dtype
```

pytorch의 tensor는 GPU에 올려서 사용 가능

```python
x_data.device
# device(type = 'cpu')

if torch.cuda.is_available():
    x_data_cuda = x_data.to('cuda')
x_data_cuda.device
# device(type = 'cuda', index = 0)
```

**Tensor handling**

* view : reshape과 동일하게 tensor의 shape을 변환
reshape는 메모리 할당 시 경우에 따라 연동이 깨질 수 있음(view 권장)

* squeeze : 차원의 개수가 1인 차원을 삭제(압축)

* unsqueeze : 차원의 개수가 1인 차원을 추가

**view**

```python
tensor_ex = torch.rand(size = (2, 3, 2))
tensor_ex

'''
tensor([[[0.5583, 0.7258],
         [0.0446, 0.1461],
         [0.4350, 0.6404]],

        [[0.5925, 0.6789],
         [0.7820, 0.8708],
         [0.0845, 0.2491]]])
'''

tensor_ex.view([-1, 6])

'''
tensor([[0.5583, 0.7258, 0.0446, 0.1461, 0.4350, 0.6404],
        [0.5925, 0.6789, 0.7820, 0.8708, 0.0845, 0.2491]])
'''


tensor_ex.reshape([-1, 6])

'''
tensor([[0.5583, 0.7258, 0.0446, 0.1461, 0.4350, 0.6404],
        [0.5925, 0.6789, 0.7820, 0.8708, 0.0845, 0.2491]])
'''
```

**squeeze & unsqueeze**

```python
#2 by 2
a = torch.tensor([[1,2],[3,4]])


#1 by 2 by 2
a.unsqueeze(0)
'''
tensor([[[1, 2],
         [3, 4]]])
'''

#2 by 1 by 2
a.unsqueeze(1)
'''
tensor([[[1, 2]],
        [[3, 4]]])
'''

#2 by 2 by 1
a.unsqueeze(2)
'''
tensor([[[1],
         [2]],
        [[3],
         [4]]])
'''
```

**Tensor operations**

numpy operation과 거의 동일(사칙연산)

* 행렬곱셈 연산 함수는 dot이 아닌 mm사용

```python
n1 = np.arange(10).reshape(2,5)
t1 = torch.FloatTensor(n1)

n2 = np.arange(10).reshape(5,2)
t2 = torch.FloatTensor(n2)

t1.mm(t2)#mm은 행렬연산만 가능, 벡터일 때 오류

t1.dot(t2)#오류발생, 1차원 벡터일 경우에는 정상적으로 내적 구해줌

t1.matmul(t2)
```

matmul은 broadcasting 지원 처리

```python
a = torch.rand(5,2,3)
b = torch.rand(3)

#오류 발생
a.mm(b)

#broadcasting 지원해서 계산 가능
a.matmul(b)
'''
tensor([[0.3258, 0.6579],
        [0.5128, 0.3950],
        [0.1804, 0.8814],
        [0.7789, 0.3770],
        [0.6712, 0.5501]])
'''

#아래 연산과 동일
a[0].mm(torch.unsqueeze(b,1))
a[1].mm(torch.unsqueeze(b,1))
a[2].mm(torch.unsqueeze(b,1))
a[3].mm(torch.unsqueeze(b,1))
a[4].mm(torch.unsqueeze(b,1))
```

**nn.functional 모듈을 통해 다양한 수식 변환을 지원**

```python
import torch
import torch.nn.functional as F

tensor = torch.FloatTensor([0.5, 0.7, 0.1])
h_tensor = F.softmax(tensor, dim = 0)
h_tensor
# tensor([0.3458, 0.4224, 0.2318])

y = torch.randint(5, (10,5))
y_label = y.argmax(dim = 1)
# tensor([2, 0, 3, 0, 0, 4, 1, 1, 0, 2])
# 위의 결과는 '값'이 아닌 'index'이다

torch.nn.functional.one_hot(y_label)
'''
tensor([[0, 0, 1, 0],
        [1, 0, 0, 0],
        [0, 0, 1, 0],
        [0, 0, 0, 1],
        [1, 0, 0, 0],
        [1, 0, 0, 0],
        [0, 0, 1, 0],
        [0, 0, 1, 0],
        [0, 0, 1, 0],
        [0, 0, 1, 0]])
'''
```

**AutoGrad**

PyTorch의 핵심은 자동 미분의 지원 -> backward 함수 사용

```python
w = torch.tensor(2.0, requires_grad = True)
y = w**2
z = 10*y + 2
z.backward()
w.grad

# tensor(40.)
```

```python
a = torch.tensor([2., 3.], requires_grad = True)
b = torch.tensor([6., 4.], requires_grad = True)
Q = 3*a**3 - b**2
external_grad = torch.tensor([1., 1.])
Q.backward(gradient = external_grad)

a.grad
# tensor([36., 81.])

b.grad
# tensor([-12.,  -8.])
```

# 3)Pytorch 프로젝트 구조 이해

**ML 코드는 Jupyter에서 짜야 되는가?**

- 영원히 세발 자전거를 탈 수는 없다.

<br/>

**초기단계**

대화식 개발 과정이 유리

* 학습과정과 디버깅 등 지속적인 확인

<br/>

**배포 및 공유 단계**

notebook 공유의 어려움

* 쉬운 재현의 어려움, 실행순서 꼬임

<br/>

**DL 코드도 하나의 프로그램**

개발 용이성 확보와 유지보수 향상 필요

<br/>

**코드도 레고블럭처럼**

OOP + 모듈 -> 프로젝트

<br/>

## Pytorch Project Template

* 다양한 프로젝트 템플릿이 존재

* 사용자 필요에 따라 수정하여 사용

* 실행, 데이터, 모델, 설정, 로깅, 지표, 유틸리티 등 다양한 모듈들을 분리하여 프로젝트 템플릿화

---
추천 repository, 팩토리 패턴의 configparser 구성

<https://github.com/victoresque/pytorch-template>

---

```
# 구성 파일
(gyubin) C:\Users\yeppi\workspace\pytorch-template>ls

LICENSE    base         data_loader  model           parse_config.py   test.py   trainer
README.md  config.json  logger       new_project.py  requirements.txt  train.py  utils
```

## SSH로 서버 연결

```python
# NGROK에서 토큰 받아 사용
NGROK_TOKEN = 'NGROK 토큰 코드'
PASSWORD = '비밀번호'

!pip install colab-ssh
from colab_ssh import launch_ssh

launch_ssh(NGROK_TOKEN, PASSWORD)
```


> 해당 colab에서 실행 후 VS Code로 돌아옴
-> add ssh new -> ssh root@복사한 HOSTNAME -p 복사한PORT
-> 구성열기 -> CONNECT -> 비밀번호 입력