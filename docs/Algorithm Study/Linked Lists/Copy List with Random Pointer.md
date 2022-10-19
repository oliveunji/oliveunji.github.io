---
layout: default
title: Copy List with Random Pointer
parent: Linked Lists
grand_parent: Algorithm Study
description: "Copy List with Random Pointer"
permalink: /algorithm-study/trees-and-graphs/copy-list-with-random-pointer
---

## LeetCode 138. Copy List with Random Pointer
### 링크
- [https://leetcode.com/problems/copy-list-with-random-pointer/](https://leetcode.com/problems/copy-list-with-random-pointer/)

<img width="955" alt="image" src="https://user-images.githubusercontent.com/39396725/196606807-667ad0c3-72d0-4f5e-82af-ce87b1f03da6.png">

제약조건
- 0 <= n <= 1000
- -104 <= Node.val <= 104
- Node.random is null or is pointing to some node in the linked list.

### 풀이방법
사실 이 문제를 처음 접했을때는 어떻게 풀어야 할지 감을 못잡았던것 같다. 연결리스트 문제임으로 
1. 재귀 이용 -> 하지만 random pointer 때문에 cycle이 발생할 수 있으므로 주의해야 한다. visitedHash를 두어서 접근했던 노드는 해시에 저장해놓고 가져다 쓴다. 


### 코드 
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def __init__(self):
        self.visitedHash = {}
        
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head:
            return None
        
        if head in self.visitedHash:
            return self.visitedHash[head]
        
        node = Node(head.val, None, None)
        self.visitedHash[head] = node
        
        node.next = self.copyRandomList(head.next)
        node.random = self.copyRandomList(head.random)
        
        return node
```

### 시간복잡도
O(N)

### 공간복잡도
O(N)
