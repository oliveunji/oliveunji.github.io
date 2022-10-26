---
layout: default
title: Longest Increasing Path in a Matrix
parent: Trees and Graphs
grand_parent: Algorithm Study
description: "Longest Increasing Path in a Matrix"
permalink: /algorithm-study/trees-and-graphs/longest-increasing-path-in-a-matrix
---

## LeetCode 329. Longest Increasing Path in a Matrix
### 링크
- [https://leetcode.com/problems/longest-increasing-path-in-a-matrix/](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)

<img width="694" alt="image" src="https://user-images.githubusercontent.com/39396725/198005121-05ab5e30-e58f-4c9f-8533-5b69a796e595.png">

### 제약조건
- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 200
- 0 <= matrix[i][j] <= 231 - 1

### 풀이방법
dfs로 풀고, memoization을 이용해서 이전에 계산했던 결과값을 저장하여 효율적으로 풀어야 하는 문젱다.
dfs로 풀때 탈출조건을 잘 작성하는 것도 중요한데 이부분이 헷깔려서 코드에 대한 엄두를 내지 못한거 같다. 


### 코드
```python
class Solution:
    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
        m, n = len(matrix), len(matrix[0])
        
        dp = [[-1]*n for _ in range(m)]
        
        def dfs(i,j, prev):
            if i <0 or j <0 or i>=m or j>= n or matrix[i][j] <= prev:
                return 0
            if dp[i][j] != -1:
                return dp[i][j]
            
            left = dfs(i, j-1, matrix[i][j])
            right = dfs(i, j+1, matrix[i][j])
            top = dfs(i-1, j, matrix[i][j])
            bottom = dfs(i+1, j, matrix[i][j])
            
            dp[i][j] = max(left, right, top, bottom) + 1
            return dp[i][j]
        
        ans = -1
        for i in range(m):
            for j in range(n):
                ans = max(ans, dfs(i,j, -1))
        return ans
```

### 시간복잡도
O(MN)

### 공간복잡도
O(MN)
