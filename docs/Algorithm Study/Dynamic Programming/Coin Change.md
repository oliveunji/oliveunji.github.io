---
layout: default
title: Coin Change
parent: Dynamic Programming
grand_parent: Algorithm Study
description: "Coin Change"
permalink: /algorithm-study/dynamic-programming/coin-change
---

## LeetCode 322. Coin Change
### 링크
- [https://leetcode.com/problems/coin-change/](https://leetcode.com/problems/coin-change/)

<img width="680" alt="image" src="https://user-images.githubusercontent.com/39396725/198205788-c4fe79c8-09d5-479e-9a3a-e2affec419eb.png">

제약조건
- 1 <= coins.length <= 12
- 1 <= coins[i] <= 231 - 1
- 0 <= amount <= 104

### 풀이방법
dp 결과를 저장할 array를 미리 선언해놓고, bottom up 방식으로 해당 amount를 계산하기 까지 최소의 coin갯수를 저장하고, 더 큰 amount 계산시 과거의 값을 활용한다. 

### 코드 
```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')] * (amount + 1)
        dp[0] = 0
        
        for coin in coins:
            for x in range(coin, amount + 1):
                dp[x] = min(dp[x], dp[x-coin]+1)
        return dp[amount] if dp[amount] != float('inf') else -1
```

### 시간복잡도
O(S\*N)

### 공간복잡도
O(S)
