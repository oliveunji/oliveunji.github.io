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
dp를 이용하여 i=0 부터 인덱스 마지막 값 까지 범위를 넓혀가며, 해당 인데스일때 palindrome이 어디까지 될 수 있는지 조사하고
길이가 가장 긴 결과를 리턴한다. 

### 코드 
```python
class Solution:
    def longestPalindrome(self, s):
        res = ""
        for i in range(len(s)):        
            odd  = self.palindromeAt(s, i, i)
            even = self.palindromeAt(s, i, i+1)

            res = max(res, odd, even, key=len)
        return res

    # starting at l,r expand outwards to find the biggest palindrome
    def palindromeAt(self, s, l, r):    
        while l >= 0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        return s[l+1:r]
```

### 시간복잡도
O(N^2)

### 공간복잡도
O(N^2)
