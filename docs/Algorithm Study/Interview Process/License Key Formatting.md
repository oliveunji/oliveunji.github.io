---
layout: default
title: License Key Formatting
parent: Interview Process
grand_parent: Algorithm Study
description: "License Key Formatting"
permalink: /algorithm-study/interview-process/license-key-formatting
---

## LeetCode - License Key Formatting
### 링크
- [https://leetcode.com/explore/interview/card/google/67/sql-2/472](https://leetcode.com/explore/interview/card/google/67/sql-2/472)

<img width="798" alt="image" src="https://user-images.githubusercontent.com/39396725/197739142-24af04aa-4cb5-4583-af52-e3e6ddb375fd.png">

제약조건
- 1 <= s.length <= 105
- s consists of English letters, digits, and dashes '-'.
- 1 <= k <= 104

### 풀이방법
주어진 조건에 맞게 문자열을 잘 파싱하고, 결과값을 반환하면 되는 문제이다.
풀긴 풀었으나, 내 코드는 길고 아름답지 않아서, discussion에 있는 Awesome한 풀이를 가져왔다. 

### 코드 
```python
class Solution:
    def licenseKeyFormatting(self, s: str, k: int) -> str:
        s= s.replace('-','').upper()[::-1]
        return '-'.join(s[i:i+k] for i in range(0, len(s), k))[::-1]
```

### 시간복잡도
O(N)

### 공간복잡도
O(N)
