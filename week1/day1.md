# 1) 파이썬 AI 개발환경 준비
## 1-1) Basic computer class for newbies
---
**컴퓨팅OS**

* 컴퓨터를 동작하기 위한 기반

* 프로그램은 기본적으로 Windows용 / Mac OS용 등 나누어져 있기 때문에 운영체제에 맞춰 다운로드해야 함

* *Python의 경우 운영체제에 독립적이기 때문에 별도 설치 x

**File System**

* os에서 파일을 저장하는 트리구조 저장체계

**파일의 기본체계**

* 디렉토리 : 폴더

* 파일 : 컴퓨터에서 정보를 저장하는 논리적인 단위(파일명.확장자)

**터미널**
* 마우스가 아닌 키보드로 명령을 입력하는 환경
* Command Line Interface(CLI환경)
* Windows - CMD window, Windows Terminal
* Mac, Linux - Terminal
* Console = Terminal = CMD

**유용한 미니콘다 명령어**
* **mkdir workspace** (workspace라는 directory를 현재 위치에 만들어라)
* **cd workspace** (현재 위치를 workspace directory로 옮겨라)
* **..\abc.docx** (한 칸 이전 directory의 abc.docx 파일을 열어라)
* **copy ..\\..\abc.docx .\\** (2칸 이전 directory의 abc.docx파일을 현재 위치로 복사해라)

## 1-2) Python Overview
---
**Python**
* 플랫폼 독립적
* 인터프리터 언어
* 객체지향적 언어
* 동적 타이핑 언어

## 1-3) Python 코딩환경
---
1) 운영체제

    windows vs Linux vs Mac OS

2) Python Interpreter

    Python 기본 interpreter vs Anaconda(미니콘다)

3) 코드 편집기(editor)

    메모장, VI editor, Sublime Text, Atom, VS Code, PyCharm...
    
    부스트캠프 기간동안 사용할 코드 편집기

    * 설치된 어플리케이션 : visual studio code
    * 웹기반 인터랙티브 편집기 : jupyter, colab    



# 2) 파이썬 기초 문법
## 2-1) Variables
---

**Variable & Memory**

**Variable**
* 가장 기초적인 프로그래밍 문법 개념
* 데이터(값)을 저장하기 위한 메모리 공간의 프로그래밍상 이름
    
변수에 들어가는 값은 메모리 주소에 할당된다.(주로 DRAM에 저장)

**Basic Operation**
* 기본자료형(primitive data type)
* 연산자와 피연산자
* 데이터 형변환

**기본자료형**

|유형|설명|예시|선언 형태|
|---|---|---|---|
|integer|양/음의 정수|1,-2,3|data = 1|
|float|소수점이 포함된 실수|10.2, -9.0|data = 9.0|
|string|따옴표("/")에 들어가 있는 문자형|abc, a20abc|data = 'abc'|
|boolean|참 또는 거짓|True, False|data = True|


## 2-2) Fuction & Console IO(In/Out)
---

**함수**
* 어떤 일을 수행하는 코드의 덩어리
* 반복적인 수행을 1회만 작성 후 호출
* 코드를 논리적인 단위로 분리
* 캡슐화 : 인터페이스만 알면 타인의 코드 사용가능
* Indentation(들여쓰기) : 4칸 space


**VS Code 들어가는 루트**
```
winodws -> miniconda -> cd workspace -> code . 
```

**jupyter notebook 들어가는 루트**
```
windows -> miniconda -> cd workspace -> jupyter notebook
```

**파이썬 포매팅**

```python
#formatting_example_1.py

def function(x):
    return 3*x + 7

print(function(2))

'''
parameter : x, 함수의 입력 값 인터페이스
argument : 2, 실제 parameter에 대입된 값
'''

```
**miniconda에서 파이썬 파일 열기**

```
cd workspace로 이동 -> python formatting_example_1.py 입력
```

**포매팅 종류**

1) %string

```python
date = '3월 2일'
print('today is %s' %(date))
```
%f = 실수

%s = 문자열

%d = 정수

2) format 함수
```python
date = '3월 2일'
print('today is {0}'.format(date))
```
3) f string
* PEP498에 근거한 formatting 기법
```python
date = '3월 2일'
print(f'today is {date}')
```

**미니콘다로 python 파일 만들기**
```
1) cd workspace를 입력해서 workspace 디렉토리로 이동
2) code (파일이름).py를 눌러 VS Code 켜지면서 해당 파일이름을 가진 파이썬 파일 생성
3) 실행 시 python (파일이름).py를 입력하면 바로 해당파일 실행
```
## 2-3) Conditionals & Loops
---
### **조건문 & 반복문**

**Condition**

* 조건에 따라 특정한 동작을 하게 하는 명령어

* 조건문은 ‘조건을 나타내는 기준’과 ‘실행해야 할 명령’으로 구성됨

* 조건의 참, 거짓에 따라 실행해야 할 명령이 수행되거나 되지 않음

