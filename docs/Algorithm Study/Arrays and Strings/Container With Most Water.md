---
layout: default
title: Container With Most Water
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "Container With Most Water"
permalink: /algorithm-study/arrays-and-strings/container-with-most-water
---

## LeetCode 11. Container With Most Water
### 링크
- [https://leetcode.com/problems/container-with-most-water/](https://leetcode.com/problems/container-with-most-water/)

<img width="557" alt="image" src="https://user-images.githubusercontent.com/39396725/196368306-856b944c-dff7-4cca-83f4-2136d1e56e91.png">

제약조건
- n == height.length
- 2 <= n <= 105
- 0 <= height[i] <= 104

### 풀이방법
투 포인터를 이용하여, 하나는 i = 0부터 j는 배열의 끝부터 이동하며, height이 더 크게끔 계속 두 포인터를 이동시킨다. 
두포인터가 만나는 시점에 연산을 종료하며, 중간중간 max area size를 업데이트 하면 가장 큰 너비가 구해져있다. 
배열을 한번만 스캔하기 때문에 O(N) 시간에 해결된다. 

### 코드 
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        N = len(height)
        i = 0
        j = N-1
        result = 0
        
        while i < j:
            curArea = (j-i)*min(height[i], height[j])
            result = max(result, curArea)
            if height[i] < height[j]:
                i += 1
            else:
                j -= 1
        
        return result                         
```

### 시간복잡도
O(N)

### 공간복잡도
O(1)
