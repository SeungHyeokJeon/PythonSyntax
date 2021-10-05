# Contents

1. [자료구조](#자료구조)

    1. [스택](#Stack)

    2. [큐](#Queue)

    3. [그래프](#Graph)

        - [인접 행렬](#인접-행렬)

        - [인접 리스트](#인접-리스트)
2. [알고리즘](#알고리즘)

    1. [DFS](#DFS)

        - [붙어있는 영역 개수 세기](#붙어있는-영역-개수-세기)
    2. [BFS](#BFS)
        - [최단 경로 찾기](#최단-경로-찾기)
    3. [이진탐색](#이진탐색)
        - [재귀적으로 구현](#재귀적으로-구현)
        - [반복적으로 구현](#반복적으로-구현)
3. [Dynamic Programming](#Dynamic-Programming)
    1. [Memoization 기법](#[Memoization-기법])


# [자료구조](#Contents)

## [Stack](#Contents)

- FIFO

```python
stack = []

stack.append(5)
stack.pop()
```

## [Queue](#Contents)

-  LIFO

```python
from collections import deque

# deque는 list와 달리 맨앞에 삽입됨
queue = deque()

queue.append(5) # 삽입은 append
queue.popleft() # 삭제는 제일 popleft 사용
```

## [Graph](#Contents)

### 인접 행렬

- 2차원 List로 그래프의 연결 관계를 표현
- 연결되어 있지 않은 노드는 무한의 비용(INF, 999999999)이라고 작성함
```python
INF = 999999999

graph = [
    [0,7,5],
    [7,0,INF],
    [5,INF,0]
]
```

### 인접 리스트

- 1차원 List로 그래프의 연결 관계를 표현
- 모든 노드에 연결된 노드에 대한 정보를 차례대로 연결하여 저장
```python
# row = 3
graph = [[] for _ in range(3)]

# 연결된 노드 정보
graph[0].append((1,7)) # (노드, 거리)
graph[0].append((2,5))

graph[1].append((0,7))

graph[2].append((0,5))
```





# [알고리즘](#Contents)

- 좌표가 주어지는 형태의 문제를 그래프를 사용하여 해결할 수 있음

## [DFS](#Contents)

- Depth-First Seach
- 노드가 깊은 순서부터 탐색
- 붙어있는 모든 노드를 탐색할때 사용
- 시간복잡도 O(N)
```python
def dfs(graph, v, visited):
    visited[v] = True
    print(v, end=' ')

    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

# sample    
graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3,5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]
visited = [False]*9
dfs(graph,1,visited)
```

### 붙어있는 영역 개수 세기

```python
def dfs(x,y):
    if x<0 or x>=n or y<0 or y>=m:
        return False

    if graph[x][y]==0:
        graph[x][y]=1
        dfs(x,y-1)
        dfs(x,y+1)
        dfs(x-1,y)
        dfs(x+1,y)
        return True

    return False

# n,m = map(int,input().split())
# graph = []
n=15;m=14
graph=[
    [0,0,0,0,0,1,1,1,1,0,0,0,0,0],
    [1,1,1,1,1,1,0,1,1,1,1,1,1,0],
    [1,1,0,1,1,1,0,1,1,0,1,1,1,0],
    [1,1,0,1,1,1,0,1,1,0,0,0,0,0],
    [1,1,0,1,1,1,1,1,1,1,1,1,1,1],
    [1,1,0,1,1,1,1,1,1,1,1,1,0,0],
    [1,1,0,0,0,0,0,0,0,1,1,1,1,1],
    [0,1,1,1,1,1,1,1,1,1,1,1,1,1],
    [0,0,0,0,0,0,0,0,0,1,1,1,1,1],
    [0,1,1,1,1,1,1,1,1,1,1,0,0,0],
    [0,0,0,1,1,1,1,1,1,1,1,0,0,0],
    [0,0,0,0,0,0,0,1,1,1,1,0,0,0],
    [1,1,1,1,1,1,1,1,1,1,0,0,1,1],
    [1,1,1,0,0,0,1,1,1,1,1,1,1,1],
    [1,1,1,0,0,0,1,1,1,1,1,1,1,1]
]

count=0
for i in range(n):
    for j in range(m):
        if dfs(i,j)==True:
            count+=1

print(count)
```


## [BFS](#Contents)

- Breadth First Search
- 가까운 노드부터 탐색
- 최소 거리 탐색 문제에 사용
- 시간복잡도 O(N)
```python
from collections import deque

def bfs(graph, start, visited):
    queue = deque([start])
    visited[start] = True # 현재 노드 방문 처리

    while queue:
        v = queue.popleft() # 큐에서 하나 뽑아 출력
        print(v, end=' ')

        for i in graph[v]:  # v와 연결된 방문안된 노드 삽입
            if not visited[i]:
                queue.append(i)
                visited[i] = True

# sample    
graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3,5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]
visited = [False]*9
bfs(graph,1,visited)
```

### 최단 경로 찾기

```python
from collections import deque

dx=[-1,1,0,0]
dy=[0,0,-1,1]

def bfs(x,y):
    queue = deque()
    queue.append((x,y))

    while queue:
        x, y = queue.popleft()

        # 현재 위치에서 네 방향 위치 확인
        for i in range(4):
            nx=x+dx[i]
            ny=y+dy[i]
            
            # 공간 벗어난 경우 무시
            if nx<0 or nx>=n or ny<0 or ny>=m:
                continue
            # 벽인 경우 무시
            if graph[nx][ny]==0:
                continue
            
            # 처음 방문인 경우에만 기록
            if graph[nx][ny]==1:
                graph[nx][ny]=graph[x][y]+1
                queue.append((nx,ny))
    
    # 모든 경우의 수 출력
    return graph[n-1][m-1]

# n,m = map(int,input().split())
# graph = []
n=5;m=6
graph=[
    [1,0,1,0,1,0],
    [1,1,1,1,1,1],
    [0,0,0,0,0,1],
    [1,1,1,1,1,1],
    [1,1,1,1,1,1]
]

print(bfs(0,0))
```

## [이진탐색](#Contents)

- 배열 내부 데이터가 정렬되어 있어야만 사용 가능

### 재귀적으로 구현

```python
def binary_search(array, target, start, end):
    if start > end:
        return
    
    mid = (start+end)//2 # 중간점
    
    if array[mid]==target:
        return array[mid]
    
    # 중간점 보다 작을 경우 end 값을 중간점으로
    elif array[mid]>target:
        return binary_search(array, target, start, mid-1)
    
    # 중간점 보다 클 경우 start 값을 중간점으로
    else:
        return binary_search(array, target, mid+1, end)
```

### 반복적으로 구현

```python
def binary_search(array, target, start, end):
    while start<=end:
        mid = (start+end)//2 # 중간점

        if array[mid]==target:
            return array[mid]
        
        # 중간점 보다 작을 경우 end 값을 중간점으로
        elif array[mid]>target:
            end = mid-1
        # 중간점 보다 클 경우 start 값을 중간점으로
        else:
            start = mid+1
            
    return
```

# [Dynamic Programming](#Contents)

## [Memoization 기법](#Contents)

- 피보나치 예제

```python
n=99
# Memoization하기 위한 List 정의
d = [0]*(n+1)

def fibo(x):
    # 종료 조건
    if x==1 or x==2:
        return 1
    
    # 이미 계산한 값이라면
    if d[x]!=0:
        # 계산한 값 그대로 반환
        return d[x]
    
    # 계산 안한 값이라면
    d[x] = fibo(x-1)+fibo(x-2)
    return d[x]

print(fibo(n))
```

