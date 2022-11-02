---
layout: default
title: Minimum Window Substring
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "Minimum Window Substring"
permalink: /algorithm-study/arrays-and-strings/minimum-window-substring
---

## LeetCode 76. Minimum Window Substring
### 링크
- [https://leetcode.com/problems/minimum-window-substring/](https://leetcode.com/problems/minimum-window-substring/)

<img width="643" alt="image" src="https://user-images.githubusercontent.com/39396725/199428563-dc52dc50-e3b2-49e7-909e-f964e61109ad.png">


제약조건
- m == s.length
- n == t.length
- 1 <= m, n <= 105
- s and t consist of uppercase and lowercase English letters.

### 풀이방법
1. Sliding windows를 사용하여 left right를 두고, right을 증가시켜가며 비교한다
2. 현재 windows에 t의 모든 문자가 포함되어있는지 확인하는 로직이 필요하다. -> 여기서는 간단히 length를 선언해두고, 그 값이 0이 될때로 판단했다. 
3. 슬라이딩 윈도우의 범위가 중복되서 있을 수 있는데, 이걸 체크하는게 중요한데, need[s[left]] < 0 일때, need[s[left]] == 0을 만족하는 순간까지 left를 당기는 방식으로
left, right의 범위를 조절했다.
4. 가장 작은 길이의 substring을 찾아야 해서 별도로 start, end를 두고 end-start vs right-left 비교하여 end-start에는 가장 작은 길이의 substring이 유지되도록 했다. 


### 코드 
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        need = collections.Counter(t)
        missing = len(t)
        start = end = left = 0
        
        for right, char in enumerate(s,1):
            missing -= need[char] > 0
            need[char] -= 1
            
            if missing == 0:
                while left < right and need[s[left]] < 0:
                    need[s[left]] += 1
                    left += 1
                
                if not end or end - start >= right - left:
                    start, end = left, right
                    need[s[left]] += 1
                    missing += 1
                    left += 1
        return s[start:end]
```

### 시간복잡도
O(∣S∣+∣T∣)

### 공간복잡도
O(∣S∣+∣T∣)
