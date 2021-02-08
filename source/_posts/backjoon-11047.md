---
title: "[백준알고리즘] 11407 동전0 - 파이썬(python)"
date: 2020-04-19 23:25:00
tags: 알고리즘
---

# 문제

| 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
| :-------- | :---------- | :---- | :---- | :-------- | :-------- |
| 1 초      | 256 MB      | 27606 | 14939 | 12067     | 54.587%   |

준규가 가지고 있는 동전은 총 N종류이고, 각각의 동전을 매우 많이 가지고 있다.

동전을 적절히 사용해서 그 가치의 합을 K로 만들려고 한다. 이때 필요한 동전 개수의 최솟값을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)

둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. (1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)

## 출력

첫째 줄에 K원을 만드는데 필요한 동전 개수의 최솟값을 출력한다.

## 예제 입력 1 복사

```
10 4200
1
5
10
50
100
500
1000
5000
10000
50000
```

## 예제 출력 1 복사

```
6
```

## 예제 입력 2 복사

```
10 4790
1
5
10
50
100
500
1000
5000
10000
50000
```

## 예제 출력 2 복사

```
12
```

## 출처

- 문제를 만든 사람: [baekjoon](https://www.acmicpc.net/user/baekjoon)

## 알고리즘 분류

- [그리디 알고리즘](https://www.acmicpc.net/problem/tag/그리디 알고리즘)
- [동전 교환](https://www.acmicpc.net/problem/tag/동전 교환)



# 풀이

```python
n, k = map(int, input().split())
coins = []
for _ in range(n):
    coin = int(input())
    if coin > k:
        break
    coins.append(coin)
     
count = 0
answer = 0
for i in range(1,n+1):
    count = k // coins[-i]
    k = k % coins[-i]
    answer += count
    if k == 0:
        break

print(answer)
```

n과 k를 map(int, input().split()`.strip()`) 으로 가져오니 런타임에러가 떴다.. 

없애니 실행이 잘 됐다. 



애초에 k값보다 큰 coin 값은 제외하고 coins 배열에 넣었다.

coins 배열의 인덱스를 반대로 돌면서 나눈 몫을 answer에 더하고 k엔 나눈 나머지 값을 저장하다가 k가 0이 되면 멈춘다. 