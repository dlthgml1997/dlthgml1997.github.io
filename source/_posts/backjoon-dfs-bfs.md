---
title: "[백준알고리즘] 1260번: DFS와 BFS- 파이썬(python)"
date: 2020-03-23 21:00:00
tags: 알고리즘
---

# 문제

그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

## 입력

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

## 출력

첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.

##### 예제 입력 2 

```
5 5 3
5 4
5 2
1 2
3 4
3 1
```

##### 예제 출력 2 

```
3 1 2 5 4
3 1 4 2 5
```

# 풀이

> DFS - BFS에 대해 알아본 후 문제풀이를 해보자 ! 
>
> [DFS 와 BFS의 이해를 돕는 유튜브 영상 링크][https://www.youtube.com/watch?v=_hxFgg7TLZQ]

### BFS (너비 우선 탐색)

같은 깊이 순서대로 탐색, 큐를 이용한다.

- 먼저 matrix를 생성한다.  정점의 개수(num)보다 +1 크기의 matrix를 생성한다. 

  `matrix = [[0]* (num+1) for _ in range(num+1)]`

* 간선을 가지고 있는 경우 matrix[간선을가진 정점] [간선을 가진정점]을 1로 지정한다.

위의 예제의 경우 아래와 같은 matrix가 형성될 것이다.

<img src="../image/KakaoTalk_20200323_224007711.png" alt="KakaoTalk_20200323_224007711" style="zoom:25%;" />



* BFS는 맨처음 queue배열을 생성하여 [시작 정점]을 넣으며 시작한다.

* for n range(len(matrix[시작정점]))를 돌며 시작정점과 간선을 가진 정점을 만나면 모두 queue에 넣는다. 
* for문이 끝난 후 queue.pop(0)을 통해  첫번째 인덱스의 정점을 뽑아 정답 배열에 넣은 후다시 for문을 돌며 정점과 간선을 가진 모든 정점을 queue에 넣는다. 
* 이를 queue가 빌 때까지 반복하면 된다.



### DFS (깊이 우선 탐색)

가장 깊은 곳까지 내려갔다가 다시 탐색 시작 정점으로 올라와 탐색을 시작하는 방식, 재귀함수를 이용한다. 

* BFS와 동일한 matrix를 생성한다.

* DFS는 for n range(len(matrix[시작정점]))를 돌며 matrix[시작정점] [n] == 1을 만나면 배열(foot_prints)에 넣는다. 
* 이 때 이미 방문한 정점은 배열에 넣지 않는다.
* for문이 끝난 후  n을 시작정점으로써 재귀함수를 호출한다. 



### 코드

```python
N, M, V = map(int, input().split())
matrix = [[0] * (N + 1) for _ in range(N + 1)]
for _ in range(M):
    link = list(map(int, input().split()))
    matrix[link[0]][link[1]] = 1
    matrix[link[1]][link[0]] = 1


def dfs(current_node, mat, foot_prints):
    foot_prints += [current_node]
    for search_node in range(len(mat[current_node])):
        if mat[current_node][search_node] and search_node not in foot_prints:
            foot_prints = dfs(search_node, mat, foot_prints)
    return foot_prints


def bfs(start):
    queue = [start]
    foot_prints = [start]
    while queue:
        current_node = queue.pop(0)
        for search_node in range(len(matrix[current_node])):
            if matrix[current_node][search_node] and search_node not in foot_prints:
                foot_prints += [search_node]
                queue += [search_node]
    return foot_prints


print(*dfs(V, matrix, []))
print(*bfs(V))
```