* 파이썬은 조건문으로 if, else, elif 등의 예약어를 사용함

**VS Code 사용법**

> VS Code에서 ctrl+shift+p를 누르면 터미널창 실행 가능
>(Python: Run python file in terminal 누르면 실행)

**삼항 연산자(Ternary operators)**

* 조건문을 사용하여 참일 경우와 거짓일 경우의 결과를 한줄로 표현
```python
value = 12
Is_even = True if value %2 == 0 else False
```

**반복문**

* 정해진 동작을 반복적으로 수행하게 하는 명령문
* 반복문은 ‘반복 시작 조건’, ‘종료 조건’, ‘수행 명령’으로 구성됨
* For, while 예약어 사용

**디버깅**

* 코드의 오류를 발견하여 수정하는 과정

* 문법적 에러를 찾기 위한 에러 메시지 분석

* 논리적 에러를 찾기 위한 테스트

* 논리적 에러 – 뜻대로 실행이 안되는 코드

## 2-4) String and advanced function concept
---
**문자열**

* 시퀀스 자료형으로 문자형 data를 메모리에 저장

* 영문자 한 글자는 1byte의 메모리공간을 사용

* 1byte = 8bit = 2^8 = 256까지 저장 가능

* 데이터 타입은 메모리의 효율적 활용을 위해 매우 중요

##### txt파일 오픈 방법

```python
f = open(“lyrics.txt”, ‘r’)
lyric = ‘’
while True:
    line = f.readline()
    if not line:
        break
    lyric = lyric + line.trip() + ‘\n’
f.close()

n_of_lyric = lyric.upper().count(‘ABC”) #대소문자 구분 제거
print(‘Number of a word ‘ABC’, n_of_lyric)
```

**파이썬에서 주석처리 빨리 하는 법**
> Ctrl + / 누르면 바로 주석 달림

### **Function**
**Call by object reference**

함수에서 parameter를 전달하는 방식

1)	값에 의한 호출(call by value)
* 함수에 인자를 넘길 때, 값만 넘김.

* 호출자에게 영향 x


2)	참조에 의한 호출(call by reference)
* 함수에 인자를 넘길 때, 메모리 주소를 넘김

* 함수 내 인자값 변경 시, 호출자의 값도 변경


3)	객체 참조에 의한 호출(call by object reference)
* 파이썬의 방식

* 객체의 주소가 함수로 전달되는 방식

* 영향을 기본적으로 주지만 새로운 객체를 생성시 분리됨


**Swap**

* 함수를 통해 변수간의 값을 교환할 때, 실제 값의 변환이 일어나는지

* Function 내에서 새롭게 들어온 값을 복사해서 사용하는 것이 좋음


**Scoping Rule**
* 변수가 사용되는 범위

* 지역변수(local variable) : 함수 내에서만 사용

* 전역변수(global variable) : 프로그램 전체에서 사용

**재귀함수(Recursive function)**

* 자기자신을 호출하는 함수

* 종료조건 존재, 종료 조건까지 함수호출 반복

**Function type hints**

* 파이썬의 가장 큰 특징 – dynamic typing
-> 처음 함수를 사용할 때 사용자가 interface를 알기 어려움

* PEP484에 기반해 type hints 기능 제공

**사용법**
```python
def func(var:var_type) -> return_type:
    pass
def calculate(var:int) -> int:
    return var+1
```
**Function docstring**

* 파이썬 함수에 대한 상세 새뇽을 사전에 작성

* 세개의 따옴표로 docstring 영역 표시

**사용법**

> Ctrl + shift + p 누르고 docstring 검색해서 누르면 바로 해당 함수의 파라미터에 따라 docstring 초안 생성됨

**함수 작성 가이드라인**

* 함수는 가능한 짧게

* 함수 이름은 역할,의도가 명확하게

* 하나의 함수에는 유사한 역할을 하는 코드만 작성

* 인자로 받은 값 자체를 바꾸지 말 것(임시변수 선언)

* 복잡한 조건, 수식은 함수로 작성

**코딩 컨벤션**

사람이 이해할 수 있게 코드를 짜는 규칙
* 구글 python convention

* 중요한 건 일관성

* 읽기 좋은 코드가 좋은 코드

* 들여쓰기는 Tab보다 4Space를 권장하며 일관성 가져야됨

* 한 줄은 최대 79자까지

* 불필요한 공백 제거

* 연산자는 1칸 이상 안 띄운다

* 주석 갱신, 불필요한 주석 삭제

* 코드 마지막에는 항상 한 줄 추가

* 소문자I, 대문자O, 대문자 I 금지

* 함수명은 소문자로 구성, 필요 시 밑줄 사용

* flake8 모듈로 체크할 것(PEP8근거)

**실행**

```
conda install flake8
flake8 (파일명).py
#눌러보면 모듈 검사 가능
```

최근에는 black 모듈을 활용하여 pep8 like수준으로 자동 수정
>conda install black
black (파일명).py

