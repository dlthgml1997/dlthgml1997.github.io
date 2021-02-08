---
title: "[알고리즘] 백준알고리즘(boj) - 12761: 돌다리 (파이썬/python)"
date: 2020-08-19 01:03:00
tags: 알고리즘
---

# 문제

| 시간 제한 | 메모리 제한 | 제출 | 정답 | 맞은 사람 | 정답 비율 |
| :-------- | :---------- | :--- | :--- | :-------- | :-------- |
| 1 초      | 128 MB      | 1856 | 923  | 773       | 51.091%   |

동규와 주미는 일직선 상의 돌 다리 위에있다. 돌의 번호는 0 부터 100,000 까지 존재하고 동규는 N번 돌 위에, 주미는 M번 돌 위에 위치하고 있다. 동규는 주미가 너무 보고싶기 때문에 최대한 빨리 주미에게 가기 위해 A,B 만큼의 힘을 가진 스카이 콩콩을 가져왔다. 동규가 정한 다리를 건너는 규칙은 턴 방식인데, 한 턴에 이동할 수 있는 거리는 이러하다. 현 위치에서 +1칸, -1칸을 이동할 수 있고, 스카이 콩콩을 이용해 현 위치에서 A나 B만큼 좌우로 점프할 수 있으며, 순간적으로 힘을 모아 현 위치의 A배나 B배의 위치로 이동을 할 수 있다. 예를 들어 지금 동규가 7번 돌 위에 있고 스카이 콩콩의 힘이 8이면 그냥 점프를 해서 15번 돌에 갈 수도 있고, 순간적으로 힘을 모아 56번 돌에 갈 수도 있다는 것이다. 주어진 8가지의 방법 중 적절한 방법을 골라서 최대한 빨리 동규가 주미를 만날 수 있게 도와주자. 단, 이동 과정에서 100,000보다 크거나 0보다 작은 번호의 돌은 존재하지 않으므로 갈 수 없고, 같은 방법을 계속 사용해도 되며 항상 도달할 수 있는 케이스만 주어진다.

## 입력

입력의 첫 줄에 스카이 콩콩의 힘 A와 B, 그리고 동규의 현재위치 N, 주미의 현재 위치 M이 주어진다. (단, 2≤A,B≤30 이고  0≤N,M≤100,000)

## 출력

동규가 주미에게 도달하기 위한 최소한의 이동 횟수를 출력하라.



### 예제 입력

```
2 3 1 20
```

### 예제 출력 

```
4
```

### 예제 입력 

```
3 7 2 98500
```

### 예제 출력 

```
10
```



# 풀이

```python
import sys
input = sys.stdin.readline

def bfs():
    while queue:
        start = queue.pop(0)
        for i in range(8):        
            if i < 6 and 0<= start+ steps[i] < 100001 and foot_prints[start + steps[i]] == 0:
                now = start + steps[i]
                foot_prints[now] = 1
                queue.append(now)
                count[now] += count[start] + 1
            elif i >= 6 and 0 <= start * steps[i] < 100001 and foot_prints[start * steps[i]] == 0 : 
                now = start * steps[i]
                foot_prints[now] = 1
                queue.append(now)
                count[now]+= count[start] + 1
            

a, b, n, m = map(int,input().split())
steps = [-1, 1, a, b, -a, -b, a, b]
queue= [n]
foot_prints = [0 for _ in range(100001)]
count = [0 for _ in range(100001)]
bfs()
print(count[m])
```



bfs 를 이용해서 풀었다.

* steps 배열에 이동할 수 있는 모든 경우의 수를 넣는다 

  > steps =  [-1칸 이동, +1칸 이동, a 만큼 이동, b만큼 이동, -a만큼 이동, -b만큼 이동, *a만큼 이동, *b만큼 이동]

* foot_prints 를 길이 100000인 배열로 만드는 이유 ! 

  * 내가 기존에 풀었던 방식인 ` if start + steps[i] not in foot_prints` 으로 하면 foot_prints를 전체탐색해야하기 때문에 시간이 오래걸려서 

* `for i in range(8)`에서 start에서 steps의 모든 방법으로 이동한 곳의 count 를 1 증가시킨다. 

  > for 문이 i= 0 부터 i=7 까지 한번 돌면 (while 문이 1번 돈 상태)
  >
  > count[start-1]
  >
  > count[start+1]
  >
  > count[start+a]
  >
  > count[start+b]
  >
  > count[start-a]
  >
  > count[start-b]
  >
  > count[start*a]
  >
  > count[start-*b]
  >
  > (if 조건을 모두 만족한다면,)
  >
  > 가 모두 1이 된다

  * 들린 곳을 모두 queue에 삽입하였기 때문에 들린 곳이 start가 되고 다시 steps의 모든 방법으로 이동한 곳의 count는 count[start]보다 1 증가한 값이 된다.

    >  while 문이 2번 돈 상태에서 ( if 조건을 모두 만족했다는 전제하에서는) count[now]는 2가 된다 (while 한번 돌았을 때 count[now] =1 이 되었기 때문) 

* while 문은 start에서 steps로 가는 모든 경우(`for i in range(8)`)가 범위가 0이상 100000이하를 만족하지 못하거나  이미 다 들린 경우(`foot_prints가 1`) 끝난다.

* 이제 count[m]은 동규(n)가 주미(m)에게 가기 위해 이동한 횟수임을 알 수 있다 !



deque 이용하는 방법 익히려고 deque 이용한 코드도 남겨두기,,

```python
두from collections import deque
import sys
input = sys.stdin.readline

def bfs():
    while queue:
        start = queue.popleft()
        for i in range(8):        
            if i < 6 and 0<= start+ steps[i] < 100001 and foot_prints[start + steps[i]] == 0:
                now = start + steps[i]
                foot_prints[now] = 1
                queue.append(now)
                count[now] += count[start] + 1
            elif i >= 6 and 0 <= start * steps[i] < 100001 and foot_prints[start * steps[i]] == 0 : 
                now = start * steps[i]
                foot_prints[now] = 1
                queue.append(now)
                count[now]+= count[start] + 1
            

a, b, n, m = map(int,input().split())
steps = [-1, 1, a, b, -a, -b, a, b]
queue = deque()
queue.append(n)
foot_prints = [0 for _ in range(100001)]
count = [0 for _ in range(100001)]
bfs()
print(count[m])
```

