---
title: "[알고리즘] 프로그래머스- N으로 표현 파이썬 (python)"
date: 2020-04-26 23:15:00
tags: 알고리즘
---

# 문제

아래와 같이 5와 사칙연산만으로 12를 표현할 수 있습니다.

12 = 5 + 5 + (5 / 5) + (5 / 5)
12 = 55 / 5 + 5 / 5
12 = (55 + 5) / 5

5를 사용한 횟수는 각각 6,5,4 입니다. 그리고 이중 가장 작은 경우는 4입니다.
이처럼 숫자 N과 number가 주어질 때, N과 사칙연산만 사용해서 표현 할 수 있는 방법 중 N 사용횟수의 최솟값을 return 하도록 solution 함수를 작성하세요.

##### 제한사항

- N은 1 이상 9 이하입니다.
- number는 1 이상 32,000 이하입니다.
- 수식에는 괄호와 사칙연산만 가능하며 나누기 연산에서 나머지는 무시합니다.
- 최솟값이 8보다 크면 -1을 return 합니다.

##### 입출력 예

| N    | number | return |
| ---- | ------ | ------ |
| 5    | 12     | 4      |
| 2    | 11     | 3      |

##### 입출력 예 설명

예제 #1
문제에 나온 예와 같습니다.

예제 #2
`11 = 22 / 2`와 같이 2를 3번만 사용하여 표현할 수 있습니다.

[출처](https://www.oi.edu.pl/old/php/show.php?ac=e181413&module=show&file=zadania/oi6/monocyfr)

# 풀이

**동적 프로그래밍 (Dynamic Programming)**을 이용하여 푸는 문제이다.

동적 프로그래밍이란, 큰 문제를 작은 단위의 문제로 나누어 풀고 이전에 계산했던 값을 저장해둔 다음 매번 다시 계산하지 않고 저장해둔 값을 재사용하는 프로그래밍 기법을 의미한다.



```python
def solution(N, number):
    case = [0,[N]]
    if N == number: 
        return 1
    for i in range(2,9): # 2부터 8까지
        num = int(str(N)*i)
        cases = []
        cases.append(num)
        for i_half in range(1, i//2+1):
            for x in case[i_half]: 
                for y in case[i-i_half]: 
                    cases.append(x*y)
                    cases.append(x+y)
                    if x > y:
                        cases.append(x-y)
                    if y > x:
                        cases.append(y-x)
                    if y != 0:
                        cases.append(x/y)
                    if x != 0:
                        cases.append(y/x)
                if number in cases:
                    return i
            case.append(cases)
    return -1
```

* 제일 이해하기 힘들었던 부분은 for문의 range를 i의 반만 도는 이유였다 



풀이 추가하기,, 