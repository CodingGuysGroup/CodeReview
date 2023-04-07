### `문제 설명`

매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 
모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

### `제한 사항`

- scoville의 길이는 2 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.

### `결과`

Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

### `입출력 예`
### Case 1

|scoville|K|return|
|---|---|---|
|[1, 2, 3, 9, 10, 12]|7|2|

#### Explanation

스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5
가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]

스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13
가진 음식의 스코빌 지수 = [13, 9, 10, 12]

모든 음식의 스코빌 지수가 7 이상이 되었고 이때 섞은 횟수는 2회입니다.

### `ANS`

----

```
import heapq
def solution(scoville, K):
    answer = 0
    heapq.heapify(scoville) #scoville 리스트를 heap 구조로 변환
    if scoville[0]>=K: #이때 모든 scoville 이 K 값보다 크면 리턴
        return answer
    while True:
        first_scoville=heapq.heappop(scoville) # 첫번째 scoville pop
        second_scoville=heapq.heappop(scoville) # 두번째 scoville pop
        add_scoville=first_scoville+second_scoville*2 #추가할 scvoille 구하기
        heapq.heappush(scoville,add_scoville) # heap에 추가
        answer+=1 #개수 추가
        if scoville[0]>=K: #만약 최소 scoville이 K 값보다 크면 break
            break
        if len(scoville)==1: # scoville 개수가 1이라는 것은 결국 scoville 리스트 모두 K 값보다 작았다는 의미
            answer=-1 #따라서 answer는 -1
            break
    return answer

```

### Feedback
---
#### 수빈

내 작성코드
```
   while hq[0] < K: # 길이가 1이면
        if len(hq) == 1:
            return -1
        
        first = heapq.heappop(hq)
        second = heapq.heappop(hq)

        heapq.heappush(hq, first+second*2)
        count += 1
```
좌오 형 작성코드
```
 while heap[0] < K:  # 가장 작은 스코빌 지수가 K보다 작을 경우 반복
        # 가장 작은 스코빌 지수 두 개를 꺼내서 섞은 음식의 스코빌 지수 계산
        mixed_scoville = heapq.heappop(heap) + heapq.heappop(heap) * 2
        heapq.heappush(heap, mixed_scoville)  # 섞은 음식의 스코빌 지수를 힙(heap)에 삽입
        cnt += 1  # 섞은 횟수(count) 증가

        # 모든 음식을 섞어도 스코빌 지수가 K 이상이 되지 않으면 -1을 반환하고 종료
        if len(heap) == 1 and heap[0] < K:
            return -1
```

나와 좌오형의 반복문을 빠져나오는 조건 또한 거짓이면 while을 빠져나오는 조건이므로 상우형의 if scoville[0]>=K: break과 다를게 없다.

이번 문제는 제시되어있는 입력값이나 문제 설명이 명확했으므로 세명의 알고리즘에 공통된 부분이 많은 것을 확인할 수 있었다.


---
#### Eros
 - 상세하고 쉬운 주석이 좋았으며 코드를 깔끔하게 작성한것 같음 
 - break문의 사용을 적절이 잘한거 같음
