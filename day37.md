# 3) 리눅스
---

<br/>

## 3-1) Linux
---

서버에서 자주 사용하는 OS

* Mac, Window도 서버로 활용은 가능하나 유료

Free, 오픈소스

안전성, 신뢰성

쉘 커맨드, 쉘 스크립트

**CLI & GUI**

CLI(Command Line Interface)

* Terminal

GUI(Graphic User Interface)

* Desktop

**대표적인 Linux 배포판**

Debian

* 온라인 커뮤니티에서 제작해 배포

Ubuntu

* 초보자들이 쉽게 접근할 수 있음

Redhat

* 레드햇 회사에서 배포한 리눅스

CentOS

* Redhat의 브랜드, 로고를 제거한 후 배포

**학습 가이드**

최초에 자주 사용하는 쉘 커맨드, 쉘 스크립트 위주로 학습

* 필요한 코드가 있는 경우 검색

* 새로운 커맨드 학습 후 정리

* 이유에 대한 고민

VirtualBos에 Linux 설치, Docker로 설치

WSL 사용(윈도우)

Notebook에서 터미널 실행

VSCode에서 터미널 실행

<br/>

## 3-2) Shell Command
---

### 쉘

사용자가 문자를 입력해 컴퓨터에 명령할 수 있도록 하는 프로그램

### 터미널/콘솔

쉘을 실행하기 위해 문자 입력을 받아 컴퓨터에 전달

* 프로그램의 출력을 화면에 작성

### sh

최초의 쉘

### bash

Linux 표준 셀

### zsh

Mac 카탈리나 OS 기본 쉘

<br/>

## 쉘 UX

username@hostname:current_folder

* hostname = 컴퓨터 네트워크에 접속된 장치에 할당된 이름. IP 대신 기억하기 쉬운 글자로 저장

* host = 우리 컴퓨터

## 쉘을 사용하는 경우

-서버에서 접속해 사용하는 경우

-crontab 등 Linux의 내장 기능을 활용하는 경우

-데이터 전처리를 하기 위해 쉘 커맨드 사용

-Docker를 사용하는 경우

-수백대의 서버를 관리할 경우

-Jupyter Notebook의 Cell에서 앞에 !를 붙이면 쉘 커맨드 사용가능

-터미널에서 python3, jupyter notebook도 쉘 커맨드임

-Test Code 실행

-배포 파이프라인 실행

## 기본 쉘 커맨드

```bash
#쉘 커맨드의 메뉴얼 문서를 보고싶은 경우
man python
종료: ':q' 입력

#폴더 생성하기(Make Directory)
mkdir linux-test

#현재 접근한 폴더의 파일 확인(List Segments)
ls 뒤에 아무것도 작성하지 않으면 현재 폴더 기준으로 실행
폴더를 작성하면 폴더 기준에서 실행
옵션
-a: .으로 시작하는 파일, 폴더를 포함해 전체 파일 출력
-l: 퍼미션, 소유자, 만든 날짜, 용량까지 출력
-h: 용량을 사람이 읽기 쉽도록 GB, MB 등 표현. '-l'과 같이 사용
ls ~
ls
ls -al
ls -lh

#현재 폴더 경로를 절대 경로로 보여줌(Print Working Directory)
pwd

#폴더 변경하기, 폴더로 이동하기(Change Directory)
cd linux-text

#Python의 print처럼 터미널에 텍스트 출력
echo "hi"

#echo '쉘 커맨드'입력시 쉘 커맨드의 결과를 출력. ':1 왼쪽에 있는 backtick
echo 'pwd'

#파일 또는 폴더 복사하기(Copy)
-r: 디렉토리를 복사할 때 디렉토리 안에 파일이 있으면 recursive(재귀적)으로 모두 복사
-f: 복사할 때 강제로 실행
cp vi-test.sh vi-test2.sh
```

## vi

vim 편집기로 파일 생성

INSERT 모드에서만 수정할 수 있음

vi vi-test.sh

(새로운 창이 뜨면) i를 눌러서 INSERT 모드로 변경

그 후 echo "hi" 작성

ESC 누른 후 :wq (저장하고 나가기, write and quit)

ESC:wq!: 강제로 저장하고 나오기

ESC:q: 그냥 나가기

