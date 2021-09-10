# Contents

1. [선택정렬](#선택정렬)

2. [삽입정렬](#삽입정렬)

3. [병합정렬](#병합정렬)

4. [퀵정렬](#퀵정렬)

- 정렬은 파이썬 기본 정렬 라이브러리가 보통 시간이 제일 빠르며, 아래는 특정 정렬 알고리즘을 사용하라고 할때 사용


# [선택정렬](#Contents)

- 매번 가장 작은 값을 선택
- 가장 작은 값과 현재자리의 값을 서로 바꾸는 방식
- 시간복잡도 $O(N^2)$

```python
def selection_sort(array):
    for i in range(len(array)):
        min_index=i

        for j in range(i+1, len(array)):
            if array[min_index] > array[j]:
                min_index = j
        
        array[i], array[min_index] = array[min_index], array[i]
    
    return array
```


# [삽입정렬](#Contents)

- 두번째 데이터부터 정렬 시작
- 각각 맞는 위치에 삽입하여 정렬
- 시간복잡도 $O(N^2)$

```python
def insertion_sort(array):
    for i in range(1, len(array)):
        for j in range(i,0,-1): # i부터 -1
            if array[j]<array[j-1]:
                array[j], array[j-1] = array[j-1], array[j]
            else:
                break

    return array
```


# [병합정렬](#Contents)

- 시간복잡도 = $O(NlogN)$

```python
def mergesort(array):
    if len(array)<=1:
        return array
	#divide
    mid = len(array)//2
    leftarray = array[:mid]
    rightarray = array[mid:]
    mergesort(leftarray)
    mergesort(rightarray)
	#merge
    left = 0
    right = 0
    current = 0
    while left<len(leftarray) and right < len(rightarray):
        if leftarray[left] < rightarray[right]:
            array[current] = leftarray[left]
            left+=1
            current+=1
        else:
            array[current] = rightarray[right]
            right+=1
            current+=1
    while left<len(leftarray):
        array[current] = leftarray[left]
        left+=1
        current+=1
    while right<len(rightarray):
        array[current] = rightarray[right]
        right+=1
        current+=1

    return array
```


# [퀵정렬](#Contents)

- 피벗 설정 후, 피벗보다 작은면 왼쪽, 크면 오른쪽으로 분리
- 그 다음 분류된 것에서 피벗을 재설정 하고 그 안에서 정렬 진행
- 시간복잡도 $O(NlogN)$

```python
def quick_sort(array):
    if len(array)<=1:
        return array

    pivot = array[0]
    tail = array[1:]

    left_array = [x for x in tail if x<=pivot]
    right_array = [x for x in tail if x>pivot]

    return quick_sort(left_array) + [pivot] + quick_sort(right_array)
```


# [계수정렬](#Contents)

- 데이터가 정수 형태로 표현가능할 때만 사용 가능
- 일반적으로 데이터의 최소, 최대값 차이가 1,000,000이 넘지 않을 경우에 효과적임

- 계수정렬은 0~n까지의 인덱스가 있는 리스트에 정렬할 리스트를 돌리며 인덱스에 값을 하나씩 카운트하는 방식으로 정렬함
- 시간복잡도 $O(N+K)$

```python
def count_sort(array):
    count = [0] * (max(array)+1)

    for i in range(len(array)):
        count[array[i]]+=1
    
    for i in range(len(count)): # 출력
        for j in range(count[i]):
            print(i, end=' ')
```