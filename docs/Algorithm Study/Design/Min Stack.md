---
layout: default
title: Min Stack
parent: Design
# nav_order: 1
grand_parent: Algorithm Study
description: "Min Stack"
permalink: /algorithm-study/design/min-stack
---

## LeetCode 155.Min Stack
### 링크: [https://leetcode.com/problems/min-stack/](https://leetcode.com/problems/min-stack/)

<img width="613" alt="image" src="https://user-images.githubusercontent.com/39396725/197498173-7f3e8e10-a5d1-4c0a-a3fa-b7478585a11a.png">

### 제약조건
- -231 <= val <= 231 - 1
- Methods pop, top and getMin operations will always be called on non-empty stacks.
- At most 3 * 104 calls will be made to push, pop, top, and getMin.

### 풀이방법
Stack 두개를 사용해서 하나는 min값만 신경쓰는 배열로 구현하여, getMin을 O(1)에 처리되게 한다. 

### 코드
```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.minStack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        if not self.minStack or val <= self.minStack[-1]:
            self.minStack.append(val)        

    def pop(self) -> None:
        if self.minStack[-1] == self.stack[-1]:
            self.minStack.pop()
        self.stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.minStack[-1]
```
### 시간복잡도: O(1)

### 공간복잡도: O(N)
