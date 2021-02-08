---
title: "해쉬 알고리즘이란?"
date: 2020-03-14 15:46:00
tags: 알고리즘설명
---

### 해쉬 알고리즘 O(1)

해쉬는 임의의 크기를 가진 데이터를 고정된 데이터의 크기로 변환시키는 것.

key 값을 계산 하는 함수는 **해쉬 함수**라고 한다.



#### 해쉬 함수

- 문자열을 받아 숫자로 변환하는 함수

- 문자열에 숫자를 Mapping (할당)한다.

- 일관성을 유지해야하며, 다른 단어가 들어가면 꼭 다른 숫자가 나와야한다.

- **사용방법**

  1. 0 ,1 , 2, 3, 4 인덱스의 배열이 있다고 하자.

  2. apple을 해쉬 함수에 넣으면 해쉬 함수는 3을 출력한다고 가정, 이 때 apple의 가격을 3번 인덱스 위치에 저장한다.
     1. milk 는 0을 출력한다고 가정, 이 때 milk의 가격을 0번 인덱스 위치에 저장한다.
     2. 위와 같은 방법으로 전체 배열을 채운다.

  3. 이 때 milk의 가격을 묻는다면 배열을 탐색할 필요 없이 milk를 해시함수에 넣기만 하면 해당 가격이 있는 인덱스를 출력하게 될 것이다.

     >해시 함수는 배열의 크기를 알고 있어야하며 유요한 인덱스만 반환해야한다.
     >
     >해시함수와 같은 이름 : 해시 맵, 맵, 딕셔너리, 연관 배열

- **용도**

  - 해시 테이블로 조회하기

    ```python
    phone_book = dict()
    phone_book["jenny"] = 8675409
    phone_book["emergency"] = 911
    
    print(phone_book["jenny"]) # 8675409
    ```

  - 중복 항목 방지하기

    ```python
    voted = {}
    value = voted.get{"tom"} # tom이 있으면 value를 없다면 None을 출력
    
    def check_voter(name):
        if voted.get(name):
            print("이미 투표")
        else:
            voted[name] = True
            print("투표하세요.")
    ```

  - 해시 테이블을 캐시로 사용하기

    ```python
    cache = {}
    
    def get_page(url):
        if cache.get(url):
            return cache[url]
        else:
            data = get_data_from_server(url)
            cache[url] = data
            return data
    ```

- **장점**

  1. 어떤 것과 다른 것 사이의 관계를 모형화
  2. 중복 방지
  3. 서버에게 작업을 시키지 않고 캐싱 가능

  

#### 충돌(Collusion)

해쉬테이블의 가장 큰 문제점이다. 다른 `k`값이 동일한 `h(k)`값을 가져 동일한 `slot`에 저장되는 경우이다. 예를 들어 k1 과 k2 를 해쉬했을 때 h(k1) == h(k2) 인 경우이다. 이러한 문제를 해결하기 위해서는 배열과 리스트를 조합하여 사용하는 자료구조를 사용한다.



[참고](hsp1116.tistory.com/35)

