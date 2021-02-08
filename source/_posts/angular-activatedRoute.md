---
title: "[앵귤러/Angular] URL에 존재하는 라우팅 변수 참조하기(ActivatedRoute 이용)"
date: 2020-03-12 21:56:00
tags: 앵귤러
---



### ActivatedRoute

- 컴포넌트의 인스턴스를 생성하면서 적용한 라우팅 규칙에 대한 정보를 담고있다.

- 아래 코드를 통해 로드할 수 있다.

  ```typescript
  import { ActivatedRoute } from '@angular/router';
  ```



#### URL에 존재하는 라우팅 변수 참조하기

1. 라우팅 변수를 참고할 컴포넌트의 생성자에 ActivatedRoute를 private 프로퍼티로 선언한다.

   ```typescript
   constructor(
     private route: ActivatedRoute
   ) {}
   ```

2. 예를 들어 '/detail/:id' 형태의 URL에서 id값을 가져오고 싶을 때, 아래 코드를 입력한다.

   ```typescript
   const id = +this.route.snapshot.paraMap.get('id');
   ```

   - `route.snapshot`: 컴포넌트가 생성된 직후에 존재하는 라우팅 규칙에 대한 정보를 담고있는 객체이다.
   - `paraMap`: route.snapshot 객체가 paraMap을 사용하면 URL에 존재하는 라우팅 변수를 참조할 수 있다.

   > 추가: javaScript (+) 연산자를 사용해서 라우팅 변수를 숫자로 변환하였다.