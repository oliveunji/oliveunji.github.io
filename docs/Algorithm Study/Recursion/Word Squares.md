---
layout: default
title: Word Squares
parent: Recursion
grand_parent: Algorithm Study
description: "Word Squares"
permalink: /algorithm-study/recursion/word-squares
---

## LeetCode 425. Word Squares
### 링크
- [https://leetcode.com/problems/word-squares/](https://leetcode.com/problems/word-squares/)

<img width="571" alt="image" src="https://user-images.githubusercontent.com/39396725/196827742-d8726fa6-9227-456e-8777-00ebac99f853.png">

제약조건
- 1 <= words.length <= 1000
- 1 <= words[i].length <= 4
- All words[i] have the same length.
- words[i] consists of only lowercase English letters.
- All words[i] are unique.

### 풀이방법
일단 문제에 대해 잘 이해하고 풀수 있는 전략을 세워야 한다.
다음과 같이 정사각형모양의 word square를 만들어서 가능한 조합을 찾아낼 수 있다. 
<img width="458" alt="image" src="https://user-images.githubusercontent.com/39396725/196915009-3baa8b94-3fc0-4c8c-b26a-e451d86545a7.png">

그다음 이를 코드로 구현해야 하는데, backtracking 방식으로 step을 진행하며 조건에 충족하는지 살핀다.
<img width="504" alt="image" src="https://user-images.githubusercontent.com/39396725/196915264-c19fd7a3-54a5-48e9-9d90-13f2e2171b71.png">


### 코드 
```python
class Solution:
    def wordSquares(self, words: List[str]) -> List[List[str]]:
        self.words = words
        self.N = len(words[0])
        
        results = []
        word_squares = []
        
        for word in words:
            word_squares = [word] # try with every word as the starting word
            self.backtracking(1, word_squares, results)
        return results
    
    def backtracking(self, step, word_squares, results):
        if step == self.N:
            # when dfs runs as the length of word_squares, append the result with deep copied value
            results.append(word_squares[:])
            return 
        
        prefix = ''.join([word[step] for word in word_squares])
        for candidate in self.getWordsWithPrefix(prefix):
            word_squares.append(candidate)
            self.backtracking(step+1, word_squares, results)
            word_squares.pop()
    
    def getWordsWithPrefix(self, prefix):
        for word in self.words:
            if word.startswith(prefix):
                yield word

sol = Solution()
sol.wordSquares(["abat","baba","atan","atal"])
```

### 시간복잡도
O(N*26^N)

### 공간복잡도
O(N\*L + N\*L/2)
