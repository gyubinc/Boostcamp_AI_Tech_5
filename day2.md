# 3)파이썬 기초문법 2
---
## 3-1) Python Data Structure
---

**파이썬 기본 데이터 구조**
* 스택과 큐(stack & queue with list)

* 튜플과 집합(tuple & set)

* 사전(dictionary)

* Collection모듈

**스택**

* 나중에 넣은 데이터를 먼저 반환(LIFO)

* 입력을 Push, 출력을 Pop이라고 함

**큐**
* 먼저 넣은 데이터를 먼저 반환(FIFO)

* Stack과 반대

**튜플**

* 값의 변경이 불가능한 리스트

* 리스트의 연산, 인덱싱, 슬라이싱 등을 동일하게 사용

* 프로그램 작동 동안 변경되지 않는 데이터의 저장

**Set**

* 값을 순서없이 저장, 중복 불허

**Dictionary**

* 데이터 저장 시 구분지을 값과 함께 저장

* 구분을 위한 데이터 고유 값을 Identifier 도는 Key라고 함

* Key 값을 활용하여, 데이터 값(Value)를 관리

* 다른 언어에서는 Hash Table이라는 용어 사용

**Collections**


* List, Tuple, Dict에 대한 Python Built-in 확장 자료 구조(모듈)

* deque, Counter, OrderedDict, defaultdict, namedtuple 등의 모듈 존재

* 빠른 속도

**가상환경 생성**
> Conda create -n gyubin python

**가상환경 활성화**
> Conda activate gyubin

## 3-2) Pythonic code
---
**Pythonic code**

* 파이썬 스타일의 코딩 기법

* 파이썬 특유의 문법, 효율적 코드

* 남 코드에 대한 이해도

* for, loop, append보다 list가 조금 더 빠르다.

* 간지

### 종류
**1)split & join**

String type의 값을 ‘기준값’으로 나눠서 List형태로 변환
```python
text = ‘hello I’m gyubin’.split()
print(text)
#reulst : [‘hello’, ‘I’m’, ‘gyubin’]
```

**2)list comprehension**

기존 List 사용하여 간단히 다른 List 만드는 기법
* 파이썬에서 가장 많이 사용

* for + append보다 빠르다

```python
#원래 방식
result = []
for i in range(10):
    result.append(i)
    
#comprehension
result = [i for i in range(10)]
```

이러한 방식도 가능
```python
#원래 방식
A = ‘abc’
B = ‘def’
result = []
for i in A:
    For j in B:
        result.append(i+j)

#comprehension
A = ‘abc’
B = ‘def’
result = [i+j for i in A for j in B]
#result : [‘ad’, ‘ae’, ‘af’, ‘be’, ‘be’…….
```
+뒤에 if문 넣으면 filter역할 가능

**3)enumerate & zip**

**Enumerate**

list의 element를 추출할 때 번호를 붙여서 추출
```python
For i, v in enumerate([‘a’, ‘b’, ‘c’]):
Print(i, v)
#i = index, v = value
```
**Zip**

두 개의 list의 값을 병적으로 추출
```python
A = [‘a’, ‘b’, ‘c’]
B = [‘d’, ‘e’, ‘f’]

[c for c in zip(A,B)]
#[(‘a’, ‘d’), (‘b’, ‘e’), (‘c’, ‘f’)]
```

**4)lambda & map & reduce**

**Lambda**

함수 이름 없이, 함수처럼 쓸 수 있는 익명함수

* 요즘은 권장하지는 않으나 많이 씀 (해석, 테스트가 어려움)
* 
```python
f = lambda x,y : x+y
f(10,50)

#다른 방식
(lambda x,y : x+y)(10,50)
```

**Map**

두 개 이상의 list에도 적용 가능함, if filter도 사용 가능
```python
A = [1,2,3]
f = lambda x,y : x+y
print(list(map(f, A, A)

#result : 2 4 6
```
**Reduce**
```python
from functools import reduce
print(reduce(lambda x, y : x+y, [1,2,3,4,5]

#과정 : 3, 6, 10, 15 출력 : 15
```

**5)generator**

큰 데이터를 처리할 때 generator expression을 고려
파일 데이터 처리 시 권장

**Iterable object**

내부적 구현으로 __iter__ 와 __next__ 사용
```python
A = [1,2,3,4,5]
Next_text = iter(A)
next(Next_text)

#하나씩 밖으로 나옴
#yield를 통해 제네레이터를 만들면 필요할 때마다 호출해 메모리 효율적 활용 가능
```
**Generator comprehension**

```python
list_gen = (I * I for I in range(500))
#list(list_gen)
#for i in List_gen과 같이 활용
```
**6)function passing arguments**

**keyword arguments**

함수에 입력되는 parameter의 변수명을 사용
```python
def func(a,b):
    pass
func(b = ‘hi’, a = ‘bye’)
#위와 같이 넣으면 a, b를 각각 찾아서 들어감
```

**default arguments**

parameter의 기본값을 사용, 입력하지 않아도 기본값 출력
```python
def func(a, b = ‘bye’):
    pass
func(‘hi’)
#위와 같이 넣으면 b를 넣지 않아도 b 값에 ‘bye’ 입력
```

**variable-length arguments(가변 인자)**

Asterisk(*) 기호를 사용해 parameter 표시

* 가변인자는 오직 한 개만

* args 변수명 주로 사용

* tuple 형태로 저장

```python
def asterisk_func(a, b, *args):
	print(a, b, sum(args)

asterisk_func(1,2,3,4,5)
```

 **keyword variable-length(키워드 가변인자)**
 
asterisk(*) 2개 사용해서 표시

* dict type으로 사용

