---
title: "[백준알고리즘] 2178번: 미로 탐색- 파이썬(python)"
date: 2020-03-23 21:00:00
tags: 알고리즘
---

# 문제

N×M크기의 배열로 표현되는 미로가 있다.

| 1    | 0    | 1    | 1    | 1    | 1    |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | 0    | 1    | 0    | 1    | 0    |
| 1    | 0    | 1    | 0    | 1    | 1    |
| 1    | 1    | 1    | 0    | 1    | 1    |

미로에서 1은 이동할 수 있는 칸을 나타내고, 0은 이동할 수 없는 칸을 나타낸다. 이러한 미로가 주어졌을 때, (1, 1)에서 출발하여 (N, M)의 위치로 이동할 때 지나야 하는 최소의 칸 수를 구하는 프로그램을 작성하시오. 한 칸에서 다른 칸으로 이동할 때, 서로 인접한 칸으로만 이동할 수 있다.

위의 예에서는 15칸을 지나야 (N, M)의 위치로 이동할 수 있다. 칸을 셀 때에는 시작 위치와 도착 위치도 포함한다.

## 입력

첫째 줄에 두 정수 N, M(2 ≤ N, M ≤ 100)이 주어진다. 다음 N개의 줄에는 M개의 정수로 미로가 주어진다. 각각의 수들은 **붙어서** 입력으로 주어진다.

## 출력

첫째 줄에 지나야 하는 최소의 칸 수를 출력한다. 항상 도착위치로 이동할 수 있는 경우만 입력으로 주어진다.

#### 예제 입력 1

```
4 6
101111
101010
101011
111011
```

#### 예제 출력 1

```
15
```

#### 예제 입력 2

```
4 6
110110
110110
111111
111101
```

#### 예제 출력 2

```
9
```

#### 예제 입력 3

```
2 25
1011101110111011101110111
1110111011101110111011101
```

#### 예제 출력 3

```
38
```

#### 예제 입력 4

```
7 7
1011111
1110001
1000001
1000001
1000001
1000001
1111111
```

#### 예제 출력 4

```
13
```



# 풀이

```python
def main():
    n, m = map(int, input().split())
    data = []
    for _ in range(n):
        data.append(list(map(int, str(input()))))
    distance = [[0 for _ in range(m)] for _ in range(n)]
    distance[0][0] = 1
    queue = [[0,0]]
    foot_prints = []

    while queue:
        [i, j] = queue.pop(0)
        foot_prints.append([i,j])
    
        if j > 0 and data[i][j-1] == 1 and [i,j-1] not in foot_prints and [i,j-1] not in queue:
            queue.append([i,j-1])
            distance[i][j-1] = distance[i][j] + 1
        if j < m-1 and data[i][j+1] == 1 and [i,j+1] not in foot_prints and [i,j+1] not in queue:
            queue.append([i,j+1])
            distance[i][j+1] = distance[i][j] + 1
        if i > 0 and data[i-1][j] == 1 and [i-1,j] not in foot_prints and [i-1,j] not in queue:
            queue.append([i-1,j])
            distance[i-1][j] = distance[i][j] + 1
        if i < n-1 and data[i+1][j] == 1 and [i+1,j] not in foot_prints and [i+1,j] not in queue:
            queue.append([i+1,j])    
            distance[i+1][j] = distance[i][j] + 1

    return distance[n-1][m-1]
    
print(main())
```



큐를 이용한 bfs를 통해 문제 풀이를 하였다.



(출처)[https://claude-u.tistory.com/212]