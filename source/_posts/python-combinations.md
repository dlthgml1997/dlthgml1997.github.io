---
title: "[파이썬] 조합(combinations)을 사용하여 리스트에 있는 값들의 모든 조합 구하기"
date: 2020-05-05 14:54:00
tags: 파이썬
---

> 정의

- **Combinations** **(조합 nCr)** : 하나의 리스트에서 모든 조합을 계산해야할 때 사용한다.

- Permutations (순열 nPr) 과의 차이

  순열은 순서가 바뀐 경우도 포함하고, 조합은 순서가 바뀐 경우는 포함하지 않는다(순서 상관 없음).

  예를 들어 1,2,3 으로 이루어진 리스트에서 순열은 (1,2),(1,3),(2,3),(2,1),(3,1),(3,2) 조합은 (1,2),(1,3),(2,3) 이다.



> 사용 방법

```python
from itertools import combinations # itertools 중 combinations를 import

items = ['1','2','3']
c = list(combinations(items,2)) # 2가지 조합으로 이루어질 수 있는 모든 경우의 수를 list로 만든다.
print(list(c))
# [(1,2), (1,3), (2,3)]
```

