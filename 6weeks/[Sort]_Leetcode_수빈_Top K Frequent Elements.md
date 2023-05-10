### `Problem explain`

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

----

### `문제 설명`

정수형 배열 nums와 정수 k가 주어졌을 때, 가장 빈번한 요소를 k개로 list로 반환하라. 반환하는 list는 정렬되어있지 않아도 된다. 

----

### `Constraints`

1 <= nums.length <= 105

-104 <= nums[i] <= 104

k is in the range [1, the number of unique elements in the array].

It is guaranteed that the answer is unique.

## Example 1:

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

```
## Example 2:

```
Input: nums = [1], k = 1
Output: [1]
```
----

## `ANS`

### 사전형을 먼저 떠올리고 알고리즘을 구상하여 수월하게 문제를 풀었다.

```python
class Solution(object):
    def topKFrequent(self, nums, k):
        answer = []
        dictnums = {}
        for i in nums:
            if dictnums.get(i,-1) == -1: # 사전에 정의되지 않았을 경우
                dictnums[i] = 1
            else: # 정의되어 있을 경우
                dictnums[i] += 1
        #print(dictnums)
        freqarr = []
        for key, value in dictnums.items():
            freqarr.append([key,value])
        print(freqarr)
       
        freqarr.sort(key = lambda x : x[1], reverse=True)
        #print(enum)
        for i in range(k):
            answer.append(freqarr[0][0])
            del freqarr[0]
       
        return answer
                        
```


### FeedBack
---
#### 이름

---
#### 이름



