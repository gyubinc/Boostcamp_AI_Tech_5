# 4) Convolutional Neural Networks
---

**Convolution**

(f*g)(t)

(I*K)(i,j)

* Continuous convolution

* Discrete convolution

* 2D image convolution<br/>filter와 image의 곱연산

**Convolutional Neural Networks**

CNN consists of convolution layer, pooling layer, and fully connected layer.

* Convolution and pooling layers: feature extraction

* Fully connected layer: decision making(e.g., classification)

**Stride**

Convolution filter가 한 번에 움직이는 보폭

**Padding**

Input과 Output의 dimension을 고려하기 위해 빈 공간을 채워주는 행위

## Convolution Arithmetic

**parameter의 수는 Kernel의 dimension에만 영향을 받는다**

Padding(1), Stride(1), 3 x 3 Kernel을 사용,

* Input dimension: (W:40, H:50, C:128)

* Output dimension: (W:40, H:50, C:64)

**필요한 parameters 수는?**

3 x 3 x 128개의 Kernel이 64개 필요

3 x 3 x 128 x 64 = 73,728개의 parameters

* fully connected layer(Dense layer)는 너무 많은 파라미터를 생성하므로 폭을 줄이고 깊이를 늘리는 방향으로 모델 설정

**1x1 Convolution**

* Dimension(channel) reduction

* reduce the number of parameters while increasing the depth

* e.g., bottleneck architecture

# 5) Modern Convolutional Neural Networks
---

**ILSVRC**(ImageNet Large-Scale Visual Recognition Challenge)

* Classification / Detection / Localization / Segmentation

* 1,00 different categories

* Over 1 million images

* Training set: 456,567 images

**AlexNet**

5 convolutional layers & 3 dense layers (total 8 layers)

**Key ideas**

* Rectified Linear Unit(ReLU) activation

* GPI implementations(2 GPUs)

* Local response normalization, Overlapping pooling

* Data augmentation

* Dropout

**RELU**

* Preserves properties of linear models

* Easy to optimize with gradient descent

* Good generalization

* Overcome the vanishing gradieint problem

**VGGNet**

* 3x3 convolution filters(with stride 1)만을 사용

* 1x1 convolution for fully connected layers

* Dropout

**Why 3x3 convolution?**

Receptive field : 입력의 special dimensions

* 3x3 convolution을 2번 거치면 5x5의 Receptive field를 거친 것

* 128 channel에 3x3 convolution layer 2개 사용할 때 # of parameters: 3x3x128x128x2 = 294,912

* 5x5의 convolution layer 1개 사용할 때 # of parameters: 5x5x128x128 = 409,600

**GooLeNet**

22 layers, 비슷한 구조가 반복되는 network in network(NiN) 구조

**Inception blocks**

하나의 Input에 대해 여러개의 receptive field를 갖는 layer로 나누고 다시 concatenation

* Reduce the number of parameter

* Recall how the number of parameters is computed

* 1x1 convolution can be seen as channel-wise dimension reduction

**Benefit of 1x1 convolution**

128 channel에 3x3 convolution을 적용해 128 channel로 다시 만들 때

* 1x1 convolution을 통해 32channel로 변환 후 3x3 convolution을 적용해 다시 128channel로 변환: 1x1x128x32 + 3x3x32x128 = 40,960

* 바로 3x3 convolution 적용: 3x3x128x128 = 147,456

**# of parameters**

1. AlexNet(8-layers): 60M

2. VGGNet(19-layers): 110M

3. GoogLeNet(22-layers): 4M

**ResNet**

Deeper neural networks are hard to train.

* Overfitting is usually caused by an excessive number of parameters.

* But, not in this case.

* Add an identity map(skip connection)

* f(x) <- x + f(x)

Simple shortcut vs Projected Shortcut

**Bottleneck architecture**

3x3 convolution 하기 전에 1x1 convolution로 input channel을 줄이고 1x1 convolution을 통해 다시 input channel의 차원과 맞춤

**DenseNet**

uses concatenation instead of addition

**Dense Block**

* Each layer concatenates the feature maps of all preceding layers.

* The number of channels increases geometrically

**Transition Block**

* BatchNorm -> 1x1 Conv -> 2x2 AvgPooling

* Dimension reduction

## Summary

**Key takeaways**

* VGG: repeated 3x3 blocks

* GoogLeNet: 1x1 convolution

* ResNet: skip-connection

* DenseNet: concatenation

# 6) Computer Vision Applications
---

## Semantic Segmentation

주어진 image를 pixel마다 분류하는 것

**Fully Convolutional Network**

* ordinary CNN에서 dense layer를 제거

* Number of parameters는 동일

* This process is called convolutionalization

* Transforming fully connected layers into convolution layers enables a classification net to output a heat map

**Deconvolution(conv transpose)**

convolution의 역연산을 통해 special dimension을 키워줌

* 엄밀히 역연산은 아니지만 padding을 주어 마치 거꾸로 연산하는 듯하게 표현

## Detection

**R-CNN**

input image 내에서 random 하게 2000개의 region을 뽑은 후 input dimension에 맞춰 SVM으로 classify

**SPPNet**

idea: R-CNN이 CNN을 2000번 돌려야하니 시간상 한번만 돌려보자

* 전체 image를 넣어서 bounding box에 해당하는 sub-tensor를 뜯어서 활용

**Fast R-CNN**

neural network를 통해 bounding box를 움직임

**Faster R-CNN**

Bounding box를 뽑는 방식을 random이 아닌 학습을 통해 정하자

* Region Proposal Network + Fast R-CNN

**Region Proposal Network**

* anchor box = 미리 정해놓은 box의 크기

* 9: Three different region sizes(128, 256, 512) with three different ratios(1:1, 1:2, 2:1)

* 4: four bounding box regressiong parameters

* 2: box classification (whether to use it or not)

9*(4+2) 채널 사용

**YOLO**

extremely fast object detection algorithm

* It simultaneously predicts multiple bounding boxes and class probabilities

* SxSx(B*5 + C) size

* SxS: number of cells of the grid

* B*5: B bounding boxes with offsets(x,y,w,h) and confidence

* C: Number of classes



