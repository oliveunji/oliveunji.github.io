---
layout: default
title: Split Array Largest Sum
parent: Dynamic Programming
grand_parent: Algorithm Study
description: "Split Array Largest Sum"
permalink: /algorithm-study/dynamic-programming/split-array-largest-sum
---

## LeetCode 410. Split Array Largest Sum
### 링크
- [https://leetcode.com/problems/split-array-largest-sum/](https://leetcode.com/problems/split-array-largest-sum/)

<img width="763" alt="image" src="https://user-images.githubusercontent.com/39396725/198215875-bdd61541-f00a-4812-8562-2ab49e38b39d.png">

제약조건
- 1 <= nums.length <= 1000
- 0 <= nums[i] <= 106
- 1 <= k <= min(50, nums.length)

### 풀이방법
다시 읽어보고 이해해야 함.

### 코드 
```python
class Solution:
    def splitArray(self, nums: List[int], k: int) -> int:
        lo, hi = max(nums), sum(nums)
        while lo < hi:
            mid = (lo+hi) // 2
            tot, cnt = 0, 1
            for num in nums:
                if tot + num <= mid:
                    tot += num
                else:
                    tot = num
                    cnt += 1
            if cnt > k:
                lo = mid + 1
            else:
                hi = mid
        return hi
```

### 시간복잡도
O(N\*log(S))

### 공간복잡도
O(1)