<br/>

### vi 편집기의 Mode

- Command Mode

- Insert Mode

- Last Line Mode

**Command Mode**

vi 실행시 기본 Mode

- 방향키를 통해 커서 이동 가능

```bash
dd: 현재 위치한 한 줄 삭제
i: INSERT 모드로 변경
x: 커서가 위치한 곳의 글자 1개 삭제(5x: 문자 5개 삭제)
yy: 현재 줄을 복사(1줄을 ctrl + c)
p: 현재 커서가 있는 줄 바로 아래에 붙여넣기
k: 커서 위로
j: 커서 아래로
l: 커서 오른쪽으로
h: 커서 왼쪽으로
```

**Insert Mode**

파일을 수정할 수 있는 Mode

만약 Command Mode로 다시 이동하고 싶다면 ESC 입력

**Last Line Mode**

ESC를 누른 후 콜론(:)을 누르면 나오는 Mode

```bash
w: 현재 파일명으로 저장
q: vi 종료(저장되지 않음)
q!: vi 강제종료(!는 강제를 의미)
wq: 저장한 후 종료
/문자: 문자 탐색
 - 탐색한 후 n을 누르면 계속 탐색 실행
set nu: vi 라인 번호 출력
```

<br/>

### bash

bash로 쉘 스크립트 실행
```bash
bash vi-test.sh
```

앞에서 작성한 "hi"가 출력

터미널에서 Tab을 누르면 자동완성(지원 안하는 쉘도 존재)

<br/>

### sudo

최고 권한을 가진 슈퍼 유저로 프로그램을 실행

<br/>

### mv

```bash
#파일, 폴더 이동하기(Move)
mv vi-test.sh vi-test3.sh
```

<br/>

### cat
```bash
#특정 파일 내용 출력(concatenate)
cat vi-test.sh

#여러 파일을 인자로 주면 합쳐서 출력
cat vi-test2.sh vi-test3.sh

#파일에 저장(OVERWRITE)하고 싶은 경우
cat vi-test2.sh vi-test3.sh > new_test.sh

#파일에 추가(APPEND)하고 싶은 경우
cat vi-test2.sh vi-test3.sh >> new_test.sh
```

<br/>

### clear

터미널 창을 깨끗하게 해줌

<br/>

### history

최근에 입력한 쉘 커맨드 History 출력

History 결과에서 느낌표를 붙이고 숫자 입력시 그 커맨드를 다시 활용가능

* ex) !30

<br/>

### find

파일 및 디렉토리를 검색할 때 사용

find . -name "File": 현재 폴더에서 File이란 이름을 가지는 파일 및 디렉토리 검색

<br/>

### export

export로 환경 변수 설정

```bash
export water="물"
echo $water

#쉘에서는 파이썬처럼 '='에 띄어쓰기 하지 않음
```

<br/>

### alias

기본 명령어를 간단히 줄이기

터미널에 alias라고 치면 현재 별칭으로 설정된 것 볼 수 있음

```bash
#설정법
alias ll2='ls -l'
```
ll2를 입력하면 ls -l이 동작됨

<br/>

### tree

폴더의 하위 구조를 계층적으로 표현

```bash
tree -L 레벨
tree -L 1: 1단계까지 보여주기
tree -L 2: 2단계까지 보여주기
```

<br/>

### head, tail

파일의 앞/뒤 n행 출력

```bash
head -n 3 vi-test.sh
```

<br/>

### sort

행 단위 정렬

-r: 정렬을 내림차순으로 정렬(Default 옵션: 오름차순)

-n: Numeric Sort

```bash
vi fruits.txt

cat fruits.txt | sort
cat fruits.txt | sort -r
```

<br/>

### uniq

중복된 행이 연속으로 있는 경우 중복 제거

sort와 함께 사용

-c: 중복 행의 개수 출력

```bash
cat fruits.txt | uniq
cat fruits.txt | sort | uniq

cat fruits.txt | uniq | wc -l
cat fruits.txt | wort | uniq | wc -l
```

<br/>

### grep

파일에 주어진 패턴 목록과 매칭되는 라인 검색

grep은 뒤에서 나올 pipe와 같이 사용

grep 옵션 패턴 파일명

**옵션**

