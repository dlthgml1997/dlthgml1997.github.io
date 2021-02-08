---
title: "[앵귤러/Angular] 의존성 주입"
date: 2020-03-11 14:11:00
tags: 앵귤러
---



**의존성 주입(Dependency injection, DI)**

> 의존성을 직접 생성하지 않고 외부 어딘가에서 받아오도록 요청하는 패턴

- **의존성**(dependencies) : 어떤 클래스가 동작하기 위해 필요한 서비스나 객체를 의미
- 클래스의 인스턴스가 생성될 때 이 클래스에 필요한 의존성을 프레임워크가 생성해서 전달

- 애플리케이션 디자인 패턴 중에서도 아주 중요한 패턴
- 이 패턴을 활용하면 Angular 애플리케이션을 좀 더 효율적인 모듈 형태로 구성할 수 있다.

- 한 가지 예로는 데이터를 처리하는 Service를 만들 때 new 키워드로 인스턴스를 직접 생성하는것이 아닌, Angular가 제공하는 의존성 주입 매커니즘에 따라 component의 생성자로 주입되는 것



### 의존성 주입 가능한 서비스 생성하고 등록하기

- 목 데이터는 파일에 정의해두고 이 데이터를 서비스 클래스로 감싸 컴포넌트에 주입

> 한 파일에 클래스를 여러개 정의하면 이 파일을 접하는 많은 사람들에게 혼란을 줄 수 있기 때문에 컴포넌트와 서비스는 파일 하나에 하나씩 정의하는 것이 좋다.  
>
> 또한 컴포넌트와 서비스가 같은 파일에 정의해야 한다면 서비스 먼저 정의해야한다. 그렇지 않으면 런타임 null 참조 에러가 발생한다. (컴포넌트를 먼저 정의하고자 하면 forwardRef() 메소드를 사용하면 된다.)



#### 의존성으로 주입할 서비스 클래스 정의

Angular CLI를 사용하여 아래 명령을 이용하면 `HeroService` 클래스가 생성된다.  

```
ng generate service hero
```

`hero.sevice.ts` 초기 생성 파일은 아래와 같다.

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  // 이 서비스를 애플리케이션 최상위 인젝터에 등록합니다.
  providedIn: 'root',
})
export class HeroService {
  constructor() { }
}
```

- ***@Injectable()*** : 클래스를 인젝터에 프로바이더로 등록할 때 사용하는 데코레이터

  - `인젝터`:  서비스의 인스턴스를 생성하고 클래스에 주입하는 역할을 한다. 인스턴스를 생성할 때 프로바이더를 이용한다. 

  - `프로바이더`: 프로바이더 인터페이스들 중 하나를 구현하는 오브젝트, 프로바이더 객체는 DI토큰과 관련된 주입 가능한 의존성을 얻는 방법을 정의한다. 프로바이더에 서비스 클래스를 등록하면 인젝터는 new 키워드를 사용해 인스턴스를 생성한다. 

    1. **서비스 클래스에서 @Injectable() 데코레이터로 직접 등록할 수 있다.** 
    2. NgModule의 @NgModule() 데코레이터에 등록할 수있다.
    3. 컴포넌트의 @Component() 데코레이터에 등록할 수있다.

    위의 예제는 1번의 방식을 사용하였다.

    > 여러 클래스를 같은 서비스 타입으로 인젝터에 등록 가능하며, 서로 다른 프로바이더를 각기 다른 인젝터에 등록할 수 있다. 

  - `proviededIn`

    1. @Injectable() 데코레이터를 사용할 때: 메타 데이터 옵션으로 서비스가 root인젝터에 등록될지, 특정 NgModule에 등록될지 지정할 수 있다.
       - 서비스가 최상위 인젝터에 등록되면 Angular는 HeroService의 인스턴스를 하나만 생성하며, 이 클래스가 주입되는 모든 곳에서 같은 인스턴스를 공유한다.
    2. @NgModule() 이나 @Component() 데코레이터를 사용할 때 : NgModule 계층이나 컴포넌트 계층의 인젝터에 프로바이더를 등록할 수 있다.

  - 이 데코레이터가 등록된 클래스가 실제로 사용되지 않으면 이 클래스를 최종 빌드 결과물에서 제거하는 대상으로 등록하는 역할도 한다.



### 서비스 주입하기

#### 의존성 주입을 사용하는 컴포넌트 vs 사용하지 않는 컴포넌트

> 의존성 주입을 사용하지 않는 컴포넌트

아래 HeroListComponent는 다른 mock 파일에 정의된 HEROES라는 배열을 메모리에 올려서 참조한다.

```typescript
...
import { HEROES }      from './mock-heroes';
...
export class HeroListComponent {
  heroes = HEROES;
}
```

이 방식은 실제 운영환경에서는 적합하지 않다. 테스트를 적용하거나 리모트 서버에서 데이터를 가져오도록 변경한다면 HerosListComponent를 반드시 수정해야하기 때문이다. 상황에 따라 매번 HEROES 목 데이터를 변경해야할 수도 있다. 

> 의존성 주입을 사용하는 컴포넌트

```typescript
...
import { Hero }        from './hero';
import { HeroService } from './hero.service';
...
export class HeroListComponent {
  heroes: Hero[];

  constructor(heroService: HeroService) {
    this.heroes = heroService.getHeroes();
  }
}
```

이 때 서비스클래스는 부모 인젝터 중 어딘가에 반드시 등록되어야 하지만, 컴포넌트의 입장에서는 서비스가 어디에 등록되어 있는지는 중요하지 않다.



이 때 서비스 클래스의 코드는 아래와 같다.

```typescript
import { Injectable } from '@angular/core';
import { HEROES } from './mock-heroes';

@Injectable({
  // 이 서비스를 애플리케이션 최상위 인젝터에 등록합니다.
  providedIn: 'root',
})
export class HeroService {
  getHeroes() { return HEROES; }
}
```

