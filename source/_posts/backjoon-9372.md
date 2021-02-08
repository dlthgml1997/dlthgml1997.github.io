---
title: "[알고리즘] 백준알고리즘(boj) - 9372: 상근이의 여행 (파이썬/python)"
date: 2020-08-11 02:37:00
tags: 알고리즘
---

# 문제

상근이는 겨울방학을 맞아 N개국을 여행하면서 자아를 찾기로 마음먹었다. 

하지만 상근이는 새로운 비행기를 무서워하기 때문에, 최대한 적은 종류의 비행기를 타고 국가들을 이동하려고 한다.

이번 방학 동안의 비행 스케줄이 주어졌을 때, 상근이가 **가장 적은 종류**의 비행기를 타고 모든 국가들을 여행할 수 있도록 도와주자.

상근이가 한 국가에서 다른 국가로 이동할 때 다른 국가를 거쳐 가도(심지어 이미 방문한 국가라도) 된다.

## 입력

첫 번째 줄에는 테스트 케이스의 수 T(T ≤ 100)가 주어지고,

각 테스트 케이스마다 다음과 같은 정보가 주어진다.

- 첫 번째 줄에는 국가의 수 N(2 ≤ N ≤ 1 000)과 비행기의 종류 M(1 ≤ M ≤ 10 000) 가 주어진다.
- 이후 M개의 줄에 a와 b 쌍들이 입력된다. a와 b를 왕복하는 비행기가 있다는 것을 의미한다. (1 ≤ a, b ≤ n; a ≠ b) 
- 주어지는 비행 스케줄은 항상 연결 그래프를 이룬다.

## 출력

테스트 케이스마다 한 줄을 출력한다.

- 상근이가 모든 국가를 여행하기 위해 타야 하는 비행기 종류의 최소 개수를 출력한다.

#### 예제 입력 1

```
2
3 3
1 2
2 3
1 3
5 4
2 1
2 3
4 3
4 5
```

#### 예제 출력 1

```
2
4
```

#### 출처

[ICPC ](https://www.acmicpc.net/category/1)> [Regionals ](https://www.acmicpc.net/category/7)> [Europe ](https://www.acmicpc.net/category/10)> [Northwestern European Regional Contest ](https://www.acmicpc.net/category/15)> [Benelux Algorithm Programming Contest ](https://www.acmicpc.net/category/89)> [BAPC 2013](https://www.acmicpc.net/category/detail/1160) F번

- 문제의 오타를 찾은 사람: [rhksdlr134](https://www.acmicpc.net/user/rhksdlr134) [vl0612](https://www.acmicpc.net/user/vl0612)
- 문제를 번역한 사람: [WeissBlume](https://www.acmicpc.net/user/WeissBlume)

## 알고리즘 분류

- [최소 스패닝 트리](https://www.acmicpc.net/problem/tag/최소 스패닝 트리)
- [BFS](https://www.acmicpc.net/problem/tag/BFS)



# 풀이

```python
import sys
input = sys.stdin.readline

def bfs(start):
    queue = [start]
    foot_prints = [start]
    answer = 0
    while queue:
        start = queue.pop(0)
        for i in range(len(airplane[start])):
            if airplane[start][i] and i not in foot_prints:
                queue.append(i)
                foot_prints.append(i)
                answer += 1
    return answer

T = int(input())
while T:
    N , M = map(int,input().split())
    airplane = [[0] * (N+1) for _ in range(N+1)]
    for _ in range(M):
        a, b = map(int,input().split())
        airplane[a][b] = 1
        airplane[b][a] = 1
    print(bfs(1))
    T -= 1
```



이번 문제는 입력을 받아오는 방법이 새로웠다.

1. 테스트 케이스의 개수를 T로 받아오고, **T** 개의 테스트 케이스 라인들을 받아오기 위해 **while 문**을 이용한다. 

2. 국가마다 이어지는 것이기 때문에 **배열(airplane) 은  N+1 * N+1 의 크기로** 생성한다. (N: 국가의 수) 
   - N+1 의 크기를 이용하는 이유 : BFS 탐색 노드를 출력하는 문제의 경우, 인덱스와 노드의 숫자가 일치하도록 배열을 생성하면  print할 때나 사용할 때 이해하기 편하다고 생각해서 !

3. 이후 M개의 줄에 a b 쌍이 입력되기 때문에 **for문은 M만큼** 돌며 a b를 받아온다.

4. a와 b를 왕복하는 비행기가 있다는 것은 a국가와 b국가 사이에 **간선**이 있다는 것이다. 1로 표현한다.

   ```python
   airplane[a][b] = 1
   airplane[b][a] = 1
   ```

5. 배열을 완성한 후 **BFS**를 실행한다. (시작 노드는 1)



사실 비행기들은 모든 국가를 들릴 수 있도록 이어져 있기 때문에 타야 하는 **비행기 종류의 최소 개수**는 **N-1**(국가의 수-1) 이다. 

하지만 BFS 구현 코드를 다시 떠올릴 겸 BFS를 이용하여 풀어보았다. 

* 들린 국가의 수 출력이 아닌 비행기 종류의 개수 출력이기 때문에 국가를 이동할 때마다 answer에 1을 더하여 탄 비행기 종류 개수를 반환한다. 



아래 코드를 추가하니 시간 초과 문제가 해결되었다.

```python
import sys
input = sys.stdin.readline
```



