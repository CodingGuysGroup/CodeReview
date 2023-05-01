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
### 수빈

1. 사전형 비교를 람다를 쓰지 않고 파이썬 함수 cmp_to_key를 쓴 점이 독특하다.

*구글링 후 찾은 cmp_to_key

cmp_to_key()란 sort()나 sorted()를 사용할 때 그 안에서 정렬조건으로 넣는 그 key를 말한다. 

일반적으로는 lambda를 사용해서 비교해보고는 한다. x와 y가 '3'과 같이 str화 되어있는 숫자일 때를 감안한 compare함수(숫자가 str화 되어있을 때 사용하면 좋을 것 같은 함수)


---
### 이름
