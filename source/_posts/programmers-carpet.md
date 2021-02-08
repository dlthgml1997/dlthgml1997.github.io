---
title: "[프로그래머스] 카펫 - 파이썬"
date: 2020-03-04 21:06:00
tags: 알고리즘
---



# 문제설명

Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 빨간색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

![image.png](https://grepp-programmers.s3.amazonaws.com/files/ybm/7c94563a35/2ff27ac9-97d0-43a9-9cf8-a344b8e7912e.png)

Leo는 집으로 돌아와서 아까 본 카펫의 빨간색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 빨간색 격자의 수 red가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 빨간색 격자의 수 red는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

##### 입출력 예

| brown | red  | return |
| ----- | ---- | ------ |
| 10    | 2    | [4, 3] |
| 8     | 1    | [3, 3] |
| 24    | 24   | [8, 6] |

[출처](http://hsin.hr/coci/archive/2010_2011/contest4_tasks.pdf)

※ 공지 - 2020년 2월 3일 테스트케이스가 추가되었습니다.

# 풀이

이 문제는 완전 탐색(exhausitve search)를 이용하여 푸는 문제이다. 



**red** 의 가로를 `x` 세로를 `y`라고할 때, 

**red**는 `x*y` 가 되고 **brown**은 `2(x*y)+4`가 된다. 

**brown**의 가로와 세로는 `x+2` , `y+2` 이다.



이 때 `x`는 `y`보다 길거나 같으며 `red = x*y`를 성립하기 때문에, `y`는 **red**의 제곱근보다 작거나 같다.



처음엔

```python
def solution(brown, red):
    for y in range(1, int(red**0.5)+1):
        x = red // y
        if 2*(x+y) +4 == brown:
            return [x+2,y+2]
    return answer
```

이렇게 풀었더니 13개의 테스트 중 5개를 실패하였다.

이유는 나머지가 0이 아닌 상황이 나오기 때문이었다. 



`if red % y == 0` 를 추가하였다.

```python
def solution(brown, red):
    for y in range(1, int(red**0.5)+1):
        if red % y ==0:
            x = red // y
            if 2*(x+y) +4 == brown:
                return [x+2,y+2]
    return answer

```

끝 !