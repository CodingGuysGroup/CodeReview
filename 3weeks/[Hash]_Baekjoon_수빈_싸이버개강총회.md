```python
import sys
input = sys.stdin.readline
S, E, Q = map(str, input().split())

def TimeToFloat(time):
    idx = time.index(":")
    h = time[:idx]
    m = time[idx+1:]
    hm = h + '.' + m
    hm = float(hm)
    return hm

# 입장, 퇴장이 각각 이루어져야 하므로 사전에 중복되어 있어야 함

dict = {}
S = TimeToFloat(S)
E = TimeToFloat(E)
Q = TimeToFloat(Q)

# 입장과 퇴장이 이루어진 학생만 셈함
Attend = 0

try:  # 입력 테스트 케이스가 정해져있지 않기 때문에 try, catch
    while True:
        T, N = map(str, input().split())
        T = TimeToFloat(T)
        if dict.get(N, 0) == 0:  # 사전에 없으면(입장)
            if T <= S:  # 개총 시작한 시간 이전 출석 or 시작하자마자 출석
                dict[N] = T
        else:  # 사전에 있다면(퇴장)
            if E <= T and T <= Q:  # 개강총회를 끝내자마자 or 끝내고 나서 스트리밍 까지 퇴장
                #  or 스트리밍이 끝나자마자 퇴장
                del (dict[N])
                Attend += 1
except:  # 입력값 없이 while문을 들어갈 경우 오류발생
    print(Attend)
    exit(0)


```

문제의 입력 케이스인 학생의 입장, 퇴장 시간(10:30)들이 string으로 들어오는 것을 파악한 후 해당 시간 문자열들을 ':'를 기준으로 소수로 만드는 함수를 미리 선언한 뒤 풀이하였음

상우 형의 코드 리뷰 말대로 소수가 아닌 정수형으로 바꿔 풀이하였다면 성능이 조금 좋아졌을 것이라고 판단됨


ㅡㅡㅡ

## Feedback
---
### 이름

1.내용

---
### 이름

1.내용
