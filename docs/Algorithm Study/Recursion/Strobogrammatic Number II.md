---
layout: default
title: Strobogrammatic Number II
parent: Recursion
grand_parent: Algorithm Study
description: "Strobogrammatic Number II"
permalink: /algorithm-study/recursion/strobogrammatic-number-II
---

## LeetCode 247. Strobogrammatic Number II
### 링크
- [https://leetcode.com/problems/strobogrammatic-number-ii/](https://leetcode.com/problems/strobogrammatic-number-ii/)

<img width="525" alt="image" src="https://user-images.githubusercontent.com/39396725/196930837-9a0e6f56-e393-4f1f-9e60-f28c5891d361.png">

제약조건
- 1 <= n <= 14

### 풀이방법
dfs로 재귀적으로 돌면서, 양쪽으로 두개씩 빼면서 양 옆으로 뒤집어도 같은 모양인 숫자들을 계속해서 append해주고 그 결과를 리턴한다.
풀이방법에 대한 감은 잡았으나 구현 실력 부족으로 인해 코드를 작성하지 못해서 너무 아쉬웠다. 

### 코드 
```python
class Solution:
    def findStrobogrammatic(self, n: int) -> List[str]:
        reversible_pairs = [
            ['0','0'], ['1','1'],['6','9'],['8','8'],['9','6']
        ]
        
        def gen_strobo_num(n, final_length):
            if n == 0:
                return [""]
            
            if n == 1:
                return ['0','1','8']
            
            prev_strobo_nums = gen_strobo_num(n-2, final_length)
            curr_strobo_nums = []
            
            for prev_strobo_num in prev_strobo_nums:
                for pair in reversible_pairs:
                    if pair[0] != '0' or n != final_length:
                        curr_strobo_nums.append(pair[0] + prev_strobo_num + pair[1])
            return curr_strobo_nums
        
        return gen_strobo_num(n,n)
```

### 시간복잡도
O(N\*5^(n/2+1))

### 공간복잡도
O(N\*5^(N/2))
