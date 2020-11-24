# Contents

???

????

# 선택 정렬

# 삽입 정렬

# 병합정렬

- 시간복잡도 = O(nlogn)

```python
def mergesort(list):
    if len(list)<=1:
        return list
	#divide
    mid = len(list)//2
    leftlist = list[:mid]
    rightlist = list[mid:]
    mergesort(leftlist)
    mergesort(rightlist)
	#merge
    left = 0
    right = 0
    current = 0
    while left<len(leftlist) and right < len(rightlist):
        if leftlist[left] < rightlist[right]:
            list[current] = leftlist[left]
            left+=1
            current+=1
        else:
            list[current] = rightlist[right]
            right+=1
            current+=1
    while left<len(leftlist):
        list[current] = leftlist[left]
        left+=1
        current+=1
    while right<len(rightlist):
        list[current] = rightlist[right]
        right+=1
        current+=1
```

# 퀵 정렬