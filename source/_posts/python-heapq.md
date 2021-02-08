---
title: "[파이썬] heapq 모듈"
date: 2020-08-27 18:12:00
tags: 파이썬
---

>  heapq 모듈에 대해 간략히 알아보자 ! 



### Heap 이란 ? 

힙(heap)은 최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 완전이진트리(complete binary tree)를 기본으로 한 자료구조(tree-based structure)로서 다음과 같은 힙 속성(property)을 만족한다.

- A가 B의 부모노드(parent node)이면, A의 키(key)값과 B의 키값 사이에는 대소관계가 성립한다.

힙에는 두가지 종류가 있으며, 부모노드의 키값이 자식노드의 키값보다 항상 큰 힙을 '최대 힙', 부모노드의 키값이 자식노드의 키값보다 항상 작은 힙을 '최소 힙'이라고 부른다. 아래 사진은 **최대 힙**의 예시이다.



<img src="../image/image-20200827173046492.png" alt="image-20200827173046492" style="zoom:50%;" />

출처 : [위키백과 '힙 (자료 구조)'](https://ko.wikipedia.org/wiki/%ED%9E%99_(%EC%9E%90%EB%A3%8C_%EA%B5%AC%EC%A1%B0))



## heapq

**완전 이진트리 기반의 최소 힙 자료구조**이다. heapq의 첫번째 인덱스 값은 최소값이다.

부모 노드의 key 값은 자식 노드의 key 값보다 작거나 같다.

heapq 모듈은 큐 알고리즘이라고도 하는 힙(heap) 큐 알고리즘의 구현을 제공한다.

### python에 쓰이는 heapq 코드 

- ` import heapq ` : heapq 모듈을 사용하기 위해 써주어야한다.
- `heapq.heapify(x)` : 값이 들어있는 리스트 x를 최소 힙으로 변환하는 코드이다. 이 때 주의할 점은 최소 힙을 만족시키는리스트가 아닌 최소 힙(리스트x)으로 변경된다는 사실이다.
- `heapq.heappush(heap, item)` : item 값을 힙으로 푸시한다.
- `heapq.heappushpop(heap, item)` : 힙에 item을 푸시한 다음, heap에서 가장 작은 항목을 팝하고 반환한다. ( `heapq.heappush(heap)` => `heapq.heappop(heap)`)
- `heapq.heapreplace(heap, item)` : heap에서 가장 작은 항목을 팝하고 반환하며, 새로운 item도 푸시한다. heap 이 비어있을 시에 IndexError가 발생한다. ( `heapq.heappop(heap)` => `heapq.heappush(heap)`)

주의할 점 ! sort 와 달리 전체를 정렬하는 것이 아니므로 맨앞의 값이 최소값인 것은 확실하지만 두번째 값이 두번째로 작은 값임은 확신할 수 없다. 

이 경우 heapq.heappop(heap)을 한 다음 heap[0] 으로 접근한다.



참고: https://python.flowdas.com/library/heapq.html 

