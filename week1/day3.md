# 5)파이썬으로 데이터 다루기
---
## 5-1)File & Exception & Log handling
---
**exception**

프로그램 사용할 때 일어나는 오류들

* 예상 가능한 예외
사전에 인지 가능

* 예상 불가능한 예외
인터프리터 과정에서 발생하는 예외

**예외 처리(Exception Handling)**

**try~except 문법**

* if문으로 대체 가능

* else 구문 생략 가능
```python
try:
    예외 발생 가능 코드
except <Exception Type>:
    예외 발생시 대응 코드

#생략 가능
else:
    에외 발생하지 않을 때 코드

#생략 가능
finally:
    무조건 실행하는 코드

#예외 발생시 멈추지 않고 이어서 돌아간다는 장점    
```

**raise 구문**

강제적으로 Exception 발셍

**assert 구문**

조건을 만족하지 않았을 경우 예외 발생

**File Handling**

text 파일과 binary 파일 존재

* text 파일 : 메모장으로 열 수 있는, 인간이 이해 가능한 파일 (텍스트 파일, python 코드...)

* binary 파일 : 컴퓨터만 이해 가능 (엑셀파일, 워드 파일...)

**Python File I/O**

```python
#기본
f = open("<파일명>", "접근 모드")
txt = f.read()
print(txt)
f.close

#with 구문
with open("파일명", "접근모드") as f:
    txt = f.read()
    print(txt)
```
**접근모드의 종류**

|접근 모드|설명|
|:---:|:---:|
|r|읽기|
|w|쓰기|
|a|추가|

**list 형태로 한 줄씩 묶음**

```python
with open("파일명", "접근모드") as f:
    txt = f.readlines()
    print(txt)

#writing(접근모드 w,a)을 위해서는 encoding 필요(CP949, utf8...)
```

**Pickle**

파이썬의 객체를 영속화(persistence)하는 built-in 객체
```python
import pickle

f = open(파일, 'wb')
대상 = [데이터]
pickle.dump(대상, f)
f.close()

#pickle.load(f)로 읽기
#pickle은 wb, rb 등으로 읽고 씀
```

**Logging**

정보를 계속 기록

* 유저의 접근, Exception, 특정함수 사용시 등

* Console 출력, 파일화, DB

**logging 모듈**

```python

import logging

logging.debug('출력')
logging.info('출력')
logging.warning('출력')
logging.error('출력')
logging.critical('출력')

```

**logging level**

*프로그램 진행 시점별 logging level

* Deug > Info > Warning > Error > Critical

**configparser**

프로그램 실행 설정을 file에 저장

* dict type
```python
import configparser

config = configparser.ConfigParser()
config.sections
```

**argparser**

Console 창에서 Setting 정보 저장

```python
import argparser

parser = argparse.ArgumentParser(description = '~~')

parser.add_argument(~~)

args = parser.parse_args()
```

**Logging formatter**

Log 결과값을 format

## 5-2)Python data handling
---
**csv**

Comma Separate Value

* 쉼표로 구분된 텍스트 파일

```python
with open('~~.csv') as data:
    ~~
```
```python
import CSV

reader - CSV.reader(f, delimiter = ',', quotechar = '"', quoting = csv.QUOTE_ALL)
```

**Web**

인터넷 공간의 정식 명칭

* 데이터 송수신을 위한 HTTP 프로토콜 사용

* 데이터 표시를 위해 HTML 형식 사용

**HTML**

웹 상의 정보를 구조적으로 표현

* 꺾쇠 괄호로 표현

* 제목, 단락, 링크 등 Tag 사용 

* 트리구조

**정규식(regular expression)**

정규 표현식, 문자 표현 공식

**정규식 기본 문법**

* 문자 클래스 [ ] : [와] 사이의 문자들과 매치
[asd]는 해당 글자에 a, s, d 중 하나 이상 존재

* "-"를 사용해 범위 지정
[a-zA-z]는 모든 알파벳, [0-9]는 모든 숫자

**메타 문자**

정규식 표현에 있어 다른 용도로 사용되는 문자
```
* .(모든 문자) ^(not) $ *(앞의 글자 반복) +(앞의 글자 최소 1회이상 반복) ?(1회 반복) { }(반복 횟수) [ ] \ |(or) ( )
```

