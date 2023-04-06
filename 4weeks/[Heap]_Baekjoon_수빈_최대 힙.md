```python
import sys
from queue import PriorityQueue
que = PriorityQueue()

N = int(sys.stdin.readline())
popcount = 0

for i in range(N):

    inputv = int(sys.stdin.readline())
    if inputv == 0:
        if popcount == 0:
            print(0)
        else:
            print(que.get()[1])
            popcount -= 1
    else:
        que.put((-inputv, inputv))
        popcount += 1
    # print(heap)

```

파이썬 우선순위 큐 라이브러리를 사용하였음

PriorityQueue와 heapq 둘 다 같은 결과를 내므로 어떤 것을 사용하여도 무방하다고 생각됨

PriorityQueue와 heapq는 최소 힙만 다룰 수 있기 때문에 큰 수부터 pop 하고싶을 때는 - 부호를 붙혀 push하면 됨


---

아래는 힙을 직접 구현한 코드이며 heapify를 진행할 때 버블정렬을 쓰는 것과 배열에 값을 저장할 때나 뺄 때 노드의 왼쪽 자식은 2x+1 오른쪽 자식은 2x+2가 됨만 확인하면 좋을 것 같음

```python
# 아래의 코드는 최대 힙을 구현한 것이며 주석에서 언급한 부분의 코드를 바꾸면 최소 힙이 된다.
heap = []
sz = 0

def push(x):
    global sz
    heap.append(x)
    sz += 1
    idx = sz - 1
    while (idx != 0):  # 최댓값의 idx가 0이되면 break
        # print(heap)
        par = int((idx - 1) / 2)
        if heap[par] >= heap[idx]:  # 부모가 자식 노드들 보다 클 경우 이상없음(최대 힙), 반대의 경우는 최소 힙
            break
        temp = heap[par]
        heap[par] = heap[idx]
        heap[idx] = temp
        idx = par  # 최댓값의 idx가 0으로 만들기 위함


def pop():
    global sz
    sz -= 1
    heap[0] = heap[sz]  # 삭제하려는 부분(루트)을 맨 마지막 노드와 바꿈
    heap.pop()
    idx = 0
    while (2*idx + 1 < sz):
        lc = 2*idx + 1
        rc = 2*idx + 2
        max_child = lc
        if rc < sz:  # 오른쪽 노드가 존재한다면
            if heap[rc] > heap[lc]:
                max_child = rc
        if heap[idx] >= heap[max_child]:  # 부모가 자식 노드들 보다 클 경우 이상없음(최대 힙), 반대의 경우는 최소 힙
            break
        temp = heap[max_child]
        heap[max_child] = heap[idx]
        heap[idx] = temp
        idx = max_child


def top():
    return heap[0]
```



ㅡㅡㅡ

## Feedback
---
### Eros

1. 우선순위 큐를 사용하며 코드가 전체적으로 깔끔하게 끝나서 좋았슴
2. 최대 힙 구현은 진짜 대단한거 같음

---
### 이름

1.내용
