### `문제 설명`

홍준이는 요즘 주식에 빠져있다. 그는 미래를 내다보는 눈이 뛰어나, 날 별로 주가를 예상하고 언제나 그게 맞아떨어진다. 매일 그는 아래 세 가지 중 한 행동을 한다.

1. 주식 하나를 산다.

2. 원하는 만큼 가지고 있는 주식을 판다.

3. 아무것도 안한다.

홍준이는 미래를 예상하는 뛰어난 안목을 가졌지만, 어떻게 해야 자신이 최대 이익을 얻을 수 있는지 모른다. 따라서 당신에게 날 별로 주식의 가격을 알려주었을 때, 최대 이익이 얼마나 되는지 계산을 해달라고 부탁했다.

예를 들어 날 수가 3일이고 날 별로 주가가 10, 7, 6일 때, 주가가 계속 감소하므로 최대 이익은 0이 된다. 그러나 만약 날 별로 주가가 3, 5, 9일 때는 처음 두 날에 주식을 하나씩 사고, 마지막날 다 팔아 버리면 이익이 10이 된다.

---

### INPUT EXAMPLE

입력의 첫 줄에는 테스트케이스 수를 나타내는 자연수 T가 주어진다. 각 테스트케이스 별로 첫 줄에는 날의 수를 나타내는 자연수 N(2 ≤ N ≤ 1,000,000)이 주어지고, 둘째 줄에는 날 별 주가를 나타내는 N개의 자연수들이 공백으로 구분되어 순서대로 주어진다. 날 별 주가는 10,000이하다.

EX1)

#INPUT
```
3
3
10 7 6
3
3 5 9
5
1 1 3 1 2
```
#OUTPUT
```
0
10
5
```
----

### `ANS`

```python
import sys

input = sys.stdin.readline

T = int(input())


def stock(day_stock):
    ans = 0

    day_len = len(day_stock)
    maxstock = 0
    maxidx = 0
    for i in range(day_len):
        if maxstock < day_stock[i]:
            maxstock = day_stock[i]
            maxidx = i

    idx = 0
    while True:
        if maxidx == 0:
            break
        sumstock = sum(day_stock[idx:maxidx])
        prevlen = len(day_stock[idx:maxidx])
        ans += (maxstock * prevlen - sumstock)
       # print("최대 주가*지난 날 = {}*{} - 지니고있는 주가 = {}, ".format(maxstock, prevlen, sumstock))

        idx = maxidx + 1
        if idx == day_len:
            break
        maxstock = 0
        maxidx = 0
        for i in range(idx, day_len):
            if maxstock < day_stock[i]:
                maxstock = day_stock[i]
                maxidx = i

    return ans


'''
    day_stock[0:maxidx]
    print(max(day_stock))
    ans = 0
    for i in range(len(day_stock)):
        if len(have_stock) == 0:  # 주식이 없을 때
            maxval = max(day_stock[i:len(day_stock)])
            if day_stock[i] < maxval:
                have_stock.append([day_stock[i], day_stock.index(maxval)])
        else:  # 주식이 있을 때
            maxval = max(day_stock[i:len(day_stock)])
            if day_stock[i] < maxval:
                have_stock.append([day_stock[i], day_stock.index(maxval)])
            elif i == have_stock[0][1]:
                while len(have_stock) != 0:
                    tmpstock = have_stock.popleft()
                    ans += (day_stock[i] - tmpstock[0])
    return ans
'''
# buy
# sell
# donot


for i in range(T):
    N = int(input())
    day = list(map(int, input().split()))
    print(stock(day))




```


### FeedBack
---
#### 이름

---
#### 이름
