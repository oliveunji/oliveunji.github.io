---
layout: default
title: Decode String
parent: Trees and Graphs
grand_parent: Algorithm Study
description: "Decode String"
permalink: /algorithm-study/trees-and-graphs/decode-string
---

## LeetCode 394. Decode String
### 링크
- [https://leetcode.com/problems/decode-string/](https://leetcode.com/problems/decode-string/)

<img width="721" alt="image" src="https://user-images.githubusercontent.com/39396725/198014436-ac4d85e4-9f41-4d28-a70b-50c794cd0f8e.png">

### 제약조건
- 1 <= s.length <= 30
- s consists of lowercase English letters, digits, and square brackets '[]'.
- s is guaranteed to be a valid input.
- All the integers in s are in the range [1, 300].

### 풀이방법
Stack을 이용하여 아주 우아하게 풀 수 있다.. 뭔가 비슷하게 생각했지만, 어떻게 stack을 관리하고  대괄호가 열리고 닫힐때 stack에 있는 값들을 효과적으로 꺼내서 계산할지 
구현하지 못했다.. 구글에 다니시는 고수님의 아름다운 코드를 외우기로 결심했다... 

### 코드
```python
class Solution:
    def decodeString(self, s: str) -> str:
        stack = []
        curString = ''
        curNum = 0
        
        for c in s:
            if c == '[':
                stack.append(curString)
                stack.append(curNum)
                curString = ''
                curNum = 0
            elif c == ']':
                num = stack.pop()
                prevString = stack.pop()
                curString = prevString + num * curString
            elif c.isdigit():
                curNum = curNum*10 + int(c)
            else:
                curString += c
        return curString
```

### 시간복잡도 & 공간복잡도
<img width="675" alt="image" src="https://user-images.githubusercontent.com/39396725/198020330-dc1ce71b-b585-4527-b170-25219f0d5914.png">
