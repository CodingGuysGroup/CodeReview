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
### 수빈


```
left, right = 0, len(arr) - k  # k 요소를 포함하는 구간의 시작과 끝 위치
```

<img width="279" alt="image" src="https://user-images.githubusercontent.com/84978165/230080789-38bafc10-2a05-40ac-a36c-128233fa52c0.png">

배열의 0번째 인덱스에서 부터 k개의 범위를 설정하기 위해 left의 초기값은 '0'

또한 적어도 크기 k의 배열이 필요하기 때문에 right의 초기값은 '배열의 길이 - k'

right 수식의 이유는 그림처럼 right가 주어진 배열의 가능한 마지막 2개를 결정짓는 요소의 첫 인덱스가 될수 있기 때문

<br/>

```
while left < right:
            mid = (left + right) // 2  # 이진 탐색을 사용하여 x의 위치를 찾기
            if x - arr[mid] > arr[mid + k] - x:
                left = mid + 1  # 시작 포인터를 이동
            else:
                right = mid  # 끝 포인터를 이동
```

<img width="279" alt="image" src="https://user-images.githubusercontent.com/84978165/230082098-c3bb783f-2c1d-4f19-a508-cc2c6a478c27.png">

 
먼저 left과 right에 대하여 mid를 구함 

그리고 'mid[2]'와 mid에서 k만큼의 범위 우측의 'mid+k[4]' 중에 무엇이 더 x[5]에 가까운지를 비교하는 알고리즘이 바로 while문의 if문

<img width="279" alt="image" src="https://user-images.githubusercontent.com/84978165/230083493-b33a4164-a11c-41e5-9984-139950e50396.png">


그 다음 x에 mid를 뺀 값과 mid+k에 x를 뺀 값을 비교(이해가 되지 않는다)





---
### 이름

1.내용
