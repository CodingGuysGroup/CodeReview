## `Problem explain`

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```
---
## `ANS`

```python3
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        max_dis = 0

        while left < right:
            # 두 점을 사용하여 용기를 만들고 용량을 계산
            h = min(height[left], height[right])
            w = right - left
            # 거리 
            dis= h * w

            # 최대 용량을 갱신
            max_dis = max(max_dis, dis)

            # 높이가 낮은 쪽의 포인터를 이동
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return max_dis

```
![image](https://user-images.githubusercontent.com/86946575/237063254-48a4aeec-83db-427b-b2a3-c66d73070d6c.png)

## Feedback
---
### 수빈

---
### 상우
