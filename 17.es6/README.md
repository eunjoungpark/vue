#Vue와 ES6

ES6는 ECMAScript 2015와 같은 의미로, ECMAScript의 6번째 주 버전을 발표한 것.

##let과 const
###let
* let는 호이스팅(hoisting) 문제 해결
* 지역스코프와 전역스코프를 분리하여 서로의 스코프를 침범하지 않음.
```javscript
//호이스팅
console.log(a); //결과 : undefined
var a = 10;

console.log(b); //결과 : Uncaught ReferenceError: b is not defined
let b = 10;

========================================================================

//스코프1 : 중복선언 방지
var a = 10;
var a = 20;
console.log(a); //결과 : 20

let a = 10;
let a = 20;
console.log(a); //결과 : Uncaught SyntaxError: Identifier 'a' has already been declared

========================================================================

//스코프2 : 값의 보장
var a = 10;
{
    var a = 20;
    console.log(a); //결과 : 20
}
console.log(a); //결과 : 20

let a = 10;
(function(){
    let a = 20;
    console.log(a);
})(); //결과 : 20

console.log(a); //결과 : 10
```

*\*호이스팅(hoisting)이란, 변수나 함수가 선언되기 전에 미리 최상위에 끌어올려져 해당 변수명이 등록만 되어있는 상태로 값을 출력하려고 할때 __undefined__ 를 출력함.*
*\* __undefined__ 는 변수는 존재지만 값인 대입되지 않은 상태임.*

###const
const는 상수를 정의할 때 사용하는 것으로, 불변하는 값을 선언하기 위한 키워드.
* 반드시 초기화 되어야 함.
* 대입을 다시하려고 할 때 오류발생
* 상수값이 객체 또는 배열을 경우 프로퍼티 수정가능.

```javascript
const a;
a = 10;
console.log(a); //결과 : Missing initializer in const declaration
```
##this
###일반함수의 this
```javascript
function outer(){
    console.log(this); //window
}
outer();
```
###중첩함수의 this
```javascript
function outer(){
    function inner(){
        console.log(this); //window
    }
    inner();
}
outer();
```
###메서드의 this
```javascript
function outer(){
    console.log(this); //outer
}
var out = new outer(); //인스턴스의 this는 인스턴스
```

###메서드 내부 중첩 함수의 this
```javascript
function outer(){
    console.log(this); //outer
    function inner(){
        console.log(this); //window
    }
    inner();
}
var out = new outer(); //인스턴스의 this는 인스턴스이지만
                    //중첩함수는 인스턴스로 인한 호출이 아니므로 이곳의 this는 window
```

###Object 내부 함수의 this
```javascript
var obj = {
    outer : function (){
        console.log(this); //outer    
    }
};
obj.outer(); //obj
            //무엇의 의해 호출되었을 때의 this는 호출한 객체가 됨.

```

###Object 내부 중첩함수의 this
```javascript
var obj = {
    outer : function (){
        console.log(this); //outer    
        function inner(){
            console.log(this); //window    
        }
        inner();
    }
};
obj.outer(); //obj
            //inner함수는 객체의 의해 호출된 것이 아니므로 this가 window임.
```

###이벤트 리스너의 this
```javascript
var btn = document.querySelector("button");
btn.addEventListener("click", function(){
    console.log(this); //btn
                    //객체의 의한 호출이므로 여기서의 this는 btn임.
}, false);
```
##arrow함수의 this
arrow함수는 부모가 바라보는 this를 따라감.

###일반함수의 this
```javascript
var outer = () => {
    console.log(this); //window
                    //최상위 함수의 this는 window임.
}
outer();
```
###중첩함수의 this
```javascript
var outer = () => {
    console.log(this); //window
    var inner = () => {
        console.log(this); //window
            //부모 outer가 window이기 때문에 inner도 window임.
    }
    inner();
}
outer();
```
###메서드 내부 중첩 함수의 this
```javascript
function outer(){
    console.log(this); //outer
    var inner = ()=>{
        console.log(this); //outer
        //부모인 outer의 this가 인스턴스이므로
        //inner arrow함수의 this도 인스턴스가 됨.
    }
    inner();
}
var out = new outer();
```

###Object 내부 함수의 this
```javascript
var obj = {
    outer : ()=>{
        console.log(this); //window    
        //잘 기억해보세요. arrow함수는 부모의 this를 따라가요!
        //arrow함수가 따라가 부모가 없죠? ^^
    }
};
obj.outer();
```

###Object 내부 중첩함수의 this
```javascript
var obj = {
    outer : ()=>{
        console.log(this); //window    
        var inner = ()=>{
            console.log(this); //window    
            //부모가 window이므로 내부함수의 this도 window임.
        }
        inner();
    }
};
obj.outer();
```

###이벤트 리스너의 this1
```javascript
var btn = document.querySelector("button");
btn.addEventListener("click", ()=>{
    console.log(this); //window
                    //일반함수 였다면 호출한 객체가 this값이 었겠지만
                    //arrow함수는 무조건 부모를 따라감.
}, false);
```
###이벤트 리스너의 this2
```javascript
var obj = {
    outer : function(){
        console.log(this);//객체내부 일반함수의 this는 객체.
        var btn = document.querySelector("button");
        btn.addEventListener("click", ()=>{
            console.log(this); //객체 obj
                        //객체내부로 이벤트리스너가 들어왔을때
                        //부모를 따라 this가 obj가 됨.
        }, false);
    }
};
obj.outer();
```

* scope 와 closure
* arrow function
* 객체 리터럴
* 스프레드 오퍼레이터
* 템플릿 리터럴
* 디스트럭처링
* import & export
* async & await
  
 
