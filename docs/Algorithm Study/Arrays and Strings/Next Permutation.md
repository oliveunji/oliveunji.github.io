---
layout: default
title: Next Permutation
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "Next Permutation"
permalink: /algorithm-study/arrays-and-strings/next-permutation
---

## LeetCode 31. Next Permutation
### 링크
- [https://leetcode.com/problems/next-permutation/](https://leetcode.com/problems/next-permutation/)

<img width="1079" alt="image" src="https://user-images.githubusercontent.com/39396725/196629396-f22aaf9e-52c6-4c2d-84b5-174856cf1ff2.png">

제약조건
- 1 <= nums.length <= 100
- 0 <= nums[i] <= 100

### 풀이방법
일단, 수학적으로 next permutation이 뭘 의미하는지를 잘 이해하는게 중요하다. 나는 쉽게 이해하기 위해서 그다음으로 만들수 있는 큰수(?) 로 이해했다. 
i, j를 배열의 맨 끝으로 놓고, 앞의 수가 뒤의 수보다 작는 순간이 올때까지 i를 땡긴다.
i를 찾아놓고서는, i-1 고정해놓고, Swap할 대상인 j를 찾아야 하는데, i-1 보다 살짝 더 큰 값을 찾기 위해 j를 뒤에서부터 앞으로 가져오면서 찾는다.
그러고나서는 i 뒤의 내용의 순서를 reverse 한다. 

### 코드 
```python
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        i = j = len(nums) -1
        while i > 0 and nums[i-1] >= nums[i]:
            i -= 1
        if i > 0:
            while nums[j] <= nums[i-1]:
                j -= 1
            nums[i-1], nums[j] = nums[j], nums[i-1]
        nums[i:] = nums[i:][::-1]
```

### 시간복잡도
O(N)

### 공간복잡도
O(1) 
