---
title: "[프로그래머스] 해시- 전화번호 목록 (파이썬/ python)"
dates: 2020-08-27 20:48:00
tag: 알고리즘
---



# 문제

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- phone_book의 길이는 1 이상 1,000,000 이하입니다.
- 각 전화번호의 길이는 1 이상 20 이하입니다.

##### 입출력 예제

| phone_book                  | return |
| --------------------------- | ------ |
| [119, 97674223, 1195524421] | false  |
| [123,456,789]               | true   |
| [12,123,1235,567,88]        | false  |

##### 입출력 예 설명

입출력 예 #1
앞에서 설명한 예와 같습니다.

입출력 예 #2
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

입출력 예 #3
첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.



# 풀이

```python
def solution(phone_book):
    phone_book.sort()
    answer = True
    
    for i in range(len(phone_book)-1):
        if phone_book[i+1].startswith(phone_book[i],0,len(phone_book[i])):
            answer = False
            break
        
    return answer
```

* 새로 알게 된 것 

  * find() => 인덱스 위치 반환

  * startswith(확인하고자하는 문자, 시작위치, 끝위치) => True/ False 여부 반환

    ```python
    print('12345'.startswith('1')) # True
    print('12345'.startswith('2')) # False
    print('12345'.startswith('4',2)) # False
    print('12345'.startswith('4',3,4)) # True
    print('12345'.startswith('1',2,4)) # False
    print('12345'.startswith('1',0,2)) # True
    ```

  * endswith()

    ```python
    print('12345'.endswith('5')) # True
    print('12345'.endswith('2',0,2)) # True '12'
    print('12345'.endswith('4',0,5)) # False '12345'
    print('12345'.endswith('5',4,5)) # True '45'
    ```

    위 예제들에서 알 수 있다싶이, 배열은 두번째 인수의 인덱스 부터 세번째 인수의 인덱스-1까지 자른 후 검사한다 ! 

    default 는 배열 전체.

* phone_book.sort() 를 하면 스트링 sort이기 때문에

  `['119', '97674223', '1195524421']`-> `['119', '1195524421', '97674223']`  이러한 형식으로 sort 된다.

