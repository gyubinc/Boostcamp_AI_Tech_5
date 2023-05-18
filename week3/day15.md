# Viz 1) Welcome to Visualization
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