**정규식 in 파이썬**

re 모듈 사용

함수 : search, findall

```python
import re
import urllib.request
```

**XML**

eXtensible Markup Language

* 데이터 구조와 설명을 Tag를 사용해 표시

* HTML과 비슷

* 서로 다른 기기간 정보를 주고받기 용이

* beautifulsoup로 parsing

**BeautifulSoup**

HTML, XML 등 Markup 언어 Scraping 도구

```python
#모듈 호출
from bs4 import BeautifulSoup

#객체 생성
soup = BeautifulSoup(books_xml, "lxml")

#Tag 찾는 함수 (find_all, 패턴 반환)
soup.find_all("author")
```

**JSON**

JavaScript Object Notation

* 웹 언어 Java Script의 데이터 객체 표현 방식

* XML의 대체제로 활용

**JSON in Python**

* json 모듈 활용

* dict type과 상호 호환

* 대부분의 사이트에서 활용


# 6)Numpy 기초
---
**numpy**

Numerical Python

* Matrix, Vector과 같은 Array 연산의 표준

* List에 비해 빠르고, 메모리 효율적

* 반복문 없이 배열 처리

**미니콘다 가상환경 생성**

```
conda creat -n numpy_ex python
```

**ndarray**

numpy는 하나의 데이터 type만 배열에 사용 가능

**array 생성**

```python
import numpy as np

t_array = np.array([1,2,3,4], float)
```

**docstring 보는 법**

> shift + Tab

**array creation**

python은 기본적으로 메모리의 주소를 list에 할당하지만 numpy array는 차례대로 바로 할당

* 매우 빠른 속도

* shape : array의 dimension 구성

* dtype : array의 데이터 type

```python
print(t_array.dtype)
print(t_array.shape)
```

**array shape**

|Rank|Name|
|:---:|:---:|
|0|scalar|
|1|vector|
|2|matrix|
|n|n-tensor|

```python
data = [[1,2,3,4], [2,3,4,5], [3,4,5,6]]
a = np.array(data)
a.shape

#result : (3,4)

data = [[[1,2,3,4], [2,3,4,5], [3,4,5,6]], [[112,2,3,4],[2,3,4,5],[3,4,5,6]]]
b = np.array(data)
b.shape

#result : (2,3,4)
```

**Handling Shape**

**reshape**

Array의 shape의 크기를 변경(element 유지)

* -1 : 전체 사이즈를 기반으로 숫자 자동 설정

```python
data_a = np.array([[1,2,3,4],[2,3,4,5]])
print(data_a)

data_b = np.array(data_a).reshape(8,)
print(data_b)

'''
result

[[1 2 3 4]
 [2 3 4 5]]

[1 2 3 4 2 3 4 5]
'''
```

**flatten**

다차원 array를 1차원으로 변환

```python
data_a = np.array([[1,2,3,4],[2,3,4,5]])
print(data_a)

data_b = np.array(data_a).flatten()
print(data_b)

'''
result

[[1 2 3 4]
 [2 3 4 5]]

[1 2 3 4 2 3 4 5]
'''
```

**Indexing**

list와 다르게 [a,b]의 형태로 접근(list는 [a][b])

```python
data_a = np.array([[1,2,3,4],[2,3,4,5]])
print(data_a)

print(data_a[1,2])

'''
result
[[1 2 3 4]
 [2 3 4 5]]

4

'''
```


**Jupyter 셀 생성, 삭제**

> ESC + a : 생성
> ESC + d + d : 삭제

**Slicing**

list와 다르게 행과 열 나눠서 slicing 가능

```python
data_a = np.array([[1,2,3,4],[2,3,4,5]])
print(data_a)

print(data_a[:, 1:]) #row는 모두, column은 1이상

'''
result

[[1 2 3 4]
 [2 3 4 5]]

[[2 3 4]
 [3 4 5]]
'''
```

::a와 같이 사용할 경우 모든 열을 a간격으로 slicing

```python
data_a = np.array([[1,2,3,4],[2,3,4,5]])
print(data_a)

print(data_a[::1, ::2])

'''
result

[[1 2 3 4]
 [2 3 4 5]]

[[1 3]
 [2 4]]
'''
```

**creation function**

**np.arange(a,b,c)**

a부터 b까지 c 만큼의 step을 가지고 생성