-i: Insensitively하게, 대소문자 구분 없이 찾기

-w: 정확히 그 단어만 찾기

-v: 특정 패턴 제외한 결과 출력

-E: 정규 표현식 사용

**정규 표현식 패턴**

^단어: 단어로 시작하는 것 찾기

단어$: 단어로 끝나는 것 찾기

.: 하나의 문자 매칭

<br/>

### cut

파일에서 특정 필드 추출

-f: 잘라낼 필드 지정

-d: 필드를 구분하는 구분자. Default는 \t

```bash
vi cut_file
```

## Redirection & Pipe - 표준 스트림(Stream)

Unix에서 동작하는 프로그램은 커맨드 실행시 3개의 STream이 생성

stdin : 0, 입력(비밀번호, 커맨드 등)

stdout : 1, 출력 값(터미널에 나오는 값)

stderr : 2, 디버깅 정보나 에러 출력

<br/>

**Redirection**

프로그램의 출력(stdout)을 다른 파일이나 스트림으로 전달

\> : 덮어쓰기(Overwrite) 파일이 없으면 생성하고 저장

\>> : 맨 아래에 추가하기(Append)

```bash
echo "hi" > vi-test3.sh
echo "hello" >> vi-test3.sh

cat vi-test3.sh
```

<br/>

**Pipe**

프로그램의 출력(stdout)을 다른 프로그램의 입력으로 사용하는 경우

A의 Output을 B의 Input으로 사용(다양한 커맨드 조합)

```bash
#현재 폴더에 있는 파일명 중 vi가 들어간 단어를 찾고 싶은 경우
ls | grep "vi"

grep "vi" : 특정 단어 찾기

ls | grep "vi"
ls | grep "vi" > output.txt #output.txt에 저장

history | grep "echo"
```

<br/>

### ps

현재 실행되고 있는 프로세스 출력(Process Status)

-e : 모든 프로세스

-f : Full Format으로 자세히 보여줌

<br/>

### curl

Command Line 기반의 Data Transfer 커맨드: Client URL

Request를 테스트할 수 있는 명령어

웹 서버를 작성한 후 요청이 제대로 실행되는지 확인 가능

```bash
curl -X localhost:5000/{data}
```
curl 외에 httpie, Postman 등 활용

<br/>

### df

현재 사용 중인 디스크 용량 확인(Disk Free)

-h : 사람이 읽기 쉬운 형태로 출력

### scp

SSH을 이용해 네트워크로 연결된 호스트 간 파일을 주고 받는 명령어(Secure Copy)

-r : 재귀적으로 복사

-P : ssh 포트 지정

-i : SSH 설정을 활용해 실행

```bash
local => remote
scp local_path user@ip:remote_directory

remote => local
scp user@ip:remote_directory local_path

remote => remote
scp user@ip:remote_directory user2@ip2:target_remote_directory
```

<br/>

### nohup

터미널 종료 후에도 계속 작업이 유지되도록 실행

```bash
nohup python3 app.py &
```

Permission이 755여야 함

종료는 ps ef | grep app.py 한 후, pid(Process ID) 찾은 후 kill -9 pid로 프로세스를 Kill

로그는 nohup.out에 저장됨

screen이란 도구도 있음

<br/>

### chmod

파일의 권한을 변경하는 경우 사용(Change Mode)

유닉스에서 파일이나 디렉토리의 시스템 모드를 변경

ls -al(혹은 ll)을 입력

**Permission**

r = Read(읽기), 4

w = Write(쓰기), 2

x = eXecute(실행하기), 1

\- = Denied

r-x : 읽거나 실행할 수는 있지만 수정은 불가능

755로 퍼미션을 준다

7 = 4 + 2 + 1

5 = 4 + 1

아래와 같이 실행하여 파일의 Permission 변경

```bash
chmod 755 vi-test2.sh
```

<br/>

## 쉘 스크립트

.sh 파일을 생성하고, 그 안에 쉘 커맨드를 추가

if, while, case 문이 존재하며 작성시 bash name.sh로 실행

쉘 스크립트 = 쉘 커맨드의 조합

#!/bin/bash
* 이 스크립트를 Bash 쉘로 해석

$(date +%s) : date를 %s(unix timestamp)로 변형