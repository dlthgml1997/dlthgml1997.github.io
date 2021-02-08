---
title: "[프로그래머스] 스킬 체크 레벨 1 풀어보기(파이썬)"
date: 2020-12-10 18:00:00
tag: 알고리즘
---

* 링크 : https://programmers.co.kr/skill_checks > 레벨 1

# 풀이

난이도가 좀 많이 쉬워서 올리기 민망하지만 ㅎㅎ 풀어보았다.

* **문제 1**

  n = 3 이면 '수박수'

  n = 5 이면 '수박수박수' 와 같은 문자열을 반환한다.

```python
def solution(n):
    answer = ''
    for i in range(n):
        if i% 2 == 0:
            answer += '수'
        else:
            answer += '박'

    return answer
```

* **문제 2**

  배열 arr이 주어지면 최소 숫자를 제거한 배열을 반환한다.

  배열이 모두 비어진 경우에는 [-1]을 반환한다.

```python
def solution(arr):
    if len(arr) == 1:
        return [-1]
    i = min(arr)
    arr.remove(i)
    answer = arr
    return answer
```