**np.zeros(shape = (a,b))**

0으로 가득 찬 (a,b)차원 ndarray

**np.ones_like(array)**

array와 같은 shape의 0으로 가득 찬 array 생성

> zeros = ones로 변환 가능

**np.identity(n = a)**

a차원 단위행렬 array 생성

**np.eye(a,b, k=c)**

c행부터 단위행렬이 시작되는 (a,b)차원 array

**np.diag(array, k=a)**

array의 대각 행렬 값 a행부터 추출

**random sampling**

데이터 분포에 따른 random sample 생성

* np.random.unifom(균등분포)

* np.random.normal(정규분포)

**operation functions**

**array.sum(axis = a)**

array의 a dimension 모든 값을 더해줌

**array.mean()**

평균

**array.std()**

표준편차

**np.vstack((a,b))**

a, b array를 vertical하게 붙여줌 (hstack은 horizontal)

**np.concatenate((a,b), axis = k)**

a, b array를 k 축을 기준으로 붙여줌(0 = v, 1 = h)

**array operation**

* numpy array는 기본적인 사칙연산 제공

* \* 기호를 사용할 경우 element-wise operations(성분곱)

* dot product를 원할 경우 a.dot(b)

**array.transpose()**

전치행렬 생성

**broadcasting**

array + scalar 하면 모든 element에 scalar를 더해줌(곱셈가능)

* 차원 다른 array면 차원을 자동으로 채워줌

**comparisons**

Array의 데이터 조건 판별

```python
a = np.arange(10)
print(a)

print(np.any(a>5))

print(np.all(a>1))

'''
result

[0 1 2 3 4 5 6 7 8 9]
True
False
'''
```

**배열간 대소비교시 element끼리 비교**

**np.where**

```python
a = np.arange(10)
print(a)

np.where(a>3, 1, 0)

'''
result

[0 1 2 3 4 5 6 7 8 9]
array([0, 0, 0, 0, 1, 1, 1, 1, 1, 1])
'''
```

**argmax & argmin**

array내 최대, 최소 반환

```python
array.argsort()
#작은 순서대로 index를 반환하는 함수

np.argmax(array) 

np.argmin(array, axis = a)
#a축을 기준으로 각 축의 argmin값을 배열 형태로 반환
```

**boolean index**

특정 조건에 따른 값을 뽑아냄

```python
a = np.arange(10)
print(a)

a > 3

'''
result

[0 1 2 3 4 5 6 7 8 9]
array([False, False, False, False,  True,  True, True,  True,  True, True])
'''
```

**아래와 같이 활용 가능**

```python
a = np.arange(10)
print(a)

a[a > 3]

'''
result

[0 1 2 3 4 5 6 7 8 9]
array([4, 5, 6, 7, 8, 9])
'''
```

**fancy index**

a[b]와 같이 작성하면 b의 element의 index 해당하는 a의 값 뽑아줌

```python
a = np.array([10,20,30,40,50])
b = np.array([1,3,0,2,4,3,1])

a[b]

'''
result

array([20, 40, 10, 30, 50, 40, 20])
'''
```

# 7)Pandas 기초
---
## 7-1) Pandas 1
---

**pandas**

구조화된 데이터 처리 라이브러리

* panel data

**DataFrame**

Data Table 전체 Object

**series**

DataFrame 중 하나의 Column의 모음 Object

index를 통해 접근

**pandas function**

```python
df.values
#값 리스트만

df.index
#인덱스 리스트만

df.loc[인덱스 값]
#인덱스 값으로 해당 행 검색

df.iloc[숫자]
#인덱스 숫자로 해당 행 

df.map(lambda x : x**2)
#함수적용
```

**replace, map, drop 사용시 inplace = True해야 실제로 바뀜**

## 7-2)Pandas 2
---

**Groupby**

```python
df.groupby("기준 column")['추출 column'].sum()

#위와 같이 사용
#여러개의 column도 묶을 수 있음
```

**Hierarchical index**

2개 이상의 column으로 groupby할 경우 index가 2계층 생성

* unstack하면 테이블로 변경

**Merge**

기준에 따라 병합

* Inner Join (동시에 같은 값)

* Left Join (왼쪽 기준)

* Right Join (오른쪽 기준)

* FUll Join (모두 합침)

