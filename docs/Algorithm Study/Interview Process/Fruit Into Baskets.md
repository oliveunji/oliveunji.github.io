---
layout: default
title: Fruit Into Baskets
parent: Interview Process
grand_parent: Algorithm Study
description: "Fruit Into Baskets"
permalink: /algorithm-study/interview-process/fruit-into-baskets
---

## LeetCode 904. Fruit Into Baskets
### 링크
- [https://leetcode.com/problems/fruit-into-baskets/](https://leetcode.com/problems/fruit-into-baskets/)

<img width="664" alt="image" src="https://user-images.githubusercontent.com/39396725/197741898-1ca192cb-f14b-4539-ad00-0d417deafd3d.png">

제약조건
- -1 <= fruits.length <= 105
- 0 <= fruits[i] < fruits.length

### 풀이방법
Sliding windows (투포인터??)를 사용하며, fruits 배열을 쭉 탐색하며 최대의 길이를 구하면 되는 문제였다.
문제에 대한 감은 잡았고, 방법도 떠올렸으나, 막상 구현을 구체적으로 어떻게 해야할지 몰라서 손을 잘 못댔던 문제였다. 
right 인덱스를 땡기면서, 과일종류가 2개 보다 많아질때까지 left 인덱스도 땡기고, 그때의 light-left+1 의 max값을 계속 업뎃하여, 최종적으로는 가장 큰 max를 리턴하는 것이다. 

### 코드 
```python
class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        basket = {}
        left = 0
        max_picked = 0
        
        for right in range(len(fruits)):
            basket[fruits[right]] = basket.get(fruits[right], 0) + 1
            
            while len(basket) > 2:
                basket[fruits[left]] -= 1
                if basket[fruits[left]] == 0:
                    del basket[fruits[left]]
                left += 1
            
            max_picked = max(max_picked, right - left + 1)
        return max_picked
```

### 시간복잡도
O(N)

### 공간복잡도
O(1)
