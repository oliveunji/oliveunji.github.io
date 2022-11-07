---
layout: default
title: Flip Equivalent Binary Trees
parent: Trees and Graphs
grand_parent: Algorithm Study
description: Flip Equivalent Binary Trees"
permalink: /algorithm-study/trees-and-graphs/flip-equivalent-binary-trees
---

## LeetCode 951. Flip Equivalent Binary Trees
### 링크
- [https://leetcode.com/problems/flip-equivalent-binary-trees/](https://leetcode.com/problems/flip-equivalent-binary-trees/)

<img width="464" alt="image" src="https://user-images.githubusercontent.com/39396725/200350332-554c2947-e973-475a-91e8-fb58b34ed4b7.png">

### 제약조건
- The number of nodes in each tree is in the range [0, 100].
- Each tree will have unique node values in the range [0, 99].

### 풀이방법
재귀를 이용해서 풀 수 있다. 내가 놓쳤던 부분이 두개의 노드가 대칭인 경우도 Flip Equivalent Binary Tree로 간주되는 부분이었다. (문제를 더 꼼꼼히 읽었어야 했다)

### 코드
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def flipEquiv(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> bool:
        if not root1 and not root2:
            return True
        if not root1 or not root2 or root1.val != root2.val:
            return False
        return self.flipEquiv(root1.right, root2.left) and self.flipEquiv(root1.left, root2.right) or self.flipEquiv(root1.right, root2.right) and self.flipEquiv(root1.left, root2.left)m
```

### 시간복잡도
O(min(N1,N2))

### 공간복잡도
O(min(H1,H2))
