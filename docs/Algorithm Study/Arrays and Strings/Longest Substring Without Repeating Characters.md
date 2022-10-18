---
layout: default
title: Longest Substring Without Repeating Characters
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "Longest Substring Without Repeating Characters"
permalink: /algorithm-study/arrays-and-strings/longest-substring-without-repeating-characters
---

## LeetCode 3. Longest Substring Without Repeating Characters
### 링크
- [https://leetcode.com/problems/longest-substring-without-repeating-characters/](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

<img width="553" alt="image" src="https://user-images.githubusercontent.com/39396725/196363281-78734c3f-8156-4d05-9209-8cc782a4faa3.png">

제약조건
- 0 <= s.length <= 5 * 104
- s consists of English letters, digits, symbols and spaces.

### 풀이방법
map과 투포인터를 이용한다! 문자열을 처음부터 탐색하면서 이미 탐색한 문자의 경우, 경우에 따라 인덱스 값을 정해주고, 아닌경우 두번째 포인터를 계속 증가시키면서 max값을 계산해주다.
이 풀이의 장점은 한번 탐색으로 답을 구하는게 가능하다는 것이다. 

### 코드 
2번 방법에 대해서만 풀이하도록 하겠다. 
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        n = len(s)
        ans = 0
        i = 0
        mp = {}
        
        for j in range(n):
            if s[j] in mp:
                i = max(mp[s[j]], i)
            mp[s[j]] = j + 1
            ans = max(ans, j-i+1)
        return ans
```

### 시간복잡도
O(N)

### 공간복잡도
O(min(m,n))
