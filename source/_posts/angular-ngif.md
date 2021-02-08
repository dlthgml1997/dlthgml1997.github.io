---
title: "[앵귤러 / Angular] *ngIf"
date: 2020-03-10 14:24:00
tags: 앵귤러
---





`*ngIf` : if와 같이 동작

```html
<div *ngIf="selectedHero">
    ...
</div>
```

: `selectedHero` 가 할당되어 있을 때 실행, undefined일 땐 실행 되지 않는다.



`*ngIf`를 넣어주지 않으면` ERROR TypeError: Cannot read property 'name' of undefined` 에러가 난다. 



> `ngIf`앞에 별표(*)가 있다는 것을 잊지마세요. Angular에서 아주 중요한 문법입니다.



[출처](https://angular.kr/tutorial/toh-pt2)