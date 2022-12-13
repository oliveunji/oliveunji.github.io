---
layout: default
title: List of Products of all Elements
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "List of Products of all Elements"
permalink: /algorithm-study/arrays-and-strings/list-of-products-of-all-elements
---

## educative Challenge 4: List of Products of all Elements
### 링크
- [https://www.educative.io/module/lesson/data-structures-in-python/qVLrzVE40E2](https://www.educative.io/module/lesson/data-structures-in-python/qVLrzVE40E2)

<img width="734" alt="image" src="https://user-images.githubusercontent.com/39396725/207463240-04fbec59-ea89-4fbc-a6e2-4b1860bac303.png">

### 풀이방법
원래 생각했던것은 전체 곱을 구한다음에 다시한번 돌면서 해당 값 나눠주는 방식으로 (0은 따로 예외처리) 풀었는데,
이보다 더 신박한 방법이 있었다.
왼쪽부터 시작해서 곱하는거랑, 오른쪽부터 시작해서 곱한 결과를 다시 곱하면 그 결과가 나온다. 

<img width="355" alt="image" src="https://user-images.githubusercontent.com/39396725/207464258-0b3b4a70-8eeb-4083-b4c9-0914f18de52d.png">

### 코드 
```python
def find_product(lst):
    left = 1
    result = []
    for elem in lst:
        result.append(left)
        left *= elem

    right = 1
    for i in range(len(lst)-1, -1, -1):
        result[i] *= right
        right *= lst[i]
    return result    
```

### 시간복잡도
O(N)

### 공간복잡도
O(N)
