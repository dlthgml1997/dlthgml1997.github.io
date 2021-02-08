---
title: "[앵귤러/Angular] Angular CLI 서비스 클래스 생성"
date: 2020-03-11 14:42:00
tags: 앵귤러
---



아래 명령을 이용하면 서비스 클래스 파일이 생성된다.  

```
ng generate service hero
```

`hero.sevice.ts` 초기 생성 파일은 아래와 같다.

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class HeroService {
  constructor() { }
}
```

- *@Injectable()* : 클래스를 인젝터에 프로바이더로 등록할 때 사용하는 데코레이터