# 1) Welcome to Visualization
---

## 데이터 시각화

데이터를 그래픽 요소로 매핑하여 시각적으로 표현하는 것

* 목적

* 독자

* 데이터

* 스토리

* 방법

* 디자인

## 시각화의 요소 상태

**데이터 시각화**

데이터 시각화를 위해 데이터가 우선적 필요

시각화를 진행할 데이터

* 데이터셋 관점(global)

* 개별 데이터의 관점(global)

**데이터셋의 종류**

* 정형 데이터

테이블 형태, csv, tsv 파일로 제공, 가장 많이 제공

* 시계열 데이터

시간 흐름에 따른 데이터, 기온, 주가, 등 정형데이터와 음성, 비디오와 같은 비정형 데이터 존재

시간 흐름에 따른 추세, 계절성, 주기성 등을 살핌

* 지리 데이터

지도 정보와 보고자 하는 정보 간의 조화 중요 + 지도 정보를 단순화 시키는 경우도 존재

거리, 경로, 분포 등 다양한 실사용

* 관계형 데이터

객체와 객체 간의 관계를 시각화

객체는 Node로, 관계는 Link로

크기, 색, 수 등으로 객체와 관계의 가중치 표현

휴리스틱하게 노드 배치

* 계층적 데이터

포함관계가 분명한 데이터

Tree, Treemap, Sunburst

* 다양한 비정형 데이터

데이터의 종류는 다양하게 분류 가능

**수치형(numerical)**

연속형(continuous), 이산형(discrete)로 분류

**범주형(categorical)**

명목형(nominal), 순서형(ordinal)로 분류

## 시각화 이해하기

점,선,면에서 시작하는 시각화

A **mark**is a basic graphical element in an image

* 점, 선, 면으로 이루어진 데이터 시각화

A visual **channel**is a way to control the appearance of marks, independent of the dimensionality of the geometric primitive.

* 각 마크를 변경할 수 있는 요소들

**전주의적 속성**

Pre-attentive Attribute

주의를 주지 않아도 인지하게 되는 요소

* 시각적으로 다양한 전주의적 속성이 존재

동시에 사용하면 인지하기 어려움

* 적절하게 사용할 때, 시각적 분리(visual pop-out)

# 2) 기본적인 차트의 사용
---

## Bar plot

직사각형 막대를 사용하여 데이터의 값을 표현하는 차트/그래프

* 막대 그래프, bar chart, bar graph 등의 이름으로 사용됨

* 범주(category)에 따른 수치 값을 비교하기에 적합한 방법

방향에 따른 분류

* vertical: x축에 범주, y축에 값을 표기(.bar())

* horizontal: y축에 범주, x축에 값을 표기(.barh())

**stacked bar plot**

2개 이상의 그룹을 쌓아서 표현

* .bar()에서는 bottom 파라미터 사용

* .barh()에서는 left 파라미터 사용

* sharey = True로 설정하면 y축 맞춰줄 수 있음 (set_ylim으로 설정도 가능)

**percentage stacked bar chart에 비율을 주석으로 달면 더 표현이 좋다**

**Overlapped Bar Plot**

겹쳐서 만드는 방식

* 비교가 쉬움

* 투명도를 조정하는 파라미터 alpha 조정

* bar plot보다는 Area plot에서 더 효과적

**Grouped Bar Plot**

그룹별 범주에 따른 bar를 이웃되게 배치

Matplotlib으로는 비교적 구현이 까다로움(width/2 만큼 좌우로 분리)

* 적당한 테크닉(.set_xticks(), .set_xticklabels())

* 그룹이 5개~7개 이하일 때 효과적(많다면 ETC로 처리)

**Principle of Proportion Ink**

실제 값과 그에 표현되는 그래픽으로 표현되는 잉크 양은 비례해야 한다

* 반드시 x축의 시작은 zero(차이는 plot의 세로 비율로 표현)

## 데이터 정렬하기

정확한 정보를 위해 정렬이 필수

* Pandas에서는 sort_values(), sort_index()를 사용해 정렬

기준에 따라

* 시계열 : 시간순

* 수치형 : 크기순

* 순서형 : 범주의 순서대로

* 명목형 : 범주의 값 따라 정렬

여러 기준으로 정렬을 하여 패턴을 발견

대시보드에서는 Interactive로 제공하는 것이 유용

