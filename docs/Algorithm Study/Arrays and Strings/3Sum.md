---
layout: default
title: 3Sum
parent: Arrays and Strings
grand_parent: Algorithm Study
description: "3Sum"
permalink: /algorithm-study/arrays-and-strings/3sum
---

## LeetCode 15. 3Sum
### 링크
- [https://leetcode.com/problems/3sum/](https://leetcode.com/problems/3sum/)

<img width="945" alt="image" src="https://user-images.githubusercontent.com/39396725/196612888-1f346196-a192-4991-beba-bd3aaaa7c228.png">


제약조건
- 3 <= nums.length <= 3000
- -105 <= nums[i] <= 105

### 풀이방법
세개의 숫자를 더해서 0이 되는 경우를 찾으면 된다. 나도 처음에 생각한 방법이 일단 배열을 정렬하고, 2Sum 풀이를 응용해서 두개 합이 target value가 되는것으로 찾으려 했다.
구현이 일단 어려웠고 (잘 안되었고) 중복인 경우에 대해서 어떻게 처리하는지 잘 모르겠어서 어려웠던것 같다. 
해결책 -> nums 배열을 정렬하고, 투포인터를 사용하는데, lo, hi를 (배열의 처음과 끝)을 가리키게 하고 둘이 만나기 전까지 포인터를 조절하며 값을 찾는다. 
또한 중복 제거를 위해 nums[lo], nums[lo-1]을 비교한 로직을 두군데나 추가한것도 눈여겨 봐야겠다. 

### 코드 
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        
        for i in range(len(nums)):
            if nums[i] > 0:
                break
            
            if i == 0 or nums[i] != nums[i-1]:
                self.twoSum(nums, i, res)
        return res
        
        
    def twoSum(self, nums, i, res):
        lo, hi = i+1, len(nums)-1
        
        while lo < hi:
            sum = nums[i] + nums[lo] + nums[hi]
            
            if sum < 0:
                lo += 1
            elif sum > 0:
                hi -= 1
            else:
                res.append([nums[i], nums[lo], nums[hi]])
                lo += 1
                hi -= 1
                while lo < hi and nums[lo] == nums[lo-1]:
                    lo += 1           
```

### 시간복잡도
O(N^2)
더 정확히 말하면 O(nlogn + n^2) 왜냐하면 sorting에 nlogn이 걸리지만, n^2이 월등히 큼으로 근사하면 O(n^2)

### 공간복잡도
O(logn) ~ O(n), sorting 알고리즘의 구현에 따라 달라짐 
