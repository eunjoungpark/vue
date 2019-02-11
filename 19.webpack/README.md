#Webpack
웹 자원(플러그인)들의 관계를 정립(관리)하여, js, css, image 들을 최적화해주는 모듈번들러 역할을 함.

##모듈러가 나온 배경
* client side에 코드량이 많아지고, JS의 역할이 커지면서 복잡한 웹앱을 관리하기 위해  
Common JS, AMD, ES6 Modules가 등장하게 됨.
* 전역변수의 충돌, 스크립트 로딩순서와 복잡도를 효율정으로 관리하고자 하는 Needs가 있음.

##다른 자동화 도구와 차이점
* 기본적으로 필요한 기능을 gulp, grunt에서는 설치&추가하였던 부분을 webpack자체에서 지원해줌.
* Grunt, Gulp는 오로지 리소스들에 대한 툴로 사용되며 모듈의 의존성에 대한 개념이 없음.
* 초기에 불필요한 것들을 모두 로딩하지 않고, 필요할 때 필요한 것만 로딩함.
* 모듈간의 관계를 청크단위로 나눠 필요할 때 로딩
* 가독성이나 다수 모듈 미병행 처리등의 약점을 보완.
* Loader가 존재하여 순수 JavaScript로 변환하고 모든 리소스에 대한 모듈을 구성해 줌.
* 비슷한 도구로 Browsify가 있는데, Webpack이 보다 속도가 빠름.

*\* 청크(chunk)란 코드 혹은 모듈을 묶는 하나의 단위.*

##Webpack 설치
```
//webpack 3.x
npm install -g webpack //글로벌 설치
npm install --save-dev webpack //개발영역에 설치
npm install --save-dev webpack@<version> //특정버전 설치

//webpack 4.x
npm install webpack-cli -g //webpack4 부터는 cli를 추가 설치해야 함.
```

##Webpack 설정
1. 프로젝트 최상단에 (package.json이 있다면 같은 경로) **webpack.config.js** 생성.
2. 아래와 같이 기본설정을 구성.
```javascript
var path = require('path');

module.exports = {
  mode: 'none', //webpack4에 추가된 옵션으로 'development'는 개발용, 'production'은 배포용임.
  entry: ['./app/index.js'], //관리할 대상
  output: {
    filename: 'bundle.js', //번들후 배출파일
    path: path.resolve(__dirname, 'dist'), //배출경로
  },
  module: {
    rules: [
      { 
        test: /\.js$/,  //관리대상 파일 확장자
        exclude: /node_modules/, //관리에서 제외할 폴더
      }
    ]
  }
};

```
##번들링 명령어
```
webpack [번들대상] //1회성 번들링
webpack [번들대상] [번들결과] //번들링과 동시에, 결과를 배출할 경로 및 파일명을 설정.
 예) webpack app/index.js dist/bundle.js
webpack [번들대상] -w //계속적인 번들링을 원할 경우, watch모드로 번들.
```

##기타 명령어
* webpack ‐p : minification 기능이 들어간 빌드 (주로 배포용)
* webpack ‐d : sourcemap 포함하여 빌드
* webpack ‐‐display‐error‐details : error 발생시 디버깅 정보를 상세히 출력
* webpack ‐‐optimize‐minimize ‐‐define process.env.NODE_ENV="'production'" : 배포용
* webpack-dev-server --open : 로컬 개발서버를 구동 (--open은 선택)

###참고사이트
* https://haviyj.tistory.com/17
* https://jijong.github.io/2018-08-24/webpack_envirment/#nodejs--npm
* https://github.com/ipadorusa/sri-vuejs/wiki/Grunt-or-Gulp-vs-Webpack-%EC%9D%98-%EC%B0%A8%EC%9D%B4
