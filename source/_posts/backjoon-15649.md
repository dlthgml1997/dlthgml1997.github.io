---
title: "[백준알고리즘/ boj] N과 M(1) - 15649 (파이썬/ python)"
dates: 2020-08-26 03:12:00
tag: 알고리즘
---

| 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
| :-------- | :---------- | :---- | :---- | :-------- | :-------- |
| 1 초      | 512 MB      | 20319 | 12289 | 8369      | 60.261%   |



# 문제

실버 3 문제이당

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

- 1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열



## 입력

첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)



## 출력

한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.

수열은 사전 순으로 증가하는 순서로 출력해야 한다.



### 예제 입력 1 

```
3 1
```

### 예제 출력 1 

```
1
2
3
```

### 예제 입력 2 

```
4 2
```

### 예제 출력 2 

```
1 2
1 3
1 4
2 1
2 3
2 4
3 1
3 2
3 4
4 1
4 2
4 3
```

### 예제 입력 3

```
4 4
```

### 예제 출력 3

```
1 2 3 4
1 2 4 3
1 3 2 4
1 3 4 2
1 4 2 3
1 4 3 2
2 1 3 4
2 1 4 3
2 3 1 4
2 3 4 1
2 4 1 3
2 4 3 1
3 1 2 4
3 1 4 2
3 2 1 4
3 2 4 1
3 4 1 2
3 4 2 1
4 1 2 3
4 1 3 2
4 2 1 3
4 2 3 1
4 3 1 2
4 3 2 1
```



# 풀이

순열이랑 dfs 익히기 위해서 풀어보았당.

1. 순열을 이용하는 방법 (순서 o)

   ```python
   import sys
   from itertools import permutations
   
   input = sys.stdin.readline
   N, M = map(int,input().split())
   
   answer = permutations(range(1, N+1),M)
   
   for i in answer:
       print(' '.join(map(str, i)))
   ```

   * 1 부터 N 까지니까 `range(1, N+1)`
   *  `print(' '.join(map(str, i)))` 
     * 한 칸 띄우고 join 한다, 출력이 string 형태여서 map 한다. 
   * itertools ! permutations ! 외우기 !
     

2. DFS 를 이용하는 방법

   ```python
   import sys
   input = sys.stdin.readline
   
   N, M = map(int, input().split())
   visited = [0 for _ in range(N)]
   answer = []
   
   def dfs(depth):
       if depth == M:
           print(' '.join(map(str, answer)))
           return
       for i in range(len(visited)):
           if visited[i] == 0:
               visited[i] = 1
               answer.append(i+1)
               dfs(depth +1)
               visited[i] = 0
               answer.pop()
   
   dfs(0)
   ```
   
   