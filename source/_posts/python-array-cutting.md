---
title: "[파이썬] numpy array[::] 사용법(array 슬라이싱)"
date: 2020-02-22 15:24:00
tags: 파이썬
---



### 슬라이싱 (slicing)

기본형태 : **array[start​ : end : ​step]**

- `start` : 슬라이싱을 시작할 시작 위치
- `end`: 슬라이싱을 끝낼 위치로 end는 포함하지 않는다.
- `step`: stride라고도 하며 몇개씩 끊어서 가져올지를 정한다.

양수,음수 모두 가능



- `a[ start: ]` : start 위치부터 끝까지 가져오기

- `a[ end : ]`: 시작점부터 end 위치까지 모두 가져오기

- `a[ start : end ]` : start위치 부터 end 위치까지 모두 가져오기

- `a[ start : end : step ]` (step이 `양수` 일 때) : 오른쪽으로 step만큼 이동하면서 가져온다.

- `a[ start: end : step]`(step이 `음수`일 때): 왼쪽으로 step만큼 이동하면서 가져온다.

  ```python3
  >>> a= ['a', 'b', 'c', 'd', 'e']
  # 인덱스 1~3 까지를 꺼꾸로 가져오기
  >>> a[3 :0 :-1]
  ['d', 'c', 'b']
  ```



**더 많은 예제 참고** : https://twpower.github.io/119-python-list-slicing-examples