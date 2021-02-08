---
title: "[앵귤러/Angular] 클래스 바인딩 문법"
date: 2020-03-10 15:14:00
tags: 앵귤러
---



Angular가 제공하는 [클래스 바인딩](https://angular.kr/guide/template-syntax#class-binding) 문법을 사용하면 특정 조건에 따라 CSS 클래스를 추가하거나 제거할 수 있습니다. 스타일을 지정하려는 엘리먼트에 `[class.some-css-class]="some-condition"`와 같은 문법을 추가하면 됩니다.



#### html파일

```html
[class.selected]="hero === selectedHero"
```

-  hero === selectedHero인 줄에 selected CSS 클래스가 추가된다. 

#### css파일

```css
.heroes li.selected {
    background-color: #CFD8DC;
    color: white;
}
.heroes li.selected:hover {
    background-color: #BBD8DC;
    color: white;
}
```



---추가예정---

