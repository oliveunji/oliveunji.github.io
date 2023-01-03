---
layout: default
title: GenomicRangeQuery
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "GenomicRangeQuery"
permalink: /algorithm-study/arrays-and-strings/genomic-range-query
---

## Codility - GenomicRangeQuery
### 링크
- [https://app.codility.com/programmers/lessons/5-prefix_sums/genomic_range_query/](https://app.codility.com/programmers/lessons/5-prefix_sums/genomic_range_query/)

<img width="463" alt="image" src="https://user-images.githubusercontent.com/39396725/210314106-c36e96b4-7a03-4bc4-87df-2577dd428256.png">

### 풀이방법
문제 그대로 갯수세서 풀면 O(N\*M)으로 계산되기 때문에 TLE 에러에 걸린다. 
 O(N\*M) 을 O(N+M)으로 개선하기 위해서는, P[i] ~ Q[i] 계산시 매번 Minimun을 계산하는 방식이 아니라 새로운 배열에 누적치를 계산해놓고, 한번에 계산해야한다. 

- [https://app.codility.com/demo/results/trainingYRYNWY-ADK/](https://app.codility.com/demo/results/trainingYRYNWY-ADK/)
### 코드 
```python
def solution(S, P, Q):
    count_arr = []
    dict = {
        "A": 0,
        "C": 1,
        "G": 2,
        "T": 3
    }
    
    for i in range(len(S)):
        if not count_arr:
            temp = [0,0,0,0]
            cur_idx = dict[S[i]]
            temp[cur_idx] = 1
            count_arr.append(temp)
        else: 
            cur_idx = dict[S[i]]
            prev_item = count_arr[-1][:]
            prev_item[cur_idx] += 1
            count_arr.append(prev_item)
    

    result = []
    for idx in range(len(P)):
        p_idx = P[idx]
        q_idx = Q[idx]
        if p_idx == q_idx:
            result.append(dict[S[p_idx]]+1)
        else:
            if p_idx == 0:
                a = count_arr[q_idx]
                b = [0,0,0,0]
            else:
                a, b = count_arr[q_idx], count_arr[p_idx - 1]
            temp_arr = [ai-bi for ai, bi in zip(a,b) ]
            
            for idx,val in enumerate(temp_arr):
                if val != 0:
                    result.append(idx +1)
                    break
            
    return result         
```

### 시간복잡도
O(N+M)

### 공간복잡도
O(N)
