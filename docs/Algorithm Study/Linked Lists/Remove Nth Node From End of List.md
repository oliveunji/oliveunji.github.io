---
layout: default
title: Remove Nth Node From End of List
parent: Linked Lists
grand_parent: Algorithm Study
description: "Remove Nth Node From End of List"
permalink: /algorithm-study/trees-and-graphs/remove-nth-node-from-end-of-list
---

## LeetCode 19. Remove Nth Node From End of List
### 링크
- [https://leetcode.com/problems/remove-nth-node-from-end-of-list/](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

<img width="542" alt="image" src="https://user-images.githubusercontent.com/39396725/196356673-c4aeaf23-9b82-4a0e-bae2-1f07898a0de4.png">

제약조건
- The number of nodes in the list is sz.
- 1 <= sz <= 30
- 0 <= Node.val <= 100
- 1 <= n <= sz

### 풀이방법
1. 노드의 끝까지 탐색하여 전체 길이를 알아낸후, head에서부터 얼만큼 떨어져있는지 계산한 후, head부터 다시 이동하여, target 노드 삭제 
2. 더미노드 하나와 head 가리키는 노드 하나 (prev, cur) 두고 cur을 일단 n만큼 이동시킨 후에, cur이 끝까지 가면 prev노드의 다음 노드 삭제하면 된다.
<img width="402" alt="image" src="https://user-images.githubusercontent.com/39396725/196358059-0832cefe-3da5-4dfc-bb06-5c49a5934949.png">
장점: 한번 연결리스트 탐색으로 풀이 가능 -> 1번 풀이보다 성능이 좋을 것이다.  

### 코드 
2번 방법에 대해서만 풀이하도록 하겠다. 
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0,head)
        node1 = dummy
        node2 = head
        
        for _ in range(n):
            node2 = node2.next
        
        while node2:
            node2 = node2.next
            node1 = node1.next
        node1.next = node1.next.next
        return dummy.next
```

### 시간복잡도
O(N)

### 공간복잡도
O(1)
