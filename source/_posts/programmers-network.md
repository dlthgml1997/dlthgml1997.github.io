---
title: "[알고리즘] 프로그래머스 - 네트워크 (Python)"
date: 2020-04-13 21:37:00
tags: 알고리즘
---

# 문제

네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

##### 제한사항

- 컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
- 각 컴퓨터는 0부터 `n-1`인 정수로 표현합니다.
- i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
- computer[i][i]는 항상 1입니다.

##### 입출력 예

| n    | computers                         | return |
| ---- | --------------------------------- | ------ |
| 3    | [[1, 1, 0], [1, 1, 0], [0, 0, 1]] | 2      |
| 3    | [[1, 1, 0], [1, 1, 1], [0, 1, 1]] | 1      |



# 풀이

```python
def solution(n, computers):
    answer = 0
    visited = []
    for _ in range(n):
        visited += [0]
    def dfs(start, visited, computers):
            stack = [start]
            while stack:
                current = stack.pop(0)
                visited[current] = 1
                for search in range(n):
                    if computers[current][search] and visited[search] == 0:
                        stack.append(search)
    
    i=0
    while 0 in visited: # 다 돌 때까지 
        if visited[i] == 0: # 아직 들리지 않았다면 
            dfs(i, visited, computers) # 들린다. 한번에 연결된 노드까지 들린다.
            answer +=1
        i+=1

    return answer


```



나는 dfs를 활용하여 풀었다. 

일단 모든 컴퓨터를 다 들려야 하기 떄문에 visited 가 1이 될 때까지 dfs함수를 실행한다.

 dfs는 한번 실행될 때 연결된 모든 노드를 돌기 때문에 함수밖에서 answer의 수를 1 UP해주면 네트워크의 수가 된다!  