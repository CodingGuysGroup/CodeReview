## `Problem explain`
Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.

An integer a is closer to x than an integer b if:

- |a - x| < |b - x|, or
- |a - x| == |b - x| and a < b
 
 
## `Example 1:`

        Input: arr = [1,2,3,4,5], k = 4, x = 3
        Output: [1,2,3,4]

## `Example 2:`

        Input: arr = [1,2,3,4,5], k = 4, x = -1
        Output: [1,2,3,4]

## `Constraints:`

        1 <= k <= arr.length
        1 <= arr.length <= 104
        arr is sorted in ascending order.
        -104 <= arr[i], x <= 104
     
--- 
### `ANS`
```python
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        left, right = 0, len(arr) - k  # k 요소를 포함하는 구간의 시작과 끝 위치
        while left < right:
            mid = (left + right) // 2  # 이진 탐색을 사용하여 x의 위치를 찾기
            if x - arr[mid] > arr[mid + k] - x:
                left = mid + 1  # 시작 포인터를 이동
            else:
                right = mid  # 끝 포인터를 이동
        return arr[left:left+k]  # k 요소를 찾아 반환
        
        
```    
---


ㅡㅡㅡ

## Feedback
---
### 이름

1.내용
---
### 이름

1.내용
