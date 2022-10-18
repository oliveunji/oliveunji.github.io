---
layout: default
title: Course Scheduel 2
parent: Trees and Graphs
grand_parent: Algorithm Study
description: "Course Schedule 2"
permalink: /algorithm-study/trees-and-graphs/course-schedule-2
---

## LeetCode 210. Course Schedule 2
### 링크
- [https://leetcode.com/problems/course-schedule-ii/](https://leetcode.com/problems/course-schedule-ii/)

<img width="576" alt="image" src="https://user-images.githubusercontent.com/39396725/196342199-6a9e49e5-2520-4330-9920-e6308b746f4a.png">

제약조건
- 1 <= numCourses <= 2000
- 0 <= prerequisites.length <= numCourses * (numCourses - 1)
- prerequisites[i].length == 2
- 0 <= ai, bi < numCourses
- ai != bi
- All the pairs [ai, bi] are distinct.

### 풀이방법
1. DFS
: numCourses 배열을 돌면서 선수과목과 그 이후에 들어야 하는 과목에 대한 정보를 dictionary에 list 형태로 저장한다. 
단, 선수과목들을 순서대로 들어야 함으로 각 노드들의 상태를 색으로 구별해서 탐색하고, 깊이 우선 탐색이므로 최종 결과값을 [::-1] 해서 리턴해야 한다.
2. BFS
: 순서대로 선수과목 출력하기 위해 indegree라는 정보를 별도로 저장하여 관리하고 그 순서대로 탐색을 한다. 

### 코드
```python
from typing import List
import collections

class Solution:
    
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        adj_list = collections.defaultdict(list)
        indegree = {}
        for dest, src in prerequisites:
            adj_list[src].append(dest)
            indegree[dest] = indegree.get(dest, 0) + 1
        
        zero_indegree_queue = collections.deque([k for k in range(numCourses) if k not in indegree])
        
        topological_sorted_order = []
        
        while zero_indegree_queue:
            v = zero_indegree_queue.popleft()
            topological_sorted_order.append(v)
            
            if v in adj_list:
                for neighbor in adj_list[v]:
                    indegree[neighbor] -= 1
                    if indegree[neighbor] == 0:
                        zero_indegree_queue.append(neighbor)
        return topological_sorted_order if len(topological_sorted_order) == numCourses else []

sol = Solution()
sol.findOrder(4, [[1,0],[2,0],[3,1],[3,2]])
```

### 시간복잡도
O(V+E): V가 vertices의 수, E가 엣지수 일때

### 공간복잡도
O(V+E)
