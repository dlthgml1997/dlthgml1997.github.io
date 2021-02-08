---
title: "[앵귤러/Angular] AppRoutingModule 생성하기"
date: 2020-03-12 18:10:00
tags: 앵귤러
---



애플리케이션 최상위 라우팅을 담당하는 모듈의 클래스 이름은 일반적으로 *AppRoutingModule*이라고 칭한다.

```
ng generate module app-routing --flat --module=app
```

Angular CLI로 다음 명령을 실행하면 *app-routing.module.ts* 파일이 생성되며, 라우팅 모듈이 만들어진다. 

- `--flat` : 새로운 폴더를 만들지 않고 src/app 폴더에 파일 생성
- `--module=app` : Angular CLI가 이 라우팅 모듈을 AppModule의 imports 배열에 자동으로 추가



아래 코드는 기본적으로 생성되는 app.routing.module.ts 파일의 코드이다.

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

@NgModule({
  imports: [
    CommonModule
  ],
  declarations: []
})
export class AppRoutingModule { }
```

위 코드를 라우팅 동작을 실행할 수 있도록 아래 코드를 입력하여 *RouterModule*과 *Routes* 심볼을 로드한다.

```typescript
import { RouterModule, Routes } from '@angular/router';
```

또한 라우팅 규칙에 따라 이동할 컴포넌트 또한 로드한다.

```typescript
import { 이동할Component } from '이동할 컴포넌트의 위치';
```



> 라우팅 규칙(Route)

*라우팅 규칙*은 사용자가 링크를 클릭하거나 브라우저 주소표시줄에 URL을 직접 입력했을 때 라우터가 어떤 화면을 표시할지 정의한 것이다. 

```typescript
const routes: Routes = [
    { path: 'URL과 매칭될 문자열', component: '화면에 표시할 컴포넌트'}
];
```

위 코드를 *AppRoutingModule*에 추가한 후, `path: 'heroes'` 에 해당하는 URL을 만나면 *localhost:4200/heroes*와 같은 URL로 이동하면서 *컴포넌트*를 표시할 수 있다.



> RouterModule.forRoot()

*@NgModule*에 메타데이터를 지정하면 모듈이 생성될 때 라우터를 초기화하면서 브라우저의 주소가 변화되는 것을 감지한다. 그래서 *AppRoutingModule*에도 라우터를 초기화하기 위해 **imports 배열**에 *RouterModule*을 등록해야 한다.

```typescript
imports: [ RouterModule.forRoot(routes) ],
```

위 코드를 *@NgModule* 안에 입력하면 된다. 

- `forRoot()` :  최상위 계층에 존재하는 라우터를 설정할 때 사용하는 메소드이다. 이 메소드를 사용하면 브라우저에서 변경되는 URL을 감지할 수 있다.

또한 앱에서도 *RouterModule*을 사용할 수 있도록 **exports 배열**도 지정해야한다.

```typescript
exports: [ RouterModule ]
```

 imports 코드 아래에 위 코드를 입력하면 된다.



---

> 추가: 라우팅 영역(RouterOutlet) 추가하기

AppComponent html 파일에 아래 코드를 추가한다.

```html
<router-outlet></router-outlet>
```

- `<router-outlet> `: 라우팅 된 화면이 표시될 위치를 지정하는 엘리먼트이다.
- 위에서 `RouterModule`을 *exports 배열*을 통해 외부로 공개하였기 때문에 *AppComponent* 에서도 *RouterOutlet* 디렉티브를 사용할 수 있다. 
  - 또한 이는 맨 위쪽에서 *--module=app* 플래그를 지정하였기 때문에 자동으로 추가된 것이다.
- 파일을 직접 생성했거나 Angular CLI 외의 툴을 이용했다면 *app.module.ts* 파일에서 *AppRoutingModule*을 로드하고 *NgModule*의 *imports 배열*에 이 라우팅 모듈을 추가하면 된다.

