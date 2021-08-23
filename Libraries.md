# Contents

1. [내장함수](#내장함수)
   
2. [itertools](#itertools)
   
   1. [permutations](#permutations)
   
   2. [combinations](#combinations)
   
   3. [product](#product)
   
   4. [combinations with replacement](#combinations_with_replacement)
   
3. [heapq](#heapq)
   
4. [bisect](#bisect)
   
5. [collections](#collections)
   
   1. [deque](#deque)

   2. [Counter](#counter)
   
6. [math](#math)
   

# [내장함수](#contents)
```python
result = sum([1,2,3,4,5]) # iterable 객체 합계
result = max(1,2,3,4,5) # 주어진 값 중 최대값
result = min(1,2,3,4,5) # 주어진 값 중 최소값

result = eval('(3 + 5) * 7') # 문자열 형태로 들어온 수식 계산
```
### 정렬
```python
result = sorted([1,2,3,4,5], reverse = True) # 내림차순 정렬
data = [1,2,3,4,5] # 위와 동일
data.sort()

result = sorted([{'a',1}, {'b',2}, {'c',3}], key=lambda x: x[1]) # dictionary 특정 키 값으로 정렬
```

# [itertools](#contents)
- 반복 데이터 처리 기능 포함된 라이브러리

### permutations
- 주어진 데이터의 모든 경우의 수를 계산(순열, 순서고려o)
```python
from itertools import permutations

data = ['A','B','C']
result = list(permutations(data, 3)) # 데이터에서 3개를 뽑아서 나올 수 있는 경우의 수
print(result)

> [('A','B','C'), ('A','C','B'), ('B','A','C'), ('B','C','A'), ('C','A','B'), ('C','B','A')]
```

### combinations
- 주어진 데이터의 모든 경우의 수를 계산(조합, 순서고려 x)
```python
from itertools import combinations

data = ['A','B','C']
result = list(combinations(data, 2)) # 데이터에서 2개를 뽑아서 나올 수 있는 경우의 수
print(result)

> [('A','B'), ('A','C'), ('B','C')]
```

### product
- permutations와 같은 순열이지만, 자기자신의 중복이 포함됨
```python
from itertools import product

data = ['A','B','C']
result = list(product(data, repeat=2)) # 데이터에서 2개를 뽑아서 나올 수 있는 경우의 수
print(result)

> [('A','A'), ('A','B'), ('A','C'), , ('B','A'), , ('B','B'), ('B','C'), ('C','A'), ('C','B'), ('C','C')]
```

### combinations_with_replacement
- combinations와 같은 조합이지만, 자기자신의 중복이 포함됨
```python
from itertools import combinations_with_replacement

data = ['A','B','C']
result = list(combinations_with_replacement(data, 2)) # 데이터에서 2개를 뽑아서 나올 수 있는 경우의 수
print(result)

> [('A','A'), ('A','B'), ('A','C'), ('B','B'), ('B','C'), ('C','C')]
```

# [heapq](#contents)
- 우선순위 큐 기능을 구현하고자 할 때 사용
- PriorityQueue보다 코딩테스트에선 더 빠름
- 시간복잡도는 ```O(NlogN)```

### 힙 정렬
```python
import heapq

def heapsort(iterable):
    heap = []
    result = []
    
    for value in iterable:
        heapq.heappush(heap, value)

    for i in range(len(heap)):
        result.append(heapq.heappop(heap))
    
    return result

result = heapsort([1,3,5,7,9,2,4,6,8,0])
```

### 최대 힙 정렬
-  push와 pop할때 값의 부호를 바꿔서 구현
```python
import heapq

def heapsort(iterable):
    heap = []
    result = []
    
    for value in iterable:
        heapq.heappush(heap, -value)

    for i in range(len(heap)):
        result.append(-heapq.heappop(heap))
    
    return result

result = heapsort([1,3,5,7,9,2,4,6,8,0])
```

# [bisect](#contents)
- 이진 탐색을 위한 라이브러리
- 정렬된 배열에서 특정 원소를 찾을 때 사용
- 두 함수 모두 시간 복잡도는 ```O(logN)```

### 바로 왼쪽과 오른쪽 값 찾기
```python
from bisect import bisect_left, bisect_right

list = [1,2,4,4,8]
x = 4

print(bisect_left(list, x))
print(bisect_right(list, x))

> 2
> 4
```

### 주어진 범위 사이에 있는 원소 개수 구하기
```python
from bisect import bisect_left, bisect_right

def count_by_range(list, left_value, right_value):
    right_index = bisect_right(list, right_value)
    left_index = bisect_left(list, left_value)
    return right_index - left_index

list = [1,3,3,3,3,4,4,8,9]
# 값이 4인 데이터 개수 출력
print(count_by_range(list, 4, 4))
# 값이 [-1, 3] 범위인 데이터 개수 출력
print(count_by_range(list, -1, 3))
```

# [collections](#contents)
- deque와 counter 자료 구조를 사용하기 위한 라이브러리

### deque
- List는 앞쪽의 원소를 처리할 때 시간복잡도가 ```O(N)```이지만, deque는 어디에서든지 ```O(1)```임
- deque를 queue처럼 사용하고 싶다면 ```append(x)```와 ```popleft()```만 사용하면 됨
```python
from collections import deque

data = deque([2,3,4])

# 앞에 데이터 삽입/삭제
data.appendleft(1)
data.popleft()

# 뒤에 데이터 삽입/삭제
data.append(5)
data.pop()
```

### Counter
- 원소별 등장 횟수를 세는 기능
- 해당 iterable 객체에서 해당 원소가 몇개 있는지 세는 기능 같음
```python
from collections import Counter

counter = Counter(['r','b','r','g','b','b'])

print(counter['b'])
print(counter['g'])
print(dict(counter))
```

# [math](#contents)
- 수학 함수 라이브러리
```python
import math

# factorial
print(math.factorial(5))

# 제곱근
print(math.sqrt(7))

# 최대 공약수
print(math.gcd(21,14))

# 자연상수 e, pi
print(math.pi)
print(math.e)
```