## 적절한 공간 활용

여백과 공간만 조정해도 가독성이 높아진다

**techniques**

* X/Y axis Limit(.set_xlim(), .set_ylim())

* Spines(.spines[spine].set_visible())

* Gap(width)

* Legend(.legend())

* Margins(.margins())

## 복잡함과 단순함

필요없는 복잡함 No

정확한 차이(EDA)

큰 틀에서 비교 및 추세 파악(Dashboard)

축과 디테일 등의 복잡함

* Grid(.grid())

* Ticklabels(.set_ticklabels()) Majot & Minor

* Text의 위치(.text() or .annotate()) middle & upper

## ETC

오차 막대를 추가하여 Uncertainty 정보 추가(errorbar)

Bar 사이 Gap이 0이라면 히스토그램 사용(.hist())

다양한 Text 정보 활용

* 제목(.set_title())

* 라벨(.set_xlabel(), .set_ylabel())


## Line Plot

연속적으로 변화하는 값을 순서대로 점으로 나타내고, 이를 선으로 연결한 그래프

* 꺾은선 그래프, 선 그래프, line chart, line graph 등의 이름으로 사용

* 시간/순서에 대한 변화에 적합(시계열 분석 특화)

* .line이 아니라 .plot()으로 표현

5개 이하의 선 사용 추천

**구별요소**

* 색상(color)

* 마커(marker, markersize)

* 선의 종류(linestyle, linewidth)

**전처리**

Noise의 인지적인 방해를 줄이기 위해 smoothing을 사용

**추세에 집중**

* 꼭 축을 0에 초점을 둘 필요는 없음

* 너무 구체적인 line plot보다 생략된 line plot이 더 나을 수 있다.( Grid, Annotate등 제거)

* 생략되지 않는 선에서 범위를 조정하여 변화율 관찰(.set_ylim())

**간격**

규칙적인 간격이 아니라면 오해를 줄 수 있다!

* 그래프 상 규칙적일때: 기울기 정보의 오해

* 간격이 다를 때: 없는 데이터에 대해 있다고 오해

규칙적인 간격의 데이터가 아니라면 관측 값에 점으로 표시하여 오해를 줄이자

**보간**

Line은 점을 이어 만드는 요소 -> 점과 점 사이에 데이터가 없기에 이를 잇는 방법(보간)

error나 nois가 포함되어 있는 경우, 데이터의 이해를 도움

* Moving Average

* Smooth Curve with Scipy

* scipy.interpolate.make_interp_spline, scipy.interpolate.interp1d, scipy.ndimage.gaussian_filter1d

**Presentation에는 좋은 방법일 수 있으나**

* 없는 데이터 있다고 볼 수 있음

* 작은 차이를 없앨 수 있음

* 일반적인 분석에서는 지양

**이중 축 사용**

한 plot에 대해 2개의 축을 이중 축(dual axis)라고 함

같은 시간 축에 대해 서로 다른 종류의 데이터를 표현

* .twinx() 사용

한 데이터에 대해 다른 단위

* .secondary_xaxis(), .secondary_yaxis() 사용

2개의 plot을 그리는 것 >>> 이중 축 사용

* 이중 축은 지양

## Scatter Plot

점을 사용하여 두 feature간의 관계를 알기 위해 사용하는 그래프

* 산점도 등의 이름으로 사용

* .scatter()를 사용

**요소**

* 색(color)

* 모양(marker)

* 크기(size)

**목적**

상관관계 확인(양/ 음/ 없음)

**Overplotting**

점이 많아질수록 점의 분포를 파악하기 힘듦

* 투명도 조정

* 지터링(jittering): 점 위치를 약간씩 변경

* 2차원 히스토그램: 히트맵을 사용해 깔끔한 시각화

* Contour plot: 분포를 등고선으로 표현

**색**

연속은 gradient, 이산은 개별 색상으로

**마커**

구별이 힘듦 + 크기가 고르지 않다

**크기**

버블차트(bubble chart)라고 부름

구별하기는 쉽지만 오용하기도 쉽다

**인과관계와 상관관계**

인과관계는 항상 사전 정보와 함께 가정으로 제시할 것

**추세선**

추세선 2개 이상은 가독성이 떨어짐

**ETC**

* grid 지양, 색은 무채색으로

* 범주형이 있다면 heatmap 도는 bubble chart 추천