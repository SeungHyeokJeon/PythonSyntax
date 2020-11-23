# Contents

1. 자료형
   1. [정수/실수형](#정수/실수형)
   2. [연산자](#연산자)
   3. [리스트](#리스트)
   4. [문자열](#문자열)
   5. [튜플 자료형](#튜플 자료형)
   6. [사전 자료형](#사전 자료형)
   7. [집합 자료형](#집합 자료형)

# 정수/실수형

### 실수형 제대로 비교하기

- 반올림해서 비교함

```python
a = 0.3+0.6     #0.89999...

#소수점 넷째 자리에서 반올림
print(round(a,4))
```

# 연산자

```python
a=7; b=3
a / b   #나눗셈
a % b   #나머지
a // b  #몫
a ** b  #거듭제곱, a의 b승
```

# 리스트

### 리스트 선언방법

```python
a=list()    #1

a=[]        #2
```

### 리스트의 인덱싱

- index값을 입력해 리스트의 특정 원소에 접근하는 것

```python
a=[1,2,3,4,5,6,7,8,9]

# 뒤에서 세 번째 원소 출력
print(a[-3])
```

### 리스트의 슬라이싱

```python
a=[1,2,3,4,5,6,7,8,9]

# 리스트의 첫번째 부터 네번째 원소까지 출력
print(a[1:4])
```

### 리스트 Comprehension

- 리스트를 쉽게만들기 위한 방법
- [들어갈 값 / 반복문 / 조건] 형식으로 작성

```python
# 0부터 n까지의 수 중에서 홀수만 포함하는 리스트
array=[i for i in range(n) if 1 % 2 == 1]

# 1부터 9까지의 수의 제곱 수를 포함하는 리스트
array=[i * i for i in range(1,10)]

# N x M 크기의 2차원 리스트 초기화
array=[[0]*M for _ in range(N)]
```

- 2차원 리스트를 선언 할 때는 무조건 comprehension을 이용해야 함

### 리스트 관련 method

```python
list.append(값)   #원소 하나 맨 뒤에 삽입
list.insert(삽입할 위치 인덱스, 값) #특정 위치에 삽입
list.sort()     #원소 오름차순으로 정렬
list.reverse()  #순서 반전
list.count(값)    #특정 값 데이터 개수
list.remove(값)   #특정 값 원소 제거, 여러 개면 하나만 제거
```

- append 시간복잡도 O(1)
- sort 시간복잡도 O(NlogN)
- 그외 시간복잡도 O(N)

# 문자열

### 문자열 연산

```Python
a = "Hello"
b = "World!"
print(a+" "+b)

Hello World!
```

```python
a = "String"
print(a*3)

StringStringString
```

```python
a = "ABCDEF"
print(a[2:4])

CD
```

# 튜플 자료형

- 리스트와 달리 한 번 선언된 값을 변경할 수 없다.
- 튜플은 **소괄호**를 이용하여 선언함

```python
a = (1,2,3,4)	#튜플 선언
a = [1,2,3,4]	#리스트 선언
```

# 사전 자료형

- 키와 값을 쌍으로 가지는 자료형
- 키-값 쌍으로 이루어진 데이터를 처리할 때 **리스트보다 훨씬 빠름**

```python
data = dict()
data['사과']='Apple'
data['바나나']='Banana'
data['코코넛']='Coconut'
print(data)

{'사과': 'Apple', '바나나': 'Banana', '코코넛': 'Coconut'}

if '사과' in data:
    print("inn")

inn
```

### 사전 자료형 관련 함수

```python
data = dict()
data['사과']='Apple'
data['바나나']='Banana'
data['코코넛']='Coconut'

#키 데이터만 담은 리스트
key_list = data.keys()
#값 데이터만 담은 리스트
value_list = data.values()
```

# 집합 자료형

- 리스트와 달리 중복 허용 x
- 순서 x
- 집합은 **중괄호**를 이용하여 선언하기도함

### 집합 자료형 초기화

```python
#방법 1
data = set([1,1,2,3,4,4,5])
print(data)

{1,2,3,4,5}

#방법 2
data = {1,1,2,3,4,4,5}
print(data)

{1,2,3,4,5}
```

### 집합 자료형 연산

```python
a = {1,2,3,4,5}
b = set([3,4,5,6,7])

print(a|b) #합집합
print(a&b) #교집합
print(a-b) #차집합

{1,2,3,4,5,6,7}
{3,4,5}
{1,2}
```

### 집합 자료형 관련 함수

```python
data = {1,2,3}

#원소 추가
data.add(4)

#원소 여러개 추가
data.update([5,6])

#특정한 원소 삭제
data.remove(3)
```

# Input

### 두 개이상 변수에 입력 받기

```python
a,b = input().split()

a,b = map(int,input().split())
```

### 입력 더 빠르게 받기

```python
import sys

a = sys.stdin.readline().rstrip()
```

- rstrip() 사용이유는 readline()으로 입력받으면 맨 뒤에 공백문자까지 저장되서 그 공백문자를 없애주기 위함

### 정수 또는 실수형으로 강제 입력받기

```python
x=int(input())      #정수
x=float(input())    #실수
```

### 유니코드 문자로 입력받고, 출력하기

```python
print(ord("a"))
print(chr(97))

97
a
```

# Output

### printf 처럼 변수 넣기

```python
x=1.423
print("%f" % x)

#여러 개의 변수 넣기
a=1;b=2
print("%d %d"%(a,b))
```

- 정수는 print안에 + 사용불가능! 무조건 format 사용해야됨

# 조건문

### 기본 조건문 사용방법

```python
if 조건문 1:
    code
elif 조건문 2:
    code
else:
    code
```

### 비교 연산자

- x==y / x!=y
- x<y / x>y
- x>=y / x<=y

### 논리 연산자

- 파이썬에서는 문자로 표현한다
- && = and
- || = or
- ! = not

### 기타 연산자

- X in 리스트(문자열)
- X not in 리스트(문자열)

### 조건부 표현식

```python
score = 85
result = "Success" if score >=80 else "Fail"
```

# 반복문

### while

```python
i=0
while i<=5:
    i++
```

### for

```python
for i in range(0,5):
    print(i)

list = [1,2,3,5]
for i in list:
    print(i)
```

# 함수

```python
def functionname(parameter):
    codes...
    return value
```

