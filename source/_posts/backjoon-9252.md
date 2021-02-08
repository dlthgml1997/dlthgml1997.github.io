---
title: "[알고리즘] 백준알고리즘 - 9252 LCS2 (파이썬/python)"
date: 2020-05-17 18:30:00
tags: 알고리즘
---

# 문제

LCS(Longest Common Subsequence, 최장 공통 부분 수열)문제는 두 수열이 주어졌을 때, 모두의 부분 수열이 되는 수열 중 가장 긴 것을 찾는 문제이다.

예를 들어, ACAYKP와 CAPCAK의 LCS는 ACAK가 된다.

## 입력

첫째 줄과 둘째 줄에 두 문자열이 주어진다. 문자열은 알파벳 대문자로만 이루어져 있으며, 최대 1000글자로 이루어져 있다.

## 출력

첫째 줄에 입력으로 주어진 두 문자열의 LCS의 길이를, 둘째 줄에 LCS를 출력한다.

LCS가 여러 가지인 경우에는 아무거나 출력하고, LCS의 길이가 0인 경우에는 둘째 줄을 출력하지 않는다.

## 예제 입력 1

```
ACAYKP
CAPCAK
```

## 예제 출력 1

```
4
ACAK
```

## 알고리즘 분류

- [다이나믹 프로그래밍](https://www.acmicpc.net/problem/tag/다이나믹 프로그래밍)



# 풀이

저번에 풀었던 LCS 문제는 길이만 출력을 했다면, LCS2는 LCS 값도 출력을 해야한다.

### 코드

```python
n = input()
m = input()

strings =[[0 for _ in range(len(n) + 1)] for _ in range(len(m) + 1)]

for i in range(len(n)):
    for j in range(len(m)):
        if n[i] ==m[j]:
            strings[j+1][i+1] = strings[j][i] + 1
        else:
            strings[j+1][i+1] = max(strings[j][i+1],strings[j+1][i])

now = strings[-1][-1]
x = len(strings[0]) -1
y = len(strings) -1
answer = ''

while now != 0:
    if now -1 == strings[y][x-1] and now -1 == strings[y-1][x]:
        answer = n[x-1] + answer
        now -= 1
        x -= 1
        y -= 1
    else:
        if strings[y-1][x] > strings[y][x-1]:
            y -= 1
        else:
            x -= 1

print(strings[-1][-1])
print(answer)
```

*strings 배열*

​	   A C A Y K P

​	0 0 0 0 0 0 0 

C  0 0 1 1 1 1 1 

A  0 **1** 1 2 2 2 2 

P  0 1 1 2 2 2 3 

C  0 1 **2** 2 2 2 3

A  0 1 2 **3** 3 3 3 

K  0 1 2 3 3 **4** 4



위 배열의 맨 오른쪽 아래 `(strings[-1][-1])` 부터 돌면서 answer에 문자열을 더해가고, 값이 0 일 때 순회를 멈춘다.

* 앞과 위의 값이 현재 값보다 -1 이면 대각선 위로 이동한다.
* 그렇지 않다면 위의 값과 좌측 값 중
  * 위의 값이 클 땐 위로 이동하고,
  * 좌측값이 크다면  좌측으로 이동한다.
* 이동할 때 answer에 현재 값을 저장한 후 이동한다.



### 새로 배운점

* `배열[-1][-1]` 은 맨 마지막 배열의 value를 의미한다 !