# NPM

Node.js 기반 패키지 모듈들을 관리하는 도구.

## 설치

1. https://nodejs.org 에서 node.js설치
2. node와 npm 버전확인.

```
//버전을 확인함으로서 설치된 것을 확인.
> node -v
> npm -v
```

3. 모듈을 관리하기 위해, package.json 설정

```
> npm init //package.json 파일 생성
> npm init -y //기본선택 값으로, 질의없이 바로 package.json 생성
```

## NPM 명령어

```
> npm install [모듈명]
> npm i (축약어)
> npm install -g [모듈명] //글로벌 설치
> npm install --save-dev [모듈명] //개발모듈로 설치
> npm install --save [모듈명] //배포모듈로 설치 (앱구동을 위해 필요한 도구들)
> npm uninstall [모듈명] //설치된 모듈삭제
```

## package.json

- "script" : {} 에 필요한 명령어를 정의할 수 있음.

```javascript
{
  "name": "webpack-test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev" : "webpack-dev-server  --open",
    "build": "webpack"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {  //npm i --save vue시 해당 영역에 자동등재.
    "vue": "^2.5.11"
  },
  "devDependencies": { //npm i --save-dev webpack시 해당 영역에 자동등재.
    "@babel/core": "^7.2.2",
    "babel-loader": "^8.0.5",
    "webpack": "^4.28.1",
    "webpack-cli": "^3.2.1",
    "webpack-dev-server": "^3.1.14"
  }
}
```

_\* package.json만 있으면, 다른 환경에 세팅을 할 경우에, npm install 만으로 필요한 모듈 및 라이브러리를 한번에 설치할 수 있음._
