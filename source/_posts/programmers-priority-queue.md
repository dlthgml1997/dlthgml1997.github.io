---
title: "[프로그래머스] 이중 우선순위 큐 - 파이썬(python)"
date: 2020-08-27 18:14:00
tags: 알고리즘
---



# 문제설명

이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.

| 명령어 | 수신 탑(높이)                  |
| ------ | ------------------------------ |
| I 숫자 | 큐에 주어진 숫자를 삽입합니다. |
| D 1    | 큐에서 최댓값을 삭제합니다.    |
| D -1   | 큐에서 최솟값을 삭제합니다.    |

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

##### 제한사항

- operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.
- operations의 원소는 큐가 수행할 연산을 나타냅니다.
  - 원소는 “명령어 데이터” 형식으로 주어집니다.- 최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.
- 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.

##### 입출력 예

| operations          | return |
| ------------------- | ------ |
| [I 16,D 1]          | [0,0]  |
| [I 7,I 5,I -5,D -1] | [7,5]  |

##### 입출력 예 설명

16을 삽입 후 최댓값을 삭제합니다. 비어있으므로 [0,0]을 반환합니다.
7,5,-5를 삽입 후 최솟값을 삭제합니다. 최대값 7, 최소값 5를 반환합니다.

[출처](http://icpckorea.org/problems/2013/onlineset.pdf)



# 풀이

> 코드

```python
def solution(operations):
    import heapq
    answer = []
    priority_queue = []
    
    for operation in operations:
        op = operation[:1]
        num = int(operation[2:])
        if op == "D" and priority_queue:
            if num == 1:
                priority_queue.pop(priority_queue.index(max(priority_queue)))
            elif num == -1:
                heapq.heappop(priority_queue)
        elif op == "I":
            heapq.heappush(priority_queue, num)
        
    if priority_queue:
        answer = [max(priority_queue),heapq.heappop(priority_queue)]
    else:
        answer = [0,0]
                                   
    return answer
```



> 새로 알게 된 점

1. 문자열 인덱싱(슬라이싱) 
   - 슬라이싱을 통해 operation 과 숫자를 나눴다.
2.  `priority_queue.index(max(priority_queue))`
   - 위 코드를 통해 priority_queue에서 가장 큰 값의 인덱스를 얻어올 수 있었다. 매우 편하다!
3. `heapq.heappush(priority_queue, num)` 
   * 위 코드는 최소힙(우선순위큐)을 만족하도록 num을 push한다.
4. `heapq.heappop(priority_queue)`
   * 위 코드는 최소 값을 pop한다.



> 어려웠던 점

 사실 생각보단 금방 풀었지만 ! 맨 처음 코드가 아래와 같을 때,

```python
    for operation in operations:
        if operation == "D 1" and priority_queue:
            data = max(priority_queue)
            priority_queue.pop(priority_queue.index(data))
        elif operation == "D -1" and priority_queue:
            data = min(priority_queue)
            priority_queue.pop(priority_queue.index(data))
        else:
            num = operation[2:]
            heapq.heappush(priority_queue, int(num))
```

입력값이 `["I 16", "I -5643", "D -1", "D 1", "D 1", "I 123", "D -1"]` 인 경우,

세번 째 `"D 1"` 에서 `priority_queue`가 비어있으니  `else`로 넘어가면서 1이 push 되는 문제가 발생하였다. 

그래서 `op` 와 `num`으로 나눠서 검사를 했더니 문제가 해결되었다. 



`and priority_queue`를 넣지 않으면 ValueError : **max() arg is an empty sequence** 등의 문제가 발생한다.