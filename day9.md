# 6)모델 불러오기
---

### fine-tuning 형태로 모델을 만들자

## model. Save()

학습의 결과를 저장하기 위한 함수

* 모델 형태(architecture)와 parameter를 저장

* 모델 학습 중간 과정의 저장을 통해 최선의 결과모델을 선택

* 만들어진 모델을 외부 연구자와 공유하여 학습 재연성 향상

```python
print("Model's state_dict:")
#파라미터 표시
for param_tensor in model.state_dict():
    print(param_tensor, "\t", model.state_dict()[param_tensor].size())

#모델의 파라미터 저장
torch.save(model.state_dict(),
            os.path.join(MODEL_PATH, "model.pt"))

#같은 모델의 형태에서 파라미터만 load
new_model = TheModelClass()
new_model.load_state_dict(torch.load(os.path.join(
    MODEL_PATH, "model.pt")))

# 모델의 architecture와 함께 저장
torch.save(model, os.path.join(MODEL_PATH, "model.pt"))

#모델의 architecture와 함께 load
model = torch.load(os.path.join(MODEL_PATH, "model.pt"))
```

**checkpoints**

학습의 중간 결과를 저장하여 최선의 결과를 선택

* earlystopping 기법 사용시 이전 학습의 결과물을 저장

* loss와 metric 값을 지속적으로 확인 저장

* 일반적으로 epoch, loss, metric을 함께 저장하여 확인

* colab에서 지속적인 학습을 위해 필요

**모델 저장 방식**

```python
torch.save({'epoch': e,
'model_state_dict': model.state_dict(),
'optimizer_state_dict': optimizer.state_dict(),
'loss': epoch_loss,
}, f'saved/checkpoint_model_{e}_{epoch_loss/len(dataloader)}_{epoch_acc/len(dataloader)}.pt')

checkpoint = torch.load(PATH)
model.load_state_dict(checkpoint['model_state_dict'])
optimizer.load_state_dict(checkpoint['optimizer_state_dict'])
epoch = checkpoint['epoch']
loss = checkpoint['loss']
```

## Transfer learning

다른 데이터셋으로 만든 모델을 현재 데이터에 적용

* 일반적으로 대용량 데이터셋으로 만들어진 모델의 성능 증가

* 현재의 DL에서는 가장 일반적인 학습 기법

* backbone architecture가 잘 학습된 모델에서 일부분만 변경하여 학습을 수행함

**Freezing**

pretrained model을 활용시 모델의 일부분을 frozen 시킴

* 번갈아가면저 frozen 시키는 step freezing도 있음

# 7) Monitoring Tools for Pytorch
---

**Tensorboard, weight & biases**

## print문은 그만 쓰자!

## Tensorboard

TensorFlow의 프로젝트로 만들어진 시각화 도구

* 학습 그래프, metric, 학습 결과의 시각화 지원

* PyTorch도 연결 가능 -> DL 시각화 핵심 도구

**저장 항목**

* scalar : metric(Acc, Loss, Precision, Recall ...) 등 상수 값의 연속(epoch)을 표시

* graph : 모델의 computational graph 표시

* histogram: weight 등 값의 분포를 표현

* image : 예측 값과 실제 값을 비교 표시

* Text : 에측 값과 실제 값을 바로 비교

* mesh : 3d 형태의 데이터를 표현하는 도구

```python
#Tensorboard 기록을 위한 directory 생성
import os
logs_base_dir = 'logs'
os.makedirs(logs_base_dir, exist_ok = True)

#기록 생성 객체 SummaryWriter 생성
from torch.utils.tensorboard import SummaryWriter
import numpy as np

#add_scalar 함수 : scalar 값을 기록
#Loss/train : loss category에 train 값
#n_iter : x축의 값
writer = SummaryWriter(logs_base_dir)
for n_iter in range(100):
    writer.add_scalar('Loss/train', np.random.random(), n_iter)
    writer.add_scalar('Loss/test', np.random.random(), n_iter)
    writer.add_scalar('Accuracy/train', np.random.random(), n_iter)
    writer.add_scalar('Accuracy/test', np.random.random(), n_iter)
writer.flush() # 값 기록

#jupyter 상에서 tensorboard 수행
%load_ext tensorboard

#파일 위치 지정(logs_base_dir) 같은 명령어를 콘솔에서도 사용 가능
%tensorboard --logdir{logs_base_dir}
```

## weight & bias (wandb)

머신러닝 실험을 원활히 지원하기 위한 상용도구

* 협업, code versioning, 실혐 결과 기록 등 제공

* MLOps의 대표적인 툴로 저변 확대 중

```python
!pip install wandb -q

#config 설정
config = {'epochs': EPOCHS, 'batch_size': BATCH_SIZE, 'learning_rate': LEARNING_RATE}
wandb.init(project = 'my-test-project', config=config)
#wandb.config.batch_size = BATCH_SIZE
#wandb.config.learning_rate = LEARNING_RATE

for e in range(1, EPOCHS+1):
    epoch_loss = 0
    epoch_acc = 0
    for X_batch, y_batch in train_dataset:
        X_batch, y_batch = X_batch.to(device), y_batch.to(device).type(torch.cuda.FloatTensor)
        #...
        optimizer.step()
        #...

#기록 add_~~~함수와 동일
wandb.log({'accuracy': train_acc, 'loss': train_loss})
```



