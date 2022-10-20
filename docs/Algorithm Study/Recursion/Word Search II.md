---
layout: default
title: Word Search II
parent: Recursion
grand_parent: Algorithm Study
description: "Word Search II"
permalink: /algorithm-study/recursion/word-search-II
---

## LeetCode 212. Word Search II
### 링크
- [https://leetcode.com/problems/word-search-ii/](https://leetcode.com/problems/word-search-ii/)

<img width="518" alt="image" src="https://user-images.githubusercontent.com/39396725/196926790-66849118-22ca-41f3-8eb1-7790273c2c4c.png">

제약조건
- m == board.length
- n == board[i].length
- 1 <= m, n <= 12
- board[i][j] is a lowercase English letter.
- 1 <= words.length <= 3 * 104
- 1 <= words[i].length <= 10
- words[i] consists of lowercase English letters.
- All the strings of words are unique.

### 풀이방법
1. Words 단어들을 Trie로 구성한다.
<img width="510" alt="image" src="https://user-images.githubusercontent.com/39396725/196927158-e3ea4d0b-5aef-467d-bcc9-ecedcdc795b8.png">
2. board를 돌면서 지금해당 문자로 시작하는 단어가 trie에 존재하면, backtracking 기법 (DFS)로 끝까지 닿을수 있는지? (Trie에 정의된 단어가 실제 존재하는지?) 탐색하고, 
존재하는 경우 결과 배열에 추가한다. 
3. Optimization 코드도 무척 중요하다. 해당 단어에 대한 검색이 끝났으면, pop을 통해 dfs 탐색시 가지치기를 한다 
<img width="469" alt="image" src="https://user-images.githubusercontent.com/39396725/196927858-7b97f89d-3a9f-4fc5-9974-3457e6e6562b.png">

### 코드 
```python
class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        WORD_KEY = '$'
        
        trie = {}
        for word in words:
            node = trie
            for letter in word:
                # retrieve the next node; If not found, create a empty node.
                node = node.setdefault(letter, {})
            # mark the existence of a word in trie node
            node[WORD_KEY] = word
        
        rowNum = len(board)
        colNum = len(board[0])
        
        matchedWords = []
        
        def backtracking(row, col, parent):    
            
            letter = board[row][col]
            currNode = parent[letter]
            
            # check if we find a match of word
            word_match = currNode.pop(WORD_KEY, False)
            if word_match:
                # also we removed the matched word to avoid duplicates,
                #   as well as avoiding using set() for results.
                matchedWords.append(word_match)
            
            # Before the EXPLORATION, mark the cell as visited 
            board[row][col] = '#'
            
            # Explore the neighbors in 4 directions, i.e. up, right, down, left
            for (rowOffset, colOffset) in [(-1, 0), (0, 1), (1, 0), (0, -1)]:
                newRow, newCol = row + rowOffset, col + colOffset     
                if newRow < 0 or newRow >= rowNum or newCol < 0 or newCol >= colNum:
                    continue
                if not board[newRow][newCol] in currNode:
                    continue
                backtracking(newRow, newCol, currNode)
        
            # End of EXPLORATION, we restore the cell
            board[row][col] = letter
        
            # Optimization: incrementally remove the matched leaf node in Trie.
            if not currNode:
                parent.pop(letter)

        for row in range(rowNum):
            for col in range(colNum):
                # starting from each of the cells
                if board[row][col] in trie:
                    backtracking(row, col, trie)
        
        return matchedWords    
```

### 시간복잡도
O(M(4\*3^L-1))

### 공간복잡도
O(N)