```python
def func(**kwargs):
    print(kwargs)

func(a = 1, b = 2, c = 3)

#result : {‘a’ = 1, ‘b’ = 2, ‘c’ = 3}
```

**asterisk-unpacking a container**

tuple, dict 등 자료형의 값을 unpacking해서 입력

* zip 과 활용하면 강력
```python
func(1,*(2,3,4,5,6))

#func(1,2,3,4,5,6)으로 처리됨
```
```python
A = ([1,2], [3,4], [5,6], [7,8])
for x in zip(*A):
    print(x)

#result : (1,3,5,7) (2,4,6,8)
```

# 4) 파이썬 객체 지향 프로그래밍
---
## 4-1) Python Object Oriented Programming
---
**OOP**
* 객체 : ‘속성(Attribute)’와 ‘행동(Action)’을 가짐

* 속성 = 변수(variable), 행동 = 함수(method)

**예시**
```python
class Player(object):
    def __init__(self, name, position, back_number):
        self.name = name
        self.position = position
        self.back_number = back_number
    
    def change_back_number(self, new_number):
        print(f'선수의 등번호를 변경합니다 : From {self.back_number} to {new_number}')
        self.back_number = new_number

if __name__ == "__main__":
    gyubin = Player('gyubinc', 'striker', 13)

    print(gyubin.back_number)
    print('-'*30)
    gyubin.change_back_number(20)
    print('-'*30)
    print(gyubin.back_number)
```
**Python naming rule**
변수,함수명 짓는 방식
* snake_cas : 띄어쓰기 부분에 ‘_’를 추가해 뱀처럼 표현, 파이썬 함수, 변수명

* CamelCase: 띄어쓰기 부분에 대문자를 사용해 낙타의 등처럼 표현, 파이썬 Class명

**매직 메소드**

**\_\_init__**
* 객체에 대한 정보 선언

**\_\_str__**
* print문 사용 시 return의 값이 출력됨

**\_\_add__**
* 두 인스턴스를 더할 시 동작
```python
class Player(object):
    def __init__(self, name, position, back_number):
        self.name = name
	    self.position = position
	    self.back_number = back_number
    def __str__(self):
	    return ‘this is player’
    def __add__(self,other):
	    return self.name + other.name
```

**주의점**
* method(Action) 추가시 반드시 self를 추가해야 한다.

* Self = 생성된 instance 자신

**OOP 특성**
* 객체 지향 언어의 특징 = 실제 세상을 컴퓨터 속에 모델링

* Inheritance(상속), Polymorphism(다형성), Visibility(가시성)

**상속(Inheritance)**

부모클래스의 속성을 자식 클래스가 내려받아서 사용하는 것
```python
class Person(object):
    def __init__(self, name, age):
        pass
class Korean(Person):
    def __init__(self, name, age, gender):
        super().__init__(name, age, gender)
        self.gender = gender
    def about_me(self):
        super().about_me()
        print(“plus alpha”)
```

**다형성(Polymorphism)**

같은 이름 메소드의 내부 로직을 다르게 작성할 때
함수명은 같지만 코드 내부는 조금씩 다른 경우 (도형별 넓이 구하는 공식)

**가시성(Visibility)**

객체의 정보를 볼 수 있는 권한 조절

**캡슐화(Encapsulation) 또는 정보 은닉(Information Hiding)**

* 클래스 간 간섭/정보공유의 최소화

* ‘slef.__변수명’의 형태로 구현(mangling이 일어나 숨겨짐)

* @property를 사용 시 반환 가능

**First – class objects**
* 일급 객체

* 변수나 데이터 구조에 할당 가능한 객체

* 파이썬의 모든 함수는 일급함수

**Inner function**

* 내재함수, 함수 안에 함수를 정의

**데코레이터 function**

* 데코레이터를 쓰면 해당 함수를 데코레이터 함수에 입력된다

* 인자값을 데코레이터 함수에 적어 놓으면 내부 함수에 입력된다

```python
def happy(func):
    def inner(*args):
        print('hi')
        func(*args)
        print('bye')
    return inner

@happy
def printer(txt):
    print(txt)

printer("Im gyubin")
‘’’
result : hi
Im gyubin
Bye
‘’’
```

## 4-2) Module & Project
---
**모듈**

* 어떤 대상의 부분 혹은 조각 

* 패키지

* 모듈을 모아놓은 단위, 하나의 프로그램

* Module == py 파일을 의미

* 같은 폴더에 Module에 해당하는 py있으면 import로 호출 가능

**Namespace**

모듈 호출 범위

* from과 import 키워드를 사용

* 필요한 내용만 골라서 호출

* Alias 설정하기 – 모듈명을 별칭으로 (import ~~ as ~)

* 특정 함수 또는 클래스만 호출 (from ~~ import ~)

* 모듈에서 모든 함수, 클래스 호출 (from ~~ import *)

**Built-in Module**

* 내장함수

**패키지**

코드의 묶음
* 다양한 모듈들의 합, 폴더로 연결

* \_\_init__, \_\_main__ 등의 이름으로 만든다

**패키지 만드는 연습**
```python
'''
miniconda 들어가서 각 폴더, python 파일 만들기
모든 폴더는 __init__.py 폴더를 만든다
Bgm 폴더에다가 아래 함수 작성
'''

def bgm():
    return ‘hi’

'''
Miniconda 실행 - game폴더에서 python 실행 – from sound import bgm – bgm.bgm()
'''
```

**가상환경**

필요한 패키지만 설치하는 환경

* 기본 인터프리터 + 프로젝트 종류별 패키지 설치

* 다양한 패키지 관리도구(virtualenv / conda)

* Virtualenv + pip = 대표적, 레퍼런스 많음

* Conda =설치 용이, Windows 장점


**Miniconda 패키지 설치 방법**
>conda install tqdm
onda install jupyter
