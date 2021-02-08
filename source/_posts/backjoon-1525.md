---
title: "[백준알고리즘] 퍼즐 - 1525 (파이썬/python)"
dates: 2020-09-04 03:14:00
tag: 알고리즘
---

# 문제

| 시간 제한 | 메모리 제한 | 제출 | 정답 | 맞은 사람 | 정답 비율 |
| :-------- | :---------- | :--- | :--- | :-------- | :-------- |
| 1 초      | 32 MB       | 9234 | 3778 | 2219      | 39.386%   |



3×3 표에 다음과 같이 수가 채워져 있다. 오른쪽 아래 가장 끝 칸은 비어 있는 칸이다.

| 1    | 2    | 3    |
| :--- | ---- | ---- |
| 4    | 5    | 6    |
| 7    | 8    |      |

어떤 수와 인접해 있는 네 개의 칸 중에 하나가 비어 있으면, 수를 그 칸으로 이동시킬 수가 있다. 물론 표 바깥으로 나가는 경우는 불가능하다. 우리의 목표는 초기 상태가 주어졌을 때, 최소의 이동으로 위와 같은 정리된 상태를 만드는 것이다. 다음의 예를 보자.

| 1    |      | 3    |
| ---- | ---- | ---- |
| 4    | 2    | 5    |
| 7    | 8    | 6    |

| 1    | 2    | 3    |
| ---- | ---- | ---- |
| 4    |      | 5    |
| 7    | 8    | 6    |

| 1    | 2    | 3    |
| ---- | ---- | ---- |
| 4    | 5    |      |
| 7    | 8    | 6    |

| 1    | 2    | 3    |
| ---- | ---- | ---- |
| 4    | 5    | 6    |
| 7    | 8    |      |

가장 윗 상태에서 세 번의 이동을 통해 정리된 상태를 만들 수 있다. 이와 같이 최소 이동 횟수를 구하는 프로그램을 작성하시오.

## 입력

세 줄에 걸쳐서 표에 채워져 있는 아홉 개의 수가 주어진다. 한 줄에 세 개의 수가 주어지며, 빈 칸은 0으로 나타낸다.

## 출력

첫째 줄에 최소의 이동 횟수를 출력한다. 이동이 불가능한 경우 -1을 출력한다.

### 예제 입력 1

```
1 0 3
4 2 5
7 8 6
```

### 예제 출력 1

```
3
```

### 예제 입력 2

```
3 6 0
8 1 2
7 4 5
```

### 예제 출력 2

```
-1
```



## 출처

