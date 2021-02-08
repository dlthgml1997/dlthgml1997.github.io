---
title: "[앵귤러/Angular] Observable 반환을 이용한 동기->비동기"
date: 2020-03-11 18:23:00
tags: 앵귤러
---



아래 코드는 *heroService*라는 **서비스 클래스**에서 **목 데이터 값**을 가져오는 코드이다.

```typescript
this.heroes = this.heroService.getHeroes();
```

위 코드에서 `heroService.getHeroes()`는 *동기 방식*으로 동작하기 때문에 함수의 실행결과가 바로 반환된다. 목 데이터를 가져올 때는 동기 방식이 유효할 수 있지만, 일반적인 애플리케이션에서는 리모트 서버에서 데이터를 가져오기 때문에, *비동기 동작*을 처리해야 하는 경우가 대부분이다.

*비동기*로 동작하기 위해 여러 방법을 사용할 수 있다.

1. 콜백함수를 사용한다.
2. Promise를 반환하도록 처리한다.
3. **Observable**을 반환하도록 처리한다.

이 포스팅에서는 3번의 방법을 구현해 보겠다! (Angular가 제공하는 *HttpClient.get* 메소드가 **Observable**을 반환하기 때문에 가장 자연스럽다.)

`Observable` : *RxJS 라이브러리*가 제공하는 클래스 중 가장 중요한 클래스이다. 



먼저 서비스 클래스 파일에 코드를 추가한다.

```typescript
import { Observable, of } from 'rxjs';
```

Observable을 로드한다.



getHeroes() 메소드를 수정한다.

> 기존 getHeroes() 메소드

```typescript
getHeroes(): Hero[] {
  return HEROES;
}
```

> 수정된 getHeroes() 메소드

```typescript
getHeroes(): Observable<Hero[]> {
  return of(HEROES);
}
```

*of(HEROES)*는 히어로 목 데이터를 **Observable<Hero[]>** 타입으로한번에 반환한다.



이제는 *Observable<Hero[]>*타입을 반환하기 때문에 **컴포넌트** 코드도 수정하여야 한다.

> 기존 컴포넌트 코드

```typescript
getHeroes(): void {
  this.heroes = this.heroService.getHeroes();
}
```

> 수정된 컴포넌트 코드

```typescript
getHeroes(): void {
  this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes);
}
```



*비동기 방식*으로 수정한 후에는 서버의 응답이 언제 도착하는지와 관계없이, 이 응답이 도착했을 때 **subscribe**가 서버에서 받은 응답을 콜백함수로 전달하고, 컴포넌트는 이렇게 받은 데이터를 heroes 프로퍼티에 할당한다.

