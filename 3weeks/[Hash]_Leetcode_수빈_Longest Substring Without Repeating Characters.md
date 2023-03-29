```python
from collections import deque

# 사전에 치환되는 로마자를 넣음
roman = {}
roman[1] = 'I'
roman[5] = 'V'
roman[10] = 'X'
roman[50] = 'L'
roman[100] = 'C'
roman[500] = 'D'
roman[1000] = 'M'

deq = deque()
def setRoman(sym, temp):
    # 1994
    # 4(5), 90(50), 900(500), 1000(5000)
    if temp / (5*sym) == 1: # 5,6,7,8,9
        if temp % (5*sym) == 4*sym: # 9(IX)
            deq.append(roman[sym]) # I
            deq.append(roman[temp+sym]) # X
        else:
            deq.append(roman[5*sym])
            temp %= 5*sym # 5,6,7,8
            temp /= sym 
            for i in range(temp):
                deq.append(roman[sym])
    else: # 1,2,3,4,10(*sym)
        if temp % (5*sym) == 4*sym: # 4(IV)
            deq.append(roman[sym])
            deq.append(roman[temp + sym])
        else: # 1,2,3
            temp /= sym # 20,30, 1000
            for i in range(temp):
                deq.append(roman[sym])

class Solution(object):
    def intToRoman(self, num):
        sym = 1
        temp = 0
        # 1994 => 4, 90, 900, 1000 반대로 나오게
        # 1994 => 1000, 900, 90, 4
        # 58 => 50, 8
        temparray = deque()
        while num != 0:
            temp = num % 10 * sym
            temparray.appendleft([sym,temp])
            sym *= 10
            num /= 10

        for i in temparray:
            # 1000
            # 900
            # 90
            # 4 
            # 에 대한 로마숫자를 전역 deq에 담는 함수
            setRoman(i[0],i[1])

       # print(deq)

        retstr = ""
        for i in deq:
            retstr += i

        deq.clear()
        
        return retstr
        
        # I=1 / IV = 4, IX = 9 , XLIX = 49
        # X=10 / XL = 40, XC = 90
        # C=100 / CD = 400, CM = 900

```

코드가 다소 길게 작성될 수 있음을 로마자를 설정하는 setRoman()함수를 별도로 만들어 로마자를 관리하려 하였음


다만 코드 리뷰 도중 사전에 기본 로마자가 아닌 특수한 로마자 심볼(4,9,40,90..)등을 선언하여 문제풀이를 진행하는 것이 더 효율적이었다고 느끼게 됨

ㅡㅡㅡ

## Feedback
---
### 이름

1.내용

---
### 이름

1.내용
