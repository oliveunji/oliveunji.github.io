---
layout: default
title: MinAvgTwoSlice
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "MinAvgTwoSlice"
permalink: /algorithm-study/arrays-and-strings/min-avg-two-slice
---

## Codility - MinAvgTwoSlice
### 링크
- [https://app.codility.com/programmers/lessons/5-prefix_sums/min_avg_two_slice/](https://app.codility.com/programmers/lessons/5-prefix_sums/min_avg_two_slice/)

<img width="489" alt="image" src="https://user-images.githubusercontent.com/39396725/210468591-c9af95ad-608e-4af0-b0d0-a49fbeb54139.png">

### 풀이방법
a <= b 일때, a와 b의 평균은 a 이상이 된다. 마찬가지로 (a+b) <= (c+d)일때 (a,b)와 (c,d)의 평균은 (a+b) 이상이 된다.
따라서 원소가 4개인 그룹 (a, b, c, d)은 두개 씩 나누어 고려하면 된다.
원소가 3개인 그룹은 2개 1개 나눠서 고려해야 하지만 최소 원소 개수가 2개 임으로, 2개합과 3개 합으로 나눠서 비교하면 된다. 
수학적인 원리를 이해해야만 풀 수 있는 문제이다. 

### 코드 
```python
def solution(A):
    if len(A) == 2:
        return 0

    min_avg = sum(A[:2]) / 2
    min_str_idx = 0
    
    for i in range(1, len(A)-2):
        # avg for 2
        cur_avg = sum(A[i:i+2]) / 2
        if cur_avg < min_avg:
            min_avg = cur_avg
            min_str_idx = i
        
        # avg for 3
        cur_avg = sum(A[i:i+3]) / 3
        if cur_avg < min_avg:
            min_avg = cur_avg
            min_str_idx = i
        
    last_two_sum = (A[-2]+A[-1]) / 2
    if min_avg > last_two_sum:
        return len(A) - 2
    else:
        return min_str_idx    
```

- [https://app.codility.com/demo/results/trainingFHBGPX-D26/](https://app.codility.com/demo/results/trainingFHBGPX-D26/)

### 시간복잡도
O(N)

### 공간복잡도
O(1)
