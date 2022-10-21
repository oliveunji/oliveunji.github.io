---
layout: default
title: Maximum Product Subarray
parent: Dynamic Programming
grand_parent: Algorithm Study
description: "Maximum Product Subarray"
permalink: /algorithm-study/dynamic-programming/maximum-product-subarray
---

## LeetCode 152. Maximum Product Subarray
### 링크
- [https://leetcode.com/problems/maximum-product-subarray/](https://leetcode.com/problems/maximum-product-subarray/)

<img width="745" alt="image" src="https://user-images.githubusercontent.com/39396725/197170049-abdbf453-5719-42ba-bbfe-5f35e98f5858.png">

제약조건
- 1 <= nums.length <= 2 * 104
- -10 <= nums[i] <= 10
- The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

### 풀이방법
dp 결과를 저장할 min 저장용 변수와 max 저장용 변수를 따로 두고, result도 그때 그때 계산해서 업데이트 한다. 

### 코드 
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        min_so_far = nums[0]
        max_so_far = nums[0]
        result = max_so_far
        
        for i in range(1, len(nums)):
            cur = nums[i]
            temp = max(cur, cur*min_so_far, cur*max_so_far)
            min_so_far = min(cur, cur*min_so_far, cur*max_so_far)
            max_so_far = temp
            result = max(result, max_so_far)
        return result
```

### 시간복잡도
O(N)

### 공간복잡도
O(1)
