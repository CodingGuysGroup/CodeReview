### `문제 설명`

프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

### `제한 사항`

- 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
- 작업 진도는 100 미만의 자연수입니다.
- 작업 속도는 100 이하의 자연수입니다.
- 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.


### `결과`

배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

### `입출력 예`

### Case 1

|progresses|speeds|return|
|---|---|---|
|93,30,55|1,30,5|2,1|

#### Explanation

첫 번째 기능은 93% 완료되어 있고 하루에 1%씩 작업이 가능하므로 7일간 작업 후 배포가 가능합니다.

두 번째 기능은 30%가 완료되어 있고 하루에 30%씩 작업이 가능하므로 3일간 작업 후 배포가 가능합니다. 하지만 이전 첫 번째 기능이 아직 완성된 상태가 아니기 때문에 첫 번째 기능이 배포되는 7일째 배포됩니다.

세 번째 기능은 55%가 완료되어 있고 하루에 5%씩 작업이 가능하므로 9일간 작업 후 배포가 가능합니다.

따라서 7일째에 2개의 기능, 9일째에 1개의 기능이 배포됩니다.

### Case2

|progresses|speeds|return|
|---|---|---|
|95,90,99,99,80,99|1,1,1,1,1,1|1,3,2|

#### Explanation

모든 기능이 하루에 1%씩 작업이 가능하므로, 작업이 끝나기까지 남은 일수는 각각 5일, 10일, 1일, 1일, 20일, 1일입니다. 어떤 기능이 먼저 완성되었더라도 앞에 있는 모든 기능이 완성되지 않으면 배포가 불가능합니다.

따라서 5일째에 1개의 기능, 10일째에 3개의 기능, 20일째에 2개의 기능이 배포됩니다.

모든 기능이 하루에 1%씩 작업이 가능하므로, 작업이 끝나기까지 남은 일수는 각각 5일, 10일, 1일, 1일, 20일, 1일입니다. 어떤 기능이 먼저 완성되었더라도 앞에 있는 모든 기능이 완성되지 않으면 배포가 불가능합니다.

따라서 5일째에 1개의 기능, 10일째에 3개의 기능, 20일째에 2개의 기능이 배포됩니다.

----

### `ANS`
```

def Calu(X, Y): # 필요한 작업일 수를 구하는 함수
    Cnt=0
    while X<100:
        X+=Y
        Cnt+=1
    return Cnt
def solution(Progresses, Speeds):
    Answer = [] # 결과를 담을 리스트
    Stack = [] # 필요한 작업일 수를 담을 리스트
    Stack.append(Calu(Progresses[0],Speeds[0])) # 첫 작업일 수 삽입
    Cnt = 1 # 작업 가능한 기능 개수
    for i in range(1,len(Progresses)):
        # 현재 스택의 최댓값이 방금 들어온 작업일 수보다 크면
        if max(Stack) >= Calu(Progresses[i],Speeds[i]): 
            # 아직 최대 작업일 수를 끝내지 않았으므로 Cnt+1하고 스택에 삽입
            Cnt += 1 
            Stack.append(Calu(Progresses[i],Speeds[i]))
        else:
            # 현재 스택의 최댓값이 방금 들어온 작업일 수보다 작으면
            # 최대 작업일 수가 작업 종료되므로 스택에 쌓였던 작업일 수도 자동적으로 완료됨
            Answer.append(Cnt) #현재까지 카운트 했던 Cnt 값 결과 리스트에 담음
            for _ in range(Cnt): 
                Stack.pop() # 현재 Cnt값은 Stack의 길이와 같으므로 pop과 Cnt을 이용하여 스택 비움
            Stack.append(Calu(Progresses[i],Speeds[i])) # 방금 들어온 작업일 수 스택에 넣음
            Cnt = 1 # Cnt 초기화
    Answer.append(len(Stack)) # for 문이 끝나고 남아있는 스택의 개수만큼 결과 리스트에 삽입(언젠간 완료됨)
    while Stack: # 스택 비움
        Stack.pop()
    return Answer # 결과 리스트 


```
## Feedback
---
### Eros 
- 이 문제에서 여러번 사용될 계산을  `Calu()` 함수로 따로 만들었는데 아주 효율적임
- 그리고 마지막으로 stack을 전부다 비우는 것도 정석


---
### 수빈
- 필요한 작업량을 구하는 수식을 Calu 함수를 작성하여 코드의 가독성을 좋게 만든 것 같음
- 조건문을 통해 최댓값을 기준으로 빠른 배포일, 늦은 배포일을 나눈 알고리즘이 나와 똑같기 때문에 코드 리뷰를 다시 하며 내가 풀었던 알고리즘도 복기할 수 있었음 
