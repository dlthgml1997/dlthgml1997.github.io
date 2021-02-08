---
title: "[프로그래머스] 더 맵게 - 파이썬"
date: 2020-02-25 21:10:00
tags: 알고리즘
---



# 문제설명

매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

```
섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
```

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- scoville의 길이는 1 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.

##### 입출력 예

| scoville             | K    | return |
| -------------------- | ---- | ------ |
| [1, 2, 3, 9, 10, 12] | 7    | 2      |

##### 입출력 예 설명

1. 스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
   새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5
   가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]
2. 스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
   새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13
   가진 음식의 스코빌 지수 = [13, 9, 10, 12]

모든 음식의 스코빌 지수가 7 이상이 되었고 이때 섞은 횟수는 2회입니다.



# 풀이

```python
def solution(scoville, K):
    import heapq
    answer = 0
    heapq.heapify(scoville)
    
    while len(scoville) > 1 :
        i = heapq.heappop(scoville)
        j = heapq.heappop(scoville)
        if i < K:
            answer += 1
            mixedK = i +j *2
            heapq.heappush(scoville, mixedK)
        else:
            return answer
            
    if scoville[0] > K:
        return answer
    else:
        return -1
```

- 이를 풀기 위해 공부한 내용은 heapq 모듈이다.

- 계속 문제16번에서만 실패가 떠서 왜 그런지 찾아본 결과, `while len(scoville) > 1` 을 했기 때문에 `if scoville[0] > K: return answer ` 를 써주지 않으면 scoville의 길이가 1일 때는 -1 이 return 되기 때문이었다.

- scoville의 크기가 1 보다 크게 한 이유는 0보다 크게하면 RuntimeError가 발생하기 때문이다. 

- heappop은 힙에서 가장 작은 값을 반환한다. 