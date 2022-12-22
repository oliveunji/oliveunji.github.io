---
layout: default
title: Max Counters
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "Max Counters"
permalink: /algorithm-study/arrays-and-strings/max-counters
---

## Codility - Max Counters
### 링크
- [https://app.codility.com/programmers/lessons/4-counting_elements/max_counters/](https://app.codility.com/programmers/lessons/4-counting_elements/max_counters/)

<img width="452" alt="image" src="https://user-images.githubusercontent.com/39396725/209127870-150f4295-8bed-487a-b9a3-98c16c9c3bf6.png">

### 풀이방법
그냥 곧이 곧데로 Array 변환해서 푼다면 TLE 에러에 걸려버리고 만다 ㅠㅠ
스마트하게 생각을 해보면 매번 max 값 갱신시마다 array 전체를 갱신할 필요가 읎다. 
current max값을 저장해두고, 매번 N 보다 클때마다 max를 갱신하고 저장하고 있다가
array 변환시 그때그때 max보다 작은 값들은 갱신작업 하면되고,
나중에 전체 배열 쭉한번 돌면서, max보다 작은 것들은 max로 셋팅해주면 된다. 

### 코드 
```python
def solution(N, A):
    # Implement your solution here
    arr = [0] * N
    max_val = 0
    cur_max = 0
    for val in A:
        if val > N:
            max_val = cur_max
        else:
            if arr[val-1] < max_val:
                arr[val-1] = max_val
            arr[val-1] += 1
            cur_max = max(cur_max, arr[val-1])
    for idx in range(N):
        if arr[idx] < max_val:
            arr[idx] = max_val
    return arr
```

- 풀이 링크: [https://app.codility.com/demo/results/training7U6W62-JEE/](https://app.codility.com/demo/results/training7U6W62-JEE/)

### 시간복잡도
O(N+M)

### 공간복잡도
O(N)
