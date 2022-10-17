---
layout: default
title: Word Ladder
parent: Trees and Graphs
# nav_order: 1
grand_parent: Algorithm Study
description: "Word Ladder"
permalink: /algorithm-study/trees-and-graphs/word-ladder
---

## LeetCode 127 Word Ladder
### 링크: https://leetcode.com/problems/word-ladder/

<img width="383" alt="image" src="https://user-images.githubusercontent.com/39396725/196211019-21ec3047-8adb-4c2c-a9d8-ef5fbc08f290.png">

### 제약조건
- 1 <= beginWord.length <= 10
- endWord.length == beginWord.length
- 1 <= wordList.length <= 5000
- wordList[i].length == beginWord.length
- beginWord, endWord, and wordList[i] consist of lowercase English letters.
- beginWord != endWord
- All the words in wordList are unique.

### 풀이방법
Begin Word를 시작으로 해서, 1개 차이가 나는 단어를 그 다음 노드로 하는 연결리스트를 만들고, BFS 탐색을 통해 해결한다. 

#### 핵심적으로 생각해야 할 부분
단어차이가 1개 나는 부분을 어떻게 연산할 것인가? 
예를들어, hot이라는 단어가 주어진경우, \*ot, h\*t, ho\* 이렇게 마스킹을 해서 전처리 후 연산한다
<img width="1043" alt="image" src="https://user-images.githubusercontent.com/39396725/196218032-d183ea7c-c37f-4dcb-abf4-f58ba1395951.png">

### 코드
```python
import collections
from typing import List

class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        if endWord not in wordList or not endWord or not beginWord or not wordList:
            return 0
        L = len(beginWord)

        dict = collections.defaultdict(list)
        for word in wordList:
            for i in range(L):
                dict[word[:i] + "*" + word[i+1:]].append(word)

        queue = collections.deque([(beginWord, 1)])
        visited = {beginWord: True}

        while queue:
            cur_word, level = queue.popleft()
            for i in range(L):
                inter_word = cur_word[:i] + "*" + cur_word[i+1:]
                for word in dict[inter_word]:
                    if word == endWord:
                        return level + 1
                    if word not in visited:
                        visited[word] = True
                        queue.append((word, level+1))
                dict[inter_word] = []
        return 0
            
sol = Solution()
sol.ladderLength("hit","cog", ["hot","dot","dog","lot","log","cog"])
```
M: 각 단어의 길이 / N: WordList의 갯수
### 시간복잡도: O(M^2\*N)

### 공간복잡도: O(M^2*N)
{: .fs-3 .pt-2 .pb-2 }
