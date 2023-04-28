```python

import functools
# 숫자 두 개를 이어붙인 문자열을 비교하여 큰 수가 먼저 오도록 하는 함수
def compare(a, b):
    return int(b+a) - int(a+b)

def solution(numbers):
    if len(numbers)==1 and numbers[0]==0:
        return 0
    
    # 입력으로 받은 배열의 모든 요소를 문자열로 변환
    numbers = list(map(str, numbers))
    # 비교 함수를 cmp_to_key() 함수를 이용해 키 함수로 변환하여, 문자열 배열을 정렬
    numbers = sorted(numbers, key=functools.cmp_to_key(compare))
    # 문자열 배열의 모든 요소를 이어붙인 후, 다시 정수형으로 변환한 뒤 문자열로 변환하여 반환 (정수형으로 변환안하면 테스크 케이스 11번만 계속 에러)
     
    # return str(''.join(numbers))

    return str(int(''.join(numbers)))
    
  ```
  
---

## Feedback
---
### 이름


---
### 이름
