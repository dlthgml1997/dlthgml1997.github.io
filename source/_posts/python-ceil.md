---
title: "[파이썬] 올림, 내림, 반올림"
dates: 2020-08-27 02:01:00
tag: 파이썬
---



**올림: ceil**

**내림: floor**

**반올림: round**



예시

```python
import math

print(math.ceil(100/33)) # 4
print(math.ceil(0.3)) # 1

print(math.floor(100/33)) # 3
print(math.floor(0.6)) # 0

print(round(98/6)) #16 (몫: 16 나머지: 2 -> 나머지가 6의 반인 3보다 작은 값이기 때문에 내림 !)
print(round(100/6)) # 17 (몫: 16 나머지: 4 -> 나머지가 6의 반인 3보다 큰 값이기 때문에 올림!)
print(round(0.6)) # 1
```



