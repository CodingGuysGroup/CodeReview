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
