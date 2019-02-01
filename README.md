#VUE 소개

##VUE 설치

* NPM 명령어
* VUE2와 VUE3 차이점

##VUE 구조
* template
* script
* style

##DIRECTIVE
* v-text, v-html
* v-bind
* v-model
* v-show, v-if, v-else, v-else-if
* v-for

##INSTANCE
* new Vue()

##VUE DOM
* Virture DOM
* render 함수

##VUE 라이프사이클(LIFECYCLE)

##Template Syntax

* Mothods
* Computed
* Watch
* Filter

##COMPONENT

* Global
* Local
* props 속성

##SLOT

##EVENT
* v-click
* 키보드 수식어
* 마우스 수식어


##STYLE

##ROUTER
* 선언방법
```html
<router-view></router-view>
<router-link></router-link>
``` 
* path정의
    * 하위 path 정의
* name 속성
* parameter
    * params
    * query
* 라우터 인스턴스
* 멀티 라우터 뷰
* 리다이렉트
* 기타 고급기법

##VUEX
* 선언방법
* state
* mutations
    * commit
* actions
    * dispatch
* getters

##AXIOS
* promise

##VUE Loader


##VUE와 ES6
* let 과 const
* arrow function
* 객체 리터럴
* 스프레드 오퍼레이터
* 템플릿 리터럴
* 디스트럭처링
* import & export
* async & await




##webpack
WEBPACK

1. 역할 : 웹 자원(플러그인)들의 관계를 정립(관리)하여, js, css, image 들을 최적화해주는 모듈번들러 역할을 함.
2. 기본적으로 필요한 기능을 gulp, grunt에서는 설치&추가하였던 부분을 webpack자체에서 지원해줌.
3. 기존 javascript 작성방식 문제
	- 전역변수 충돌
	- 로딩순서
	- 복잡성으로 및 재사용을 위한 관리
4. webpack 4.*으로 버전업되면서 npm install webpack-cli -g 로 설치되게끔 바뀜.
(기존명령어 : npm install webpack)

5. lodash : 라이브러리

6. 간단한 번들링 명령어 
webpack [번들대상] [번들결과 파일명]

예) webpack app/index.js dist/bundle.js

7. require로 모듈을 가져올 경우, npm install [module name] --save로만 설치가능.
require없이 사용하고자 한다면 -g로 설치.

