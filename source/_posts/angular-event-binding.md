---
title: "[앵귤러/Angular] 이벤트 바인딩 문법"
date: 2020-03-10 13:30:00
tags: 앵귤러
---

이벤트 바인딩 문법을 사용하면 키 입력이나 마우스의 움직임, 클릭이나 터치 이벤트를 감지할 수 있습니다. 이 섹션에서 설명하는 내용은 [이벤트 바인딩 예제](https://angular.kr/generated/live-examples/event-binding/stackblitz.html) / [다운로드 링크](https://angular.kr/generated/zips/event-binding/event-binding.zip) 에서 직접 확인할 수 있습니다.



예를 들어 버튼의 클릭 이벤트를 감지하고 있다가 사용자가 버튼을 클릭할 때 컴포넌트에 있는 `onSave()` 메소드를 실행하려면 다음과 같이 구현합니다.

```html
<button (click)="onSave()">
    Save
</button>
```



--추가예정--