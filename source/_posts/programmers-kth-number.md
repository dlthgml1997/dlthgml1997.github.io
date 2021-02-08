---
title: "[프로그래머스] K번째 수 - 파이썬"
date: 2020-02-22 16:22:00
tags: 알고리즘

---

# 문제 설명

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.

##### 입출력 예

| array                 | commands                          | return    |
| --------------------- | --------------------------------- | --------- |
| [1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] | [5, 6, 3] |

##### 입출력 예 설명

[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
[1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
[1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.

[출처](https://neerc.ifmo.ru/subregions/northern.html)



# 풀이

```python
def solution(array, commands):
    answer = []
    for command_list in commands:
        sliced_array = array[command_list[0]-1 : command_list[1]]
        sliced_array.sort()
        answer.append(sliced_array[command_list[2]-1])
    return answer
```



이번 문제를 위해 공부한 내용은 array의 `slicing` 과 `sort`이다.



1. `commands` 가 [[2, 5, 3], [4, 4, 1], [1, 7, 3]] 일 때, `for command_list in commands`를 통해  [2, 5, 3] **->** [4, 4, 1] **->** [1, 7, 3] 순서로 `command_list`에 담는다.  

2. 예를 들어 `command_list`가 *[2,5,3]* 일 때, 

   `array`의 *command_list[0]-1* (1번 인덱스) 부터 *command_list[1]* (4번 인덱스까지)(`slicing`에서 ` end`부분(5)은 자르지 않기때문에 -1 해줄 필요가 없다.)까지 잘라 `sliced_array`에 담는다.

3.  `sliced_array`를 `sort()` 로 정렬한다. 

4. *`answer`에  command_list[2]-1* (3번 인덱스) 의 값을 더한다.



### 시행착오

 처음에`for i in range(len(commands))` 로 i에  인덱스를 담아 `array[commands[i] [0] -1 : commands[i] [1]] ` 이렇게 접근하였다.

 근데 `for command_list in commands` 를 사용하면 commands의 첫번째, 두번째, 세번째 배열을 command_list에 담으며 실행할 수 있다는 것을 알게 되었고 코드를 고칠 수 있었다.  