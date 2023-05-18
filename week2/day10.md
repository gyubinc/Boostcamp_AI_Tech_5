# 8) Multi-GPU 학습
---

**개념정리**

* Single vs Multi

* GPU vs Node

* Single Node SSingle GPU

* Single Node Multi GPU

* Multi Node Multi GPU

## Model parallel

다중 GPU에 학습을 분산하는 두가지 방법

* 모델을 나누기 / 데이터를 나누기

* 모델을 나누는 것은 생각보다 예전부터 썼음(alexnet)

* 모델의 병목, 파이프라인의 어려움 등으로 인해 모델 병렬화는 고난이도 과제

```python
class ModelParallelResNet50(ResNet):
    def __init__(self, *args, **kwargs):
        super(ModelParallelResNet50, self).__init__(Bottleneck, [3,4,6,3], 
        num_classes=num_classes, *args, **kwargs)
    
    self.seq1 = nn.Sequential(self.conv1, self.bn1, self.relu, 
    self.maxpool, self.layer1, self.layer2).to('cuda:0')

    self.seq2 = nn.Sequential(self.layer3, self.layer4, 
    self.avgpool).to('cuda:1')

    self.fc.to('cuda:1')

    def forward(self, x):
        x = self.seq2(self.seq1(x).to('cuda:1'))
        return self.fc(x.view(x.size(0), -1))
```

## Data parallel

데이터를 나눠 GPU에 할당 후 결과의 평균을 취하는 방법

* minibatch 수식과 유사한데 한번에 여러 GPU에서 수행

* PyTorch 기능 : DataParallel, Distributed DataParallel

**DataParallel**

단순히 데이터를 분배한 후 평균을 취함

* GPU 사용 불균형 문제 발생, Batch 사이즈 감소(한 GPU가 병목), GIL(Global Interpreter Lock)

**DistributedDataParallel**

각 CPU마다 process 생성하여 개별 GPU에 할당

* 기본적으로 DataParallel로 하나 개별적으로 연산의 평균을 냄

```python
# DataParallel
parallel_model = torch.nn.DataParallel(model)

predictions = parallel_model(inputs)
loss = loss_function(predictions, labels)
loss.mean().backward()
optimizer.step()
predictions = parallel_model(inputs)
```

```python
# DistributedDataParallel
train_sampler = otrch.utils.data.distributed.DistributedSampler(train_data)
shuffle = False
pin_memory = True

trainloader = torch.utils.data.DataLoader(train_data, batch_size = 20, shuffle = True, pin_memory = pin_memory, num_workers = 3, shuffle = shuffle, sampler = train_sampler)

'''
그 후에도 multiprocessing.spawn 정의
main 함수에서 distributed.init_process_group(멀티프로세싱 통신 규약 정의)
Distributed DataParallel 정의...
'''
```

# 9) Hyperparameter Tuning
---

**1. 모델 수정**

**2. 데이터 추가 or 수정 (가장 큰 영향)**

**3. hyperparameter tuning**

## Hyperparameter Tuning

모델 스스로 학습하지 않는 값은 사람이 지정(learning rate, 모델의 크기, optimizer 등)

* 하이퍼 파라미터에 의해서 값이 크게 좌우 될 때도 있음(요즘은 그닥)

* 마지막 0.01을 쥐어짜야 할 때 도전해볼만!

* 가장 기본적인 방법 - grid vs random

* 최근에는 베이지안 기법들이 주도 (BOHB 2018)

<br/>

**Ray**

multi-node multi processing 지원 모듈

* ML/DL의 병렬 처리를 위해 개발된 모듈

* 기본적으로 현재의 분산병렬 ML/DL 모듈의 표준

* Hyperparameter Search를 위한 다양한 모듈 제공

* Ray를 사용하기 위해서는 모델이 하나의 함수 안에 다 들어가야 한다

```python
#관련 모듈 다운
!pip install Ray
!pip install tensorboardX
from ray import tune
from ray.tune import CLIReporter
from ray.tune.schedulers import ASHAScheduler


data_dir = os.path.abspath("./data")
load_data(data_dir)

#config에 search space 지정
config = {'l1': tune.sample_from(lambda_:2**np.random.randint(2, 9)), 'l2': tune.sample_from(lambda_:2**np.random.randint(2,9)), 'lr': tune.loguniform(1e-2, 1e-1), 'batch_size': tune.choice([2,4,8,16])}

#학습 스케줄링 알고리즘 지정
scheduler = ASHSAcheduler(metric = 'loss', mode = 'min', max_t = max_num_epochs, grace_period = 1,reduction_factor = 2)

#결과 출력 양식 지정
reporter = SLIReporter(metric_columns = ['loss', 'accuracy', 'training_iteration'])

#병렬 처리 양식으로 학습 시생
result = tune.run(partial(train_cifat, data_dir = data_dir), resources_per_trial = {'cpu': 2, 'gpu': gpus_per_trial}, config = config, num_samples = num_samples, scheduler = scheduler, progress_reporter = reporeter)

```

