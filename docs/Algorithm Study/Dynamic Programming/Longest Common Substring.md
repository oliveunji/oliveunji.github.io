---
layout: default
title: Longest Common Substring
parent: Dynamic Programming
grand_parent: Algorithm Study
description: "Longest Common Substring"
permalink: /algorithm-study/dynamic-programming/longest-palindromic-substring
---

## LeetCode 5. Longest Common Substring
### 링크
- [https://leetcode.com/problems/longest-palindromic-substring/](https://leetcode.com/problems/longest-palindromic-substring/)

<img width="419" alt="image" src="https://user-images.githubusercontent.com/39396725/197345126-2807e95c-e08d-45ac-8941-8cf5db037fd3.png">

제약조건
- 1 <= s.length <= 1000
- s consist of only digits and English letters.

### 풀이방법
dp 결과를 저장할 min 저장용 변수와 max 저장용 변수를 따로 두고, result도 그때 그때 계산해서 업데이트 한다. 

### 코드 
```python
class Solution:
    def longestPalindrome(self, s):
    res = ""
    for i in xrange(len(s)):
        # odd case, like "aba"
        tmp = self.helper(s, i, i)
        if len(tmp) > len(res):
            res = tmp
        # even case, like "abba"
        tmp = self.helper(s, i, i+1)
        if len(tmp) > len(res):
            res = tmp
    return res
 
  # get the longest palindrome, l, r are the middle indexes   
  # from inner to outer
  def helper(self, s, l, r):
      while l >= 0 and r < len(s) and s[l] == s[r]:
          l -= 1; r += 1
      return s[l+1:r]
```

### 시간복잡도
O(N^2)

### 공간복잡도
O(N^2)
