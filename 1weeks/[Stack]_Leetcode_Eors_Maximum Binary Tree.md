## `Problem description`

You are given an integer array nums with no duplicates. A maximum binary tree can be built recursively from nums using the following algorithm:

Create a root node whose value is the maximum value in nums.

Recursively build the left subtree on the subarray prefix to the left of the maximum value.

Recursively build the right subtree on the subarray suffix to the right of the maximum value.

Return the maximum binary tree built from nums.

## `Input and output example`

![](https://assets.leetcode.com/uploads/2020/12/24/tree1.jpg)

        Input: nums = [3,2,1,6,0,5]
        Output: [6,3,5,null,2,0,null,null,1]
        Explanation: The recursive calls are as follow:
        - The largest value in [3,2,1,6,0,5] is 6. Left prefix is [3,2,1] and right suffix is [0,5].
            - The largest value in [3,2,1] is 3. Left prefix is [] and right suffix is [2,1].
                - Empty array, so no child.
                - The largest value in [2,1] is 2. Left prefix is [] and right suffix is [1].
                    - Empty array, so no child.
                    - Only one element, so child is a node with value 1.
            - The largest value in [0,5] is 5. Left prefix is [0] and right suffix is [].
                - Only one element, so child is a node with value 0.
                - Empty array, so no child
                
![](https://assets.leetcode.com/uploads/2020/12/24/tree2.jpg)

          Input: nums = [3,2,1]
          Output: [3,null,2,null,1] 
          
---
## "문제 설명"

중복되지 않은 정수 배열 번호가 제공됩니다. 최대 이진 트리는 다음 알고리즘을 사용하여 숫자에서 재귀적으로 만들 수 있습니다:

값이 num 단위의 최대값인 루트 노드를 만듭니다.

최대 값의 왼쪽에 있는 하위 배열 접두사에 왼쪽 하위 트리를 재귀적으로 작성합니다.

최대 값의 오른쪽에 있는 하위 배열 접미사에 오른쪽 하위 트리를 재귀적으로 작성합니다.

숫자에서 작성된 최대 이진 트리를 반환합니다.

---
## `ANS`

```python
class Solution:
    def constructMaximumBinaryTree(self, nums):
        if not nums: 
            return None
        # 제일 큰 수를  ROOT로 선정 
        Root = TreeNode(max(nums))
        # 왼쪽 트리 구성
        Root.left = self.constructMaximumBinaryTree(nums[:nums.index(max(nums))])
        # 오른쪽 트리 구성
        Root.right = self.constructMaximumBinaryTree(nums[nums.index(max(nums))+1:])
        return Root
```
![image](https://user-images.githubusercontent.com/86946575/224702328-b73f01d5-ff8e-4890-b682-768d65bf4c36.png)

## Feedback
---
### 상우
- 재귀 함수를 이용하여 간단하게 코드를 구성한 것이 인상적임
- 재귀 후 TreeNode 함수의 자료구조를 가지는 Root 값으로 트리 구성 후 리턴하기 때문에 이 방법 외에 리스트 형태로 문제에서 요구하는 값을 넣어 리턴하는 형식으로 코드를 짜는 것도 괜찮아보임

---
### 수빈
- 문제 설명에서 언급한 재귀를 사용하여 코드를 간결화하였음
- Leetcode 상에서 노드에 대한 Class를 선언해주었으나 이진 트리 구성은 중요한 개념이므로 해당 문제에 대한 구조 자체를 암기하는 식으로 외우는게 좋아보임

