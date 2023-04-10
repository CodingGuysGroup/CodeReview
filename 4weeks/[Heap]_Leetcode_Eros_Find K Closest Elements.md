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


그 다음 x에 mid를 뺀 값과 mid+k에 x를 뺀 값을 비교

공부중..(너무 어렵다)





---
### 상우

1. 이진 탐색을 이용하여 접근한 것이 이상적임 
2. right을 right부터 k만큼이 답이 될 수 있으므로 indexerror 를 피하기 위해 right=len(arr)-k 로 설정한 것과 mid 를 구하고 mid 에서 k 만큼 떨어진 곳과의 x 거리를 비교하여 left 가 더 크면 mid 바로 오른쪽에, right 가 더 크면 mid 값으로 옮겨 구하는 개수인 k를 유지시킨채 x값과 가깝게 이동시킨 점이 굉장히 신선했고 나로썬 생각하지 못했음
3. left 와 right를 최대한 x 값과 가깝게 이동시키고 left,right 값이 같거나 right 보다 left 가 더 크면 x에 최대한 가까워 진것으로 판단하고 left 부터 k만큼 슬라이싱하여 리턴한 것도 인상적임
4. 이진 탐색을 이용하면 while 문 하나로 구할 수 있기 때문에 heap 을 사용했을 때 보다 훨씬 빨라 이 방법을 좀 더 공부해볼 필요가 있다고 생각함

