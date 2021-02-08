---
title: "[알고리즘] 백준알고리즘 9251 - LCS (파이썬/python)"
date: 2020-05-11 22:16:00
tags: 알고리즘
---

# 문제

| 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
| :-------- | :---------- | :---- | :--- | :-------- | :-------- |
| 1 초      | 256 MB      | 20545 | 8389 | 6261      | 41.156%   |

LCS(Longest Common Subsequence, 최장 공통 부분 수열)문제는 두 수열이 주어졌을 때, 모두의 부분 수열이 되는 수열 중 가장 긴 것을 찾는 문제이다.

예를 들어, ACAYKP와 CAPCAK의 LCS는 ACAK가 된다.

## 입력

첫째 줄과 둘째 줄에 두 문자열이 주어진다. 문자열은 알파벳 대문자로만 이루어져 있으며, 최대 1000글자로 이루어져 있다.

## 출력

첫째 줄에 입력으로 주어진 두 문자열의 LCS의 길이를 출력한다.

## 예제 입력 1

```
ACAYKP
CAPCAK
```

## 예제 출력 1

```
4
```

## 출처

- 문제를 만든 사람: [baekjoon](https://www.acmicpc.net/user/baekjoon)
- 데이터를 추가한 사람: [qpwoeiruty](https://www.acmicpc.net/user/qpwoeiruty)

## 알고리즘 분류

- [다이나믹 프로그래밍](https://www.acmicpc.net/problem/tag/다이나믹 프로그래밍)

# 풀이

**LCS(Longest Common Subsequence)** 는 문제에 나왔듯이 최장 공통 부분 수열을 뜻하며, 

**LCS(Longest Common Substring, 최장 공통 부분 문자열)**과 헷갈릴 수 있다.

공통 부분 문자열은 두 문자열이 가지는 공통적인 문자열 중 끊기지않고 연속적인 부분을 의미하고,

공통 부분 수열은 두 문자열이 가지는 공통적인 문자열이 끊기더라도 순서가 맞으면 LCS로 인정하는 것을 의미한다.



**ABCDHEF** / **BCDEF** 두 문자열이 존재할 때

최장 공통 부분 문자열은 BCD , 최장 공통 부분 수열은 BCDEF이다.



### 코드

```python
n = list(str(input()))
m = list(str(input()))

lcs_list =[[0 for _ in range(len(n) + 1)] for _ in range(len(m) + 1)]
answer = 0

for i in range(len(n)):
    for j in range(len(m)):
        if n[i] ==m[j]:
            lcs_list[j+1][i+1] = lcs_list[j][i] + 1
        else:
            lcs_list[j+1][i+1] = max(lcs_list[j][i+1],lcs_list[j+1][i])
            
print(lcs_list[-1][-1])
```



아래의 표를 만들어가는 코드이다. 

이 문제는 길이만 출력하면 되기 때문에 lcs_list 의 마지막(맨 오른쪽 아래) 값을 출력한다.



​	   A C A Y K P

​	0 0 0 0 0 0 0 

C  0 0 1 1 1 1 1 

A  0 **1** 1 2 2 2 2 

P  0 1 1 2 2 2 3 

C  0 1 **2** 2 2 2 3

A  0 1 2 **3** 3 3 3 

K  0 1 2 3 3 **4** 4



여기서 LCS 는 **ACAK** 가 된다. 

