---
layout: default
title: Binary Tree Maximum Path Sum
parent: Trees and Graphs
grand_parent: Algorithm Study
description: "Binary Tree Maximum Path Sum"
permalink: /algorithm-study/trees-and-graphs/binary-tree-maximum-path-sum
---

## LeetCode 124. Binary Tree Maximum Path Sum
### 링크
- [https://leetcode.com/problems/word-ladder/](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

<img width="385" alt="image" src="https://user-images.githubusercontent.com/39396725/196225398-1de30a4a-3f08-49cb-a151-101bbef6beea.png">

### 제약조건
- The number of nodes in the tree is in the range [1, 3 * 104].
- 1000 <= Node.val <= 1000

### 풀이방법
재귀를 이용해서 풀 수 있다. 내가 어려웠던 부분이 Node가 None인경우 처리하는 부분이었는데, None인 경우 return을 0으로 처리한다.
그럼 값이 음수인경우 어떻게 하느냐고? 초기값을 -sys.maxsize 로 처리하기때문에 괜찮다.

### 코드
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        def gain_path(node):
            nonlocal max_sum
            if not node:
                return 0
            
            left_gain = max(gain_path(node.left), 0)
            right_gain = max(gain_path(node.right), 0)
            
            new_path_sum = node.val + left_gain + right_gain
            max_sum = max(max_sum, new_path_sum)
            return node.val + max(left_gain, right_gain)
            
            
        max_sum = -sys.maxsize
        gain_path(root)
        return max_sum
```

### 시간복잡도
O(N): 각 Node를 두번 이상 방문하지 않기 때문에 O(N)

### 공간복잡도
O(H), H는 트리의 높이를 의미하며 balanced Tree인경우 H = LogN, worst case의 경우 H = N 이다. 
