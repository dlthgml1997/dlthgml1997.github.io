---
title: "[앵귤러/Angular] 네비게이션 링크(routerLink) 추가하기"
date: 2020-03-12 21:19:00
tags: 앵귤러
---

> 앞에 글(AppRoutingModule 생성하기)에서는 URL을 통해 이동하는 방법이었다면, 이 글에서는 네비게이션을 실행하는 링크를 클릭하여 이동하는 방법을 다룰것이다!



*AppComponent*의 탬플릿 (*app.component.html*)에 아래 코드를 추가한다.

```html
<nav>
    <a routerLink="/heroes">Heroes</a>
</nav>
```

- `routerLink` : *RouterModule*이 제공하는 *RouterLink* *디렉티브*이며, 사용자가 이 디렉티브가 적용된 엘리먼트를 클릭하면 네비게이션을 실행한다.
- `"/heroes"` : `routerLink` 어트리뷰트 값으로 url을 통해 이동할 컴포넌트에 해당하는 라우팅 경로이다.