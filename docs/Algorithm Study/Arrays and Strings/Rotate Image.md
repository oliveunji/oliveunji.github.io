---
layout: default
title: Rotate Image
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "Rotate Image"
permalink: /algorithm-study/arrays-and-strings/rotate-image
---

## LeetCode 48. Rotate Image
### 링크
- [https://leetcode.com/problems/rotate-image/](https://leetcode.com/problems/rotate-image/)

<img width="631" alt="image" src="https://user-images.githubusercontent.com/39396725/197765910-8bf01f72-2ce8-4b02-98a1-66a532ddd6de.png">

제약조건
- n == matrix.length == matrix[i].length
- 1 <= n <= 20
- -1000 <= matrix[i][j] <= 1000

### 풀이방법
아... 어렵다. 제자리에서 배열 회전을 한다는게.. 인덱스 조작도 상당히 복잡하다. 
일단 너무 모르겠어서 코드를 외워야겠다.. 

<img width="761" alt="image" src="https://user-images.githubusercontent.com/39396725/205078682-7f3de3ff-d0fb-4b2a-99ed-f26b877793a2.png">

### 코드 
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        for i in range(n//2 + n%2):
            for j in range(n//2):
                tmp = matrix[n-1-j][i]
                matrix[n-1-j][i] = matrix[n-1-i][n-1-j]
                matrix[n-1-i][n-1-j] = matrix[j][n-1-i]
                matrix[j][n-1-i] = matrix[i][j]
                matrix[i][j] = tmp    
```

### 시간복잡도
O(N)

### 공간복잡도
O(1), 제자리 정렬이므로..  
