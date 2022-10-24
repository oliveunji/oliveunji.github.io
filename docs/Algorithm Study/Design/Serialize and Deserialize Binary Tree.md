---
layout: default
title: Serialize and Deserialize Binary Tree
parent: Design
# nav_order: 2
grand_parent: Algorithm Study
description: "Serialize and Deserialize Binary Tree"
permalink: /algorithm-study/design/serialize-and-deserialize-binary-tree
---

## LeetCode 297. Serialize and Deserialize Binary Tree
### 링크: [https://leetcode.com/problems/serialize-and-deserialize-binary-tree/](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

<img width="590" alt="image" src="https://user-images.githubusercontent.com/39396725/197499066-bf1ed2b5-4a77-4262-b52b-1bdfe222b3cc.png">

### 제약조건
- The number of nodes in the tree is in the range [0, 104].
- -1000 <= Node.val <= 1000

### 풀이방법
재귀와 dfs를 잘 활용한다. None 인 value를 어떻게 처리할 것인지 생각해본다. 

### 코드
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:
    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        def serialize_tree(root, result):
            if not root:
                return result.append("#")
            else: 
                result.append(str(root.val))
                serialize_tree(root.left, result)
                serialize_tree(root.right, result)
                return result
        
        result = serialize_tree(root,[])
        # print(','.join(result))
        if not result:
            return '#'
        else:
            return ','.join(result)

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        arr = data.split(',')
        # print(arr)
        
        def deserialzie_tree(arr):
            if not arr:
                return
            else:
                if arr[0] == "#":
                    arr.pop(0)
                    return None

                root = TreeNode(arr.pop(0))
                root.left = deserialzie_tree(arr)
                root.right = deserialzie_tree(arr)
                return root
        return deserialzie_tree(arr)
        
# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```
### 시간복잡도: O(N)

### 공간복잡도: O(N)
{: .fs-3 .pt-2 .pb-2 }
