---
title: "[프로그래머스] 완주하지 못한 선수 - 파이썬"
date: 2020-03-14 15:00:00
tags: 알고리즘
---

# 문제

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

##### 입출력 예

| participant                             | completion                       | return |
| --------------------------------------- | -------------------------------- | ------ |
| [leo, kiki, eden]                       | [eden, kiki]                     | leo    |
| [marina, josipa, nikola, vinko, filipa] | [josipa, filipa, marina, nikola] | vinko  |
| [mislav, stanko, mislav, ana]           | [stanko, ana, mislav]            | mislav |

##### 입출력 예 설명

예제 #1
leo는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #2
vinko는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #3
mislav는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.

[출처](http://hsin.hr/coci/archive/2014_2015/contest2_tasks.pdf)



# 풀이

```python
def solution(participant, completion):
    for c in completion:
        participant.remove(c)
    answer = participant[0]
    return answer
```

- 처음 위 코드로 풀었더니 시간복잡도가 O(N^2) 를 초과( for문 중첩 사용) 하여 효율성에서 0점이 나오게 된다 ㅠ^ㅠ



```python
def solution(participant, completion):
    participant.sort()
    completion.sort()
    for i,j in zip(participant,completion):
        if i!=j:
            return i 
    answer = participant[0]
    return answer
```

#### 새로 알게된 함수

1. `sort()` : python 내장 함수로 시간 복잡도가 **O(n logn)**이다. 

   ```python
   >>> a = [1, 4, 10, 2, 5]
   >>> a.sort()
   >>> a
   [1, 2, 4, 5, 10]
   
   >>> a.sort(reverse=True)
   >>> a
   [10, 5, 4, 2, 1]
   ```

2. `zip(*iterable)` : 동일한 개수로 이루어진 자료형을 묶어주는 역할을 하는 함수이다.

   > *iterable : 반복가능한 자료형 여러 개를 입력할 수 있다는 뜻

   ```python
   >>> list(zip[1,2,3], [4,5,6])
   [(1,4),(2,5),(3,6)]
   ```

위 두가지를 이용하므로써 *participant 배열*과 *completion 배열*을 `sort`하여 알파벳순으로 정렬한 후 `zip`을 통해 묶는다. 이 때 묶인 participant와 completion 이 같지 않다는 것은 완주를 하지 않았다는 뜻이므로 participant를 반환하면 된다. 