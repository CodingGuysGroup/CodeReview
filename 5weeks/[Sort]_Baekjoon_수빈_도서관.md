```python
from collections import deque
import sys
input = sys.stdin.readline
N, M = map(int, input().split())  # 책의 개수 N, 들수 있는 책의 개수 M

ploc = list(map(int, input().split()))  # 책의 위치(랜덤한), 책의 양수 위치만 담을 배열

ploc.sort()  # 책의 위치를 음수부터 양수까지 순서대로
ploc = deque(ploc)  # popleft를 쓰기 위함
mloc = []  # 책의 음수 위치만 담을 배열

while True:
    if len(ploc) == 0:  # ploc에 있는 모든 수가 mloc으로 넘어감 -> 모든 책의 위치가 음수
        break

    if ploc[0] < 0:  # ploc에 있는 수가 음수면 ploc에서 빼고 mloc에 넣음
        mloc.append(abs(ploc.popleft()))  # 음수는 절댓값 취해서 mloc에 넣음
    else:  # ploc[0]이 양수면 mloc에 안넣어도 되서 빠져나옴
        break

mloc.sort()  # -에 절댓값을 붙여 배열에 넣었으므로 작은수부터 큰수를 보이기 위해 정렬
mloc = deque(mloc)

# 만약 입력값이 -18 -9 -4 50 22 -26 40 -45일 경우
# 먼저 정렬된 후 -> [-39, -37, -29, -28, -6, 2, 11]

# 다음과 같이 ploc, mloc으로 나누어진다.
# print(ploc) # ploc : [2,11]
# print(mloc) # mloc : [6,28,29,37,39]

# ploc : [2,11]
# mloc : [6,28,29,37,39]
# M = 2
# 각 배열의 마지막 수(마지막 책의 위치)가 작은것에 대한 배열에 대하여 먼저 책을 갖다놓음
# ploc[-1] : 11 < mloc[-1] : 39 => 양수 위치(ploc)의 책들을 먼저 갖다놓는다.

# 왜냐면 ploc의 끝 11을 왕복하는 것이 mloc의 끝 39를 왕복하는 것 보다 더 최소의 이동이기 때문임

# 이는 아래의 코드로 구현되어 있음
'''
elif ploc[-1] < mloc[-1]:
    ans += getMoveLen(ploc, True) # 양수위치의 책을 먼저 놓으러 감, True는 다시 돌아와서 음수 책을 찾으러 가기 위
    ans += getMoveLen(mloc, False)# 그 다음 음수위치의 책을 놓으러 감, False는 책을 모두 놓았으므로 안돌아와도 된다는 의미
elif ploc[-1] >= mloc[-1]:
    ans += getMoveLen(mloc, True)
    ans += getMoveLen(ploc, False)
'''

# ploc -> 2랑 11들고 11갔다 0으로 복귀(11+11) 22

# mloc -> 6들고 6갔다 0으로 복귀 (6+6) 22+12
# 28,29들고 29로 이동했다 0으로 복귀 (29+29) 34+58
# 37,39들고 39로 이동(39) 92+39 = 131


def getMoveLen(loc, ret):
    # ret이 True 면 책을 다 갖다놓고도 0으로 오는 거리를 세야함
    lenloc = len(loc)
    rembook = lenloc % M  # 총 책의 개수에 들고갈 수 있는 책의 개수를 mod해서 나온 나머지 개수만큼만 들고 처음에만 왕복
    # 예를들어 책이 총 10개있고 들고갈 수 있는 책의 총 개수(M)가 3일 경우 rembook은 1이며 havebook은 1개만 책을 들고 놓고 옴, 그 다음 3개씩 3번 반복
    # 책이 9개 있고 들고갈 수 있는 책의 총 개수(M)가 3일 경우 rembook은 0이며 havebook은 3개씩 3번 반복하면 됨
    havebook = 0
    if rembook != 0:
        havebook = rembook
    else:
        havebook = M

    prevloc = loc.popleft()  # 책을 하나 들었음
    movlen = prevloc # 책을 놓으러 움직인 거리
    havebook -= 1 # 책하나 놓았음

    while loc:
        move = 0
        if havebook > 0: # 가지고 있는 책이 1개 이상이면 더 움직임
            move = loc[0] - prevloc
            movlen += move 
            prevloc = loc.popleft() 
            havebook -= 1 
        else:  # 책을 다 가져다 놓으면 M개의 책 가지러 0으로 복귀
            #print("책을 가지러 0으로 이동")
            movlen += prevloc  # 0으로 가져다 놓으러 이동하는 거리
            prevloc = 0  # 0에 도착
            havebook = M
    if ret == True:
        movlen += prevloc
    #print("movlen : {}, prevloc : {}".format(movlen, prevloc))
    return movlen


ans = 0
if len(ploc) == 0:  # 양수 배열이 비었음
    #print("모두 음수")
    ans += getMoveLen(mloc, False)
elif len(mloc) == 0:  # 음수 배열이 비었음
    #print("모두 양수")
    ans += getMoveLen(ploc, False)
elif ploc[-1] < mloc[-1]:
    ans += getMoveLen(ploc, True)
    ans += getMoveLen(mloc, False)
elif ploc[-1] >= mloc[-1]:
    ans += getMoveLen(mloc, True)
    ans += getMoveLen(ploc, False)

print(ans)


```

ㅡㅡㅡ

## Feedback
---
### Eros

1. 

---
### 상우

1. 