# 10) PyTorch Troubleshooting
---

## OOM

**Out of Memory**

* 왜 발생했는지 알기 어려움

* 어디서 발생했는지 알기 어려움

* Error backtracking이 이상한데로 감

* 메모리의 이전상황의 파악이 어려움

**기본적 해결법**

Batch size 줄이기 -> GPU clean -> RUN

**1. GPUtil 사용하기**

* nvidia-smi처럼 GPU의 상태를 보여주는 모듈(iter마다 보여주지는 않음)

* Colab은 환경에서 GPU 상태 보여주기 편함

* iter마다 메모리가 늘어나는지 확인!

```python
!pip install GPUtil

import GPUtil
GPUtil.showUtilization()
```

**2. torch.cuda.empty_cache()**

* 사용되지 않은 GPU상 cache를 정리

* 가용 메모리를 확보

* del 과는 구분이 필요

* reset 대신 쓰기 좋은 함수

```python
import torch
from GPUtil import showUtilization as gpu_usage

print("Initial GPU Usage")
gpu_usage()

tensorList = []
for x in range(10):
    tensorList.append(torch.randn(10000000, 10).cuda())

print("GPU Usage after allocating a bunch of Tensors")
gpu_usage()

del tensorList

print("GPU Usage after deleting the Tensors")
gpu_usage()

print("GPU Usage after emptying the cache")
torch.cuda.empty_cache()
gpu_usage()
```

**3. training loop에 tensor로 축적되는 변수는 확인할 것**

tensor로 처리된 변수는 GPU 상에 메모리 사용

* 해당 변수 loop 안에 연산이 있을 때 GPU에 computational graph를 생성(메모리 잠식)

```python
total_loss = 0

for i in range(10000):
    optimizer.zero_grad()
    output = model(input)
    loss = criterion(output)
    loss.backward()
    optimizer.step()
    total_loss += loss
```

1-d tensor의 경우 python 기본 객체로 변환하여 처리할 것

```python
total_loss = 0

for x in range(10):
    #asuume loss is computed
    iter_loss = torch.randn(3,4).mean()
    iter_loss.requires_grad = True
    
    #total_loss += iter_loss 대신
    
    total_loss += iter_loss.item
    
    #또는
    
    total_loss += float(iter_loss)
```

**4. del 명령어를 적절히 사용하기**

* 필요가 없어진 변수는 적절한 삭제가 필요함

* python의 메모리 배치 특성상 loop이 끝나도 메모리를 차지함

```python
#아래들처럼 코드를 작성하면 메모리가 남으니 적절한 시점에 del 사용하기

for x in range(10):
    i = x
print(i) # 9 is printed

for i in range(5):
    intermediate = f(input[i])
    result += g(intermediate)
output = h(result)
return output
```

**5. 가능 batch 사이즈 실험해보기**

학습시 OOM이 발생했다면 batch 사이즈를 1로 해서 실험해보기

```python
oom = False
try:
    run_model(batch_size)
except RuntimeError: #Out of memory
    oom = True

if oom:
    for _ in range(batch_size):
        run(model(1))
```

**6. torch.no_grad() 사용하기**

* Inference 시점에서는 torch.no_grad() 구문을 사용

* backward pass 으로 인해 쌓이는 메모리에서 자유로움

```python
with torch.no_grad():
    for data, target in test_loader:
        output = network(data)
        test_loss += F.nll_loss(output, target, size_average = False).item()
        pred = output.data.max(1, keepdim = True)[1]
        correct += pred.eq(target.data.view_as(pred)).sum()
```

## 예상치 못한 에러 메시지

OOM 말고도 유사한 에러들이 발생

* CUDNN_STATUS_NOT_INIT 이나 device-side-assert 등

* 해당 에러도 cuda와 관련하여 OOM의 일종으로 생각될 수 있으며, 적절한 코드 처리의 필요함

* colab에서 너무 큰 사이즈는 실행하지 말 것(linear, CNN, LSTM)

* CNN의 대부분의 에러는 크기가 안 맞아서 생기는 경우(torchsummary 등으로 사이즈를 맞출 것)

* tensor의 float precision을 16bit로 줄일 수도 있음

