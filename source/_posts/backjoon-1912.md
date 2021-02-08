---
title: "[알고리즘] 백준알고리즘 1912 연속합 (파이썬/python)"
date: 2020-05-09 23:26:00
tags: 알고리즘
---



# 문제

n개의 정수로 이루어진 임의의 수열이 주어진다. 우리는 이 중 연속된 몇 개의 수를 선택해서 구할 수 있는 합 중 가장 큰 합을 구하려고 한다. 단, 수는 한 개 이상 선택해야 한다.

예를 들어서 10, -4, 3, 1, 5, 6, -35, 12, 21, -1 이라는 수열이 주어졌다고 하자. 여기서 정답은 12+21인 33이 정답이 된다.

#### 입력

첫째 줄에 정수 n(1 ≤ n ≤ 100,000)이 주어지고 둘째 줄에는 n개의 정수로 이루어진 수열이 주어진다. 수는 -1,000보다 크거나 같고, 1,000보다 작거나 같은 정수이다.

#### 출력

첫째 줄에 답을 출력한다.

#### 예제 입력 1 

```
10
10 -4 3 1 5 6 -35 12 21 -1
```

#### 예제 출력 1 

```
33
```

#### 예제 입력 2 

```
10
2 1 -4 3 4 -4 6 5 -5 1
```

#### 예제 출력 2 

```
14
```

#### 예제 입력 3 

```
5
-1 -2 -3 -4 -5
```

#### 예제 출력 3 

```
-1
```

#### 출처

- 데이터를 추가한 사람: [djm03178](https://www.acmicpc.net/user/djm03178) [dohyeokkim](https://www.acmicpc.net/user/dohyeokkim) [doju](https://www.acmicpc.net/user/doju) [jh05013](https://www.acmicpc.net/user/jh05013) [kimdr123](https://www.acmicpc.net/user/kimdr123) [seedkin](https://www.acmicpc.net/user/seedkin)
- 빠진 조건을 찾은 사람: [isac322](https://www.acmicpc.net/user/isac322) [Qwaz](https://www.acmicpc.net/user/Qwaz)
- 문제의 오타를 찾은 사람: [jh05013](https://www.acmicpc.net/user/jh05013)
- 잘못된 데이터를 찾은 사람: [tncks0121](https://www.acmicpc.net/user/tncks0121)

#### 알고리즘 분류

- [다이나믹 프로그래밍](https://www.acmicpc.net/problem/tag/다이나믹 프로그래밍)
- [수학](https://www.acmicpc.net/problem/tag/수학)



# 풀이

#### 틀린 풀이

```python
n = map(int, input())
nums = list(map(int, input().split()))

max_num = 0
before = 0
while nums:
  for num in nums:
    total = before + num
    if total > before and max_num < total:
      max_num = total
      before = total
    else:
      break
  nums.pop(0)
  before = 0

print(max_num)
```

위 풀이는 컴파일러로 해봤을 때 동작은 되지만 문제의 **시간 제한**을 넘어서서 다른 블로그의 방법들을 찾아보고 이해해 보았다.



#### 맞은 풀이

```python
n = int(input())
nums = [0]
nums += list(map(int, input().split()))

# 0번째 인덱스는 0으로 두기 위해 n+1 크기로 배열 생성
temp = [0 for _ in range(n+1)]

result = -1001 # 최소 숫자가 -1000이기 때문
for i in range(1,n+1):
    temp[i] = max(temp[i-1]+nums[i], nums[i])
    result = max(result, temp[i])
    
print(result)

```

##### 런타임 에러 해결
위에 코드에서 n = map(int, input()) 로 했을 때엔 런타임 에러가 떴는데,  n = int(input()) 으로 바꾸니까 런타임에러가 해결됐다 ..(?)



##### 풀이방법

* 이전 값을 사용해야 하기 때문에 temp, nums 배열 모두 0번째 인덱스는 0으로 두었다. 
* 이전까지 더해온 값들에 현재값을 더한값과(temp[i-1]+nums[i]) 현재값(nums[i]) 중 더 큰 값을 temp 배열에 저장한다.
* 이전 temp 값들과 temp[i]를 비교하여 더 큰 값을 result로 지정한다.