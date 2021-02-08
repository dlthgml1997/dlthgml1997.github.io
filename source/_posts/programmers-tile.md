---
title: "[알고리즘] 프로그래머스 - 타일 장식물 (파이썬/python)"
date: 2020-05-01 16:48:00
tags: 알고리즘
---

# 문제

대구 달성공원에 놀러 온 지수는 최근에 새로 만든 타일 장식물을 보게 되었다. 타일 장식물은 정사각형 타일을 붙여 만든 형태였는데, 한 변이 1인 정사각형 타일부터 시작하여 마치 앵무조개의 나선 모양처럼 점점 큰 타일을 붙인 형태였다. 타일 장식물의 일부를 그리면 다음과 같다.

![ㅅㅡㅋㅡㄹㅣㄴㅅㅑㅅ 2018-08-21 ㅇㅗㅎㅜ 5.11.26.png](https://grepp-programmers.s3.amazonaws.com/files/production/3e31bedd54/fcc48066-e72f-45c8-af03-e4360b58b589.png)

그림에서 타일에 적힌 수는 각 타일의 한 변의 길이를 나타낸다. 타일 장식물을 구성하는 정사각형 타일 한 변의 길이를 안쪽 타일부터 시작하여 차례로 적으면 다음과 같다.
[1, 1, 2, 3, 5, 8, .]
지수는 문득 이러한 타일들로 구성되는 큰 직사각형의 둘레가 궁금해졌다. 예를 들어, 처음 다섯 개의 타일이 구성하는 직사각형(위에서 빨간색으로 표시한 직사각형)의 둘레는 26이다.

타일의 개수 N이 주어질 때, N개의 타일로 구성된 직사각형의 둘레를 return 하도록 solution 함수를 작성하시오.

##### 제한 사항

- N은 1 이상 80 이하인 자연수이다.

##### 입출력 예

| N    | return |
| ---- | ------ |
| 5    | 26     |
| 6    | 42     |

[출처](https://www.digitalculture.or.kr/koi/selectOlymPiadDissentList.do)



# 풀이

```python
def solution(N):
    tiles = [1 for _ in range(N)]
    before = tiles[1]
    before_back = tiles[0] 
    for i in range(N):
        if i == 0 or i == 1:
            continue
        tiles[i] = before+ before_back
        before = tiles[i]
        before_back = tiles[i-1] 
    
    case = [4]
    for i in range(N):
        if i==0:
            continue
        before = case[i-1]
        now = before + tiles[i] *2  
        case.append(now)
    
    answer = case[N-1] # case 배열의 마지막이 N개의 타일들로 구성된 직사각형의 둘레
    return answer
```



동적 프로그래밍을 통해 문제를 해결하였다.