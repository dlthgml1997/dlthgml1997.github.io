---
title: "[앵귤러/Angular] Angular cli overview 정리"
date: 2020-03-11 11:04:00
tags: 앵귤러
---



## Angular CLI 설치

```
npm install -g @angular/cli
```



### 기본 워크 플로우

주어진 명령에 대한 명령 또는 옵션 (예 : [generate](https://angular.kr/cli/generate) )을 간단한 설명과 함께 나열하려면 다음을 입력하면 된다.

```
ng help
ng generate --help
```

개발 서버에서 새 기본 Angular 프로젝트를 작성, 빌드 및 제공하려면 다음 명령을 사용하여 새 작업 공간의 상위 디렉토리로 이동할 수 있다.

```
new my-first-project 
cd my-first-project 
ng serve
```

브라우저에서 [http : // localhost : 4200 /](http://localhost:4200/) 을 열어 앱 실행을 확인할 수 있다.



### CLI 명령 언어 구문

ng *commandNameOrAlias* *requiredArg* [optionalArg] [options]

- 옵션 이름 앞에는 이중 대시(-)가 붙습니다. 옵션 별명은 단일 대시 (-)로 시작한다.

- 인수 및 옵션 이름은 **camelCase** 또는 **dash-case**로 지정할 수 있다. (예 : --myOptionName 또는 --my-option-name)

  

### 명령 개요

| 명령                                            | 별명           | 기술                                                         |
| :---------------------------------------------- | :------------- | :----------------------------------------------------------- |
| [`add`](https://angular.kr/cli/add)             |                | 프로젝트에 외부 라이브러리에 대한 지원을 추가합니다.         |
| [`analytics`](https://angular.kr/cli/analytics) |                | Angular CLI 사용 메트릭 수집을 구성                          |
| [`build`](https://angular.kr/cli/build)         | `b`            | 주어진 출력 경로에서 Angular 앱을 dist /라는 출력 디렉토리로 컴파일 (작업 공간 디렉토리 내에서 실행해야한다.) |
| [`config`](https://angular.kr/cli/config)       |                | 작업 공간의 angular.json 파일에서 각도 구성 값을 검색하거나 설정 |
| [`deploy`](https://angular.kr/cli/deploy)       |                | 작업 공간에서 지정된 프로젝트 또는 기본 프로젝트에 대한 배치 빌더를 호출 |
| [`doc`](https://angular.kr/cli/doc)             | `d`            | 브라우저에서 공식 Angular 문서 (angular.io)를 열고 주어진 키워드를 검색 |
| [`e2e`](https://angular.kr/cli/e2e)             | `e`            | Angular 앱을 빌드하고 제공 한 다음 각도기를 사용하여 엔드 투 엔드 테스트 |
| [`generate`](https://angular.kr/cli/generate)   | `g`            | 회로도를 기반으로 파일을 생성 및 / 또는 수정                 |
| [`help`](https://angular.kr/cli/help)           |                | 사용 가능한 명령과 간단한 설명을 나열                        |
| [`lint`](https://angular.kr/cli/lint)           | `l`            | 주어진 프로젝트 폴더의 Angular 앱 코드에서 Linting 도구를 실행 |
| [`new`](https://angular.kr/cli/new)             | `n`            | 새로운 작업 공간과 초기 Angular 앱을 생성                    |
| [`run`](https://angular.kr/cli/run)             |                | 프로젝트에 정의 된 선택적 사용자 정의 빌더 구성으로 Architect 대상을 실행 |
| [`serve`](https://angular.kr/cli/serve)         | `s`            | 파일 변경 사항을 다시 작성하여 앱을 빌드하고 제공            |
| [`test`](https://angular.kr/cli/test)           | `t`            | 프로젝트에서 단위 테스트를 실행                              |
| [`update`](https://angular.kr/cli/update)       |                | 응용 프로그램 및 해당 종속성을 업데이트                      |
| [`version`](https://angular.kr/cli/version)     | `v`            | Angular CLI 버전을 출력                                      |
| [`xi18n`](https://angular.kr/cli/xi18n)         | `i18n-extract` | 소스 코드에서 i18n 메시지를 추출                             |

> 앱 및 라이브러리에서 생성하거나 작동하는 [add](https://angular.kr/cli/add) 및 [generate](https://angular.kr/cli/generate) 와 같은 명령은 작업 영역 또는 프로젝트 폴더 내에서 실행해야한다.
>
> [ng generate](https://angular.kr/cli/generate) 명령을 사용하여 추가 구성 요소 및 서비스를위한 새 파일을 추가하고 새 파이프, 지시문 등을위한 코드를 추가할 수 있다.

>  [ng new](https://angular.kr/cli/new) 명령으로 작성된 초기 앱은 작업 공간의 최상위 레벨에 있으며, 작업 공간에서 추가 앱 또는 라이브러리를 생성하면 `projects/`하위 폴더로 이동 할 수 있다.