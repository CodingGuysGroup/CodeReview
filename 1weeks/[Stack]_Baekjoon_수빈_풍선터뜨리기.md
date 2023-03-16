
```python
N = int(input())
Balloon = list(map(int, input().split()))  # 띄어쓰기로 분류하여 문장을 배열로 입력받음

Ballist = []  # 풍선에 번호를 부여하기 위한 이중 배열

for i in range(len(Balloon)):
    Ballist.append([i+1, Balloon[i]])  # 풍선에 번호 부여
    # [EX]
    # 5
    # 3 2 1 -3 -1
    # [[1, 3], [2, 2], [3, 1], [4, -3], [5, -1]]
    # 각 List의 0번 째 인덱스는 풍선번호 1번 째 인덱스는 이동할 거리를 의미함

Boomnum = []  # 터진 풍선의 번호 순서를 담을 배열


def Cutlen(S):
    if S < 0:
        S += len(Ballist)  # S 위치가 음수일 경우 풍선의 총 갯수와 더해서 인덱스를 양수로 치환함(추후 설명)

    Move = Ballist[S][1]  # S 위치의 풍선이 이동할 거리

    print(Ballist, end=" ")
    print("S : {}".format(S))
    Boomnum.append(Ballist[S][0])  # 터진 풍선의 순서를 저장할 배열
    Ballist.pop(S)  # S 위치의 풍선 터뜨리기
    Balnum = len(Ballist)  # 터진 풍선을 제외한 나머지 풍선의 개수

    if Balnum == 1:  # 풍선이 한개 남았을 경우 함수 탈출
        Boomnum.append(Ballist[0][0])
        Ballist.pop(0)
        return 0

    if Move > 0:  # 이동거리가 양수라면

        Move += S  # 현재위치 S + 이동거리 Move를 더해서 Move에 저장

        if Move > Balnum:  # 이동거리가 풍선 개수 이상일 경우

            rem = Move % Balnum
            # 이동거리에 풍선의 개수를 나눈 나머지
            return rem - 1  # 1을 빼주는 이유는 풍선이 하나 터졌으므로
        else:  # move < ballen
            return Move - 1
    elif Move < 0:  # 종이에 적힌 수가 음수면 왼쪽으로 move
        # [2,1,-3,-1] => S = 2  / [2,1,-1] / move = -3
        Move += S
        if abs(Move) > Balnum:
            rem = Move % Balnum
            print("{} % {} = {} ".format(Move, Balnum, rem))
            return rem
        print(Move)
        return Move


S = int(0)  # 첫번째 풍선 터뜨리기
S = int(Cutlen(S))
while len(Ballist) != 0:  # 이후 풍선이 다 터질때까지 while 반복문 시행
    S = int(Cutlen(S))

for i in range(len(Boomnum)):  # 출력 조건을 맞추기 위한 반복문
    if i == len(Boomnum) - 1:
        print(Boomnum[i])
        break
    print(Boomnum[i], end=" ")


```
## Feedback
---
### 상우
- Ballist 배열을 2차원 리스트가 아닌 1차원 리스트로 만들고 순서에 대한 리스트를 따로 만드는 것이 시간 측면이나 메모리 측면에서 좋아보임
- Move 변수에 대한 조건문도 pop을 잘 활용하여 간단한 계산식으로 만들어 가독성,간결성을 높일 수 있을 것으로 보임
- 좀 길지만 어떻게든 결과를 도출하는 부분이 인상적임


---