- 문제를 번역한 사람: [baekjoon](https://www.acmicpc.net/user/baekjoon)
- 잘못된 데이터를 찾은 사람: [djm03178](https://www.acmicpc.net/user/djm03178)
- 데이터를 추가한 사람: [hello70825](https://www.acmicpc.net/user/hello70825)
- 메모리 제한을 수정한 사람: [portableangel](https://www.acmicpc.net/user/portableangel)



## 알고리즘 분류

- [그래프 이론](https://www.acmicpc.net/problem/tag/7)
- [그래프 탐색](https://www.acmicpc.net/problem/tag/11)
- [너비 우선 탐색](https://www.acmicpc.net/problem/tag/126)
- [비트마스킹](https://www.acmicpc.net/problem/tag/14)

# 풀이

BFS로 푸는 문제이다. 저번에 미로 문제를 풀 때 썼던 방식과 유사하게 풀면 될것이라 생각해서 풀었더니 완전 틀려버렸다ㅠㅠ..

처음 제출했던 코드 (틀림)

```python
import sys
input = sys.stdin.readline

table = []
for _ in range(3):
    table.append(list(map(int,input().split())))

sorted = [[1,2,3],[4,5,6],[7,8,0]]
visited = []
queue = [[0,0]]

def solution():
    answer = 0
    while queue:
        [i, j] = queue.pop(0)
        visited.append([i,j])
        if i>0 and [i-1,j] not in visited:
            if table[i-1][j] != sorted[i-1][j] and table[i][j] == 0:
                answer += 1
                table[i][j] = table[i-1][j]
                table[i-1][j] = 0
            queue.append([i-1,j])
        if j>0 and [i,j-1] not in visited:
            if table[i][j-1] != sorted[i][j-1] and table[i][j] == 0:
                answer += 1
                table[i][j] = table[i][j-1]
                table[i][j-1] = 0
            queue.append([i,j-1])
        if j<2 and [i,j+1] not in visited:
            if table[i][j+1] != sorted[i][j+1] and table[i][j] == 0:
                answer += 1
                table[i][j] = table[i][j+1]
                table[i][j+1] = 0
            queue.append([i,j+1])
        if i<2 and [i+1,j] not in visited:
            if table[i+1][j] != sorted[i+1][j] and table[i][j] == 0:
                answer += 1
                table[i][j] = table[i+1][j]
                table[i+1][j] = 0
            queue.append([i+1,j])

    if table != sorted:
        return -1

    return answer

print(solution())
```

문제점 -> 0이 움직일 수 있는 모든 조건을 검사하는 것이 아니다. 0이 움직일 수 있는 모든 조건을 검사하려면 queue 에 table 배열이 쌓여야하는데 이는 구현이 복잡할 뿐더러 메모리 제한 오류가 발생한다고 한다. 이 개념을 가능하게 하려면 배열이 아닌 string 형태로 table을 받아와 다루면 된다 (검색을 통해 알게 되었다.)



```python
import sys

def solution():
    queue = [table]
    visited = {table:0} # 딕셔너리 key: table , value: 움직인 수
    
    while queue:
        q = queue.pop(0)
        step = visited.get(q) # 해당 테이블까지 움직인 step 수를 얻어온다.
        zeroIdx = q.index('0')
 
        if q == '123456780':
            return step
 
        # q가 배열의 모습일 때, 0의 인덱스를 구한다.
        i = zeroIdx//3
        j = zeroIdx - 3*(zeroIdx//3)
 
        step += 1
        ql = list(q)
        if i > 0: # 위
            ql[zeroIdx], ql[zeroIdx-3] = ql[zeroIdx-3], ql[zeroIdx]
            qs = ''.join(ql)
            if not visited.get(qs):
                visited[qs] = step
                queue.append(qs)
            ql[zeroIdx], ql[zeroIdx-3] = ql[zeroIdx-3], ql[zeroIdx]
 
        if i < 2: # 아래
            ql[zeroIdx], ql[zeroIdx+3] = ql[zeroIdx+3], ql[zeroIdx]
            qs = ''.join(ql)
            if not visited.get(qs):
                visited[qs] = step
                queue.append(qs)
            ql[zeroIdx], ql[zeroIdx+3] = ql[zeroIdx+3], ql[zeroIdx]
        
        if j > 0: # 왼쪽
            ql[zeroIdx], ql[zeroIdx-1] = ql[zeroIdx-1], ql[zeroIdx]
            qs = ''.join(ql)
            if not visited.get(qs):
                visited[qs] = step
                queue.append(qs)
            ql[zeroIdx], ql[zeroIdx-1] = ql[zeroIdx-1], ql[zeroIdx]
            
        if j < 2: # 오른쪽
            ql[zeroIdx], ql[zeroIdx+1] = ql[zeroIdx+1], ql[zeroIdx]
            qs = ''.join(ql)
            if not visited.get(qs):
                visited[qs] = step
                queue.append(qs)
            ql[zeroIdx], ql[zeroIdx+1] = ql[zeroIdx+1], ql[zeroIdx]
 
    return -1
 
# 배열이 아닌 str 형태로 받아온다.
table = ''
for _ in range(3):
    table += ''.join(sys.stdin.readline().split())
 
print(solution())
```

난 아직 많이 부족하다는 것을 깨달았다 ㅠ-ㅠ 그래도 딕셔너리 / 새로운 bfs 방식 / 새로운 문제 접근 방식 을 배운 것에 만족하자 ! 

