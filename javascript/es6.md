#ES6

##let와 const
- 블록범위에서 유효한 변수 선언 키워드
- 전역에 let이나 const로 `window객체` 프로퍼티와 동일한 변수명을 사용하면, `window객체` 프로퍼티에 영향을 주지 않고 임시로 사용한다는 개념으로 변수를 선언할 수 있음.
*(var로 `window` 프로퍼티와 동일한 변수명으로 선언시, window 프로퍼티 값을 덮음)*

###let
\- 같은 블록범위 내에서 이미 선언된 동일한 변수명은 선언할 수 없음.
\- hoisting이 발생하지 않아, 선언전에 변수명을 호출할 경우 오류발생.
\- 반복문 문제해결
```javascript
var button = document.querySelectorAll("button");
    for(var i=0; i<3; i++){
        button[i].onclick = function(){
            console.log(i); // 모두 2를 출력, 이유는 i변수는 같은 값을 참조하므로 이미 for문으로 변경된 값을 참조하기 때문.
                            // let i 로 선언하면 스코프마다 다른 i를 생성하여 서로 다른 값을 참조하게 하여 해결.
        }    
    }
```

###const
\- 초기 선언시에 무조건 값을 할당하여 선언해야 함.
\- 한번 선언된 변수는 값을 변경할 수 없음.
\- 배열이나 객체는 참조값을 갖기 때문에 값 변경가능.
\- for-in과 for-of는 반복 실행 시마다 새로운 바인딩을 만듬. 즉, for(const fruit in fruits){}는 오류가 발생되지 않음.

##문자열 메서드
정규표현식 사용불가

|메서드|의미|
|---|---|
|`includes()`|문자열의 어느 곳에서든 주어진 문자를 찾으면 true를 반환|
|`startsWith()`|문자열의 시작점에서 주어진 문자를 찾으면 true를 반환|
|`endsWith()`|문자열의 끝에서 주어진 문자를 찾으면 true를 반환|
|`repeat()`|원본 문자열을 명시한 횟수만큼 반복하여 새로운 문자열 반환|

##문자열 문법
\- 백틱(`)으로 멀티라인 문자열 표현.
\- 치환자 ${} : 백틱 영역안에서 변수 사용 가능.
\- 템플릿 태그
```javascript
let count =10, price=0.25, greet = tag`${count} items cost ${price} hello`;

//인수1(test:문자열만 배열로 반환)
//인수2(...test2:변수값 나열)
function tag (test, ...test2){
    console.log(test); //[""," items cost "," hello"]
    console.log(...test2);//10 0.25
}
```

##함수
###인수에 기본값 설정
- 인수의 기본값으로 숫자선언가능
- 수식가능
- 첫번째 인수 선언가능
- 함수 선언가능
```javascript
function fn (number, compare = 11){
    return number + compare
}

function getValue(){
    return 5;
}

function fn2 (number, compare = getValue()){
    return number + compare
}

console.log(fn(10, 20)); //만약 다른 값 20을 할당하면, 11무시되고 20이 됨.
```
- arguments
ES5 strict모드에서는 인수의 값을 변경해도 변경되지 않음.
ES6에서는 모드와 상관없이 변경이 되지 않음.
```javascript
function fn (number, compare = 11){ //기본값 설정. 수식도 가능. 첫번째 인수값 설정가능.
    console.log(arguments[0]); //10
    console.log(arguments[1]); //20
    number = 1;                 //값이 새롭게 할당되도 arguments에 영향을 주지 않음.
    compare = 1;
    console.log(arguments[0]); //10
    console.log(arguments[1]); //20
}

fn(10, 20); //전달된 인자 수에 따라 argruments 수가 정해짐.
fn(10); //전달된 인자 수가 1개이므로 arguments[1]은 undefined가 됨.
```

###name 속성
```javascript
function doSomething(){}
var doAnotherThing = function(){}
console.log(doSomething.name); //"doSomething"
console.log(doAnotherThing.name); //"doAnotherThing"
```

##화살표함수
- 함수의 축약법
- 일반 function함수와 달리 호이스팅이 발생하지 않음.
- 생성자가 없어, new키워드 사용할 수 없음.
- prototype 프로퍼티가 없음.
- 함수의 전체 생명주기 내내 this값 동일.
- argruments객체 없음.
- 동일한 이름의 매개변수를 사용할 수 없음.
- 선언가능 방식

```javascript
//일반적 선언방식
var eun = () => {
    return "hello";
}

//{}와 return 생략
var eun = () => "hello";

//문장이 2줄 이상이면 {}, return 생략불가
var eun = (greet) => {
    var name = " eunjoung"
    return greet + name;
}

//인수가 한개이면, () 생략 가능
var eun = str => str;


//인수가 없거나 2개 이상이면 () 사용해야 함.
var eun = (greet,name) => greet + name;
```
- arrow함수의 this
    - arrow함수의 this는 전역선언일 경우 전역객체이며, 부모 함수의 this를 따라감.
    - this의 예
    
```javascript
//전역함수
var fn = ()=>{
    console.log(this); //window
}
fn();


//생성자로 선언된 함수
function Fn() {
    console.log(this); //Fn
    var sFn = () => {
        console.log(this); //Fn
    }
    sFn();
}
var fn = new Fn()

//객체 내부에 선언된 메소드
var obj = {
    fn : ()=>{
        console.log(this); //windows
    }
}

obj.fn();
```
##객체 리터럴
- 프로퍼티 초기자 축약

```javascript
var obj = {
    name : name, //이름과 값이 동일하면 축약 할수 있음.
    age : age
}

var name = "eun";
var age = 30;
var obj = {
    name, //이렇게되면 주변에 name과 age를 찾아 그 값을 할당.
    age
}
```

- 간결한 메서드

```javascript
var obj = {
    name : function(){
        return "eun";
    },
    name() {    // : fuction 이 생략됨.
        return "eun";
    }
}
```

- 계산된 프로퍼티 이름

```javascript
var lastname = "last name";
var justname = " eunjoung park";
var obj = {
    "first name" : "eunjoung", //문자열로 name을 설정
    [lastname] : "park", //상단에 선언된 "last name"을 []안에서 계산되어 사용.
    ["hello" + justname] : "hello park!!"  //[]안은 계산되어 문자열+변수 조합으로 사용할 수 있음.
}
console.log(obj["first name"]);
console.log(obj[lastname]);
console.log(obj["last name"]);
console.log(obj["hello eunjoung park"]);
```

- 나머지 연산자(스프레드 오퍼레이터) & 나머지 매개변수
    - 배열, 객체의 값을 열거하는 방식으로, 변수 나 인수로 표현 가능.
    - 나머지 매개변수의 경우 맨 마지막에 선언되어야 함.
    - 나머지 연산자로 배열과 객체를 전달할 시에 다른 값과 함께 사용가능.

```javascript
function printName(...name, age){ //...name 뒤에 다른 매개변수를 선언할 수 없음. age로 인해 오류발생
    for(var n in name){           // 출력 : 
        console.log(name[n]); // eun
                            // joung
                            // park 
    }
}

printName("eun","joung","park");
```
- 객체의 setter에 나머지변수를 사용할 수 없음. setter는 인수를 한 개만 받도록 설계되어있음. 
- 객체 메서드
    - Object.is() : 두 값을 비교하여 true, false로 반환.

```javascript
console.log(+0 == -0); //true
console.log(Object.is(+0,-0)); //false

console.log(NaN == NaN); //false
console.log(Object.is(NaN, NaN)); //true

console.log(5 == 5); //true
console.log(5 == "5"); //true

console.log(Object.is(5,5));//true
console.log(Object.is(5,"5"));//false
```

- Object.assign() : 객체 합성

```javascript
var receiver = {};
Object.assign(receiver, {
    type : "js",
    name : "file.js"
},{
    type : "css"
});

또는

var receiver = Object.assign({
    type : "js",
    name : "file.js"
},{
    type : "css"
});

console.log(receiver.type); //"css"
console.log(receiver.name); // "file.js"
```
- 객체속성 열거 
Object.getOwnPropertyNames(object name);

##구조분해
- 배열

```javascript
var num = [1,2,3];
var [a,b] = num; console.log(a, b); //1,2
var [a, ...b] = num; console.log(b); //[2,3]
var [a = 5, b, c, d = 4] = num; console.log(a,b,c,d); //1,2,3,4
var [a, , b] = num; console.log(a,b); //1,3

var a = 1;
var b =  2;
[b,a] = [a,b]; console.log(b,a); //1,2

var [a,b] = [1,2,3];console.log(a,b); //1,2
```

- 객체 : 할당할 대상의 변수명이 객체의 속성명과 동일 해야함.

```javascript
var obj = {
    name : "park",
    age : 30,
    greet (){
        console.log("hello!!!");
    }
} 
var {name, age, value, height = 160} = obj;
console.log(name , age); //park 30
console.log(value); //undefined
console.log(height); //160 - 초기값설정 가능

또는 

var name, age;
({name, age} = obj); 
console.log(name , age); //park 30


var {greet} = obj; 
greet(); //hello!!!

var {greet:hello} = obj; 
hello(); //hello!! - 변수명을 hello로 변경가능    
```
```javascript
//중첩된 객체 구조분해
let node = {
    type : "Identifier",
    name : "foo",
    loc : {
        start : {
            line : 1,
            column : 1
        }
    }
};

let {loc : {start}} = node;
console.log(start.line); //1
console.log(start.column); //1

let {loc : {start : localStart}} = node;
console.log(localStart.line); //1
console.log(localStart.column); //1
```

##Symbol
- 원시데이터형 (유형 : string, number, boolean, null, undefined, symbol)
- new 생성자 키워드를 지원하지 않음.
- 생성방법
```javascript
let symbol = new Symbol();
let symbol1 = new Symbol("sym1"); //문자열로 변수을 유추할 수 있게 함. 문자열은 toString()으로 출력하는 것 외에는
                                // 활용되지 않음.
let symbol2 = new Symbol.for("sym1"); //symbol2를 계속 활용 가능.
```
- 비공개 이름기능
```javascript
let name = Symbol.("name");
let person = {
    [name] : "park",
    age : 30
}
for(item in person){
    console.log(item); //[name]속성은 색인되지 않음.
}
```
- 유일무이한(항상 다른 ID) 값을 가짐.
```javascript
    console.log(Symbol("sym") === Symbol("sym")); //false 
```
- 유일한 식별자를 나타내면서 동일한 심벌 ID를 갖도록 처리도 가능함.(전역 심볼 저장소에 등록됨.)
```javascript
let symbol1 = Symbol.for("sym");
let symbol2 = Symbol.for("sym");
console.log(symbol1 === symbol2); //true
```

- 또다른 장점 : Symbol.for("age")가 person.age를 오버라이드 하지 않아, 다른 값을 액세스할 수 있음.
```javascript
let symbol = Symbol.for("age");

let person = {
    name : "eun",
    age : 30
}

function makeAge(obj){
    let anotherAge = Symbol.for("age");
    obj[anotherAge] = 27;
}
makeAge(person);
console.log(person[symbol]);
console.log(person["age"]);
```
- 심벌은 타입변환이 안됨.
```javascript
let symbol = Symbol("age");
console.log(symbol + "age"); //에러!
console.log(symbol + 1); //에러!
```
- 심벌 프로퍼티 열거
Object.getOwnPropertySymbols(object name);


##Set & Weak Set
###Set
- 배열 데이터를 저장함.
- 중복을 제거함.
- 키값이 없음.
- 삽입된 값의 타일을 강제변환(문자형)하지 않음.
- 배열처럼 인덱스 값으로 요소에 직접접근 불가.
- 값을 출력할 때, 이터레이터 사용.
- 메서드 종류
    - add(value) : 선택 요소 추가
    - delete(value) : 선택 요소 삭제
    - clear() : 인스턴스의 모든 값 삭제.
    - forEach(function(value,value,set){}, this) : set에 저장된 값을 순회. 두번째 인자로 this사용 가능.
    - size : 요소가 몇 개인지 반환.

```javascript
let set = new Set([1,2]);
let arr = [...set]; //배열로 변환가능.
set.forEach(function(value, value, setArray){
    console.log(value); //값을 넘기는 인자가 두개
});
```

###Weak Set
- 약한 Set
- 객체형 값만 받을 수 있음(가비지 컬렉터가 발생될 수 있는 유형에 적합).
- 이터러블이 아니므로 for-of 사용불가
- Weak Set안에 값 확인불가.
- forEach, size프로퍼티 제공하지 않음.
- 메서드 종류
    - add(value) : 선택 요소 추가
    - has(value) : 선택 요소 존재여부 반환.
    - delete(value) : 선택 요소 삭제

```javascript
let key1 = {};
let weakset = new WeakSet([key1]); //배열형태로 객체값을 초기화.
console.log(weakset.has(key1)); //true
```

##Map & Weak Map
###Map
- 키와 값이 한쌍인 컬렉션임.
- 메서드 종류
    - set(key, value) : 값 추가
    - get(key) : 값 반환
    - has(key) : 키값 존재 여부 반환.
    - delete(key) : 키와 키의 값 제거
    - clear() : map의 내용 모두 제거
    - size : 요소가 몇 개인지 반환.
    - forEach(function(value,key,map){}, this) : map의 요소를 순회. 두번째 인자로 this사용 가능.

###Weak Map
- 약한 Map
- 모든 키가 객체여야 함.
- Weak Map은 DOM 요소의 객체를 만들때 적합.
- forEach(), clear(), size프로퍼티 지원안함.
- 메서드 종류
    - set(key, value) : 값 추가
    - get(key) : 값 반환.
    - has(key) : 키값 존재 여부 반환.
    - delete(key) : 키와 키의 값 삭제 
    
```javascript
let key1 = {};
let weakmap = new WeakMap([key1,"key1Value"]); //배열형태로 객체값을 초기화.
console.log(weakmap.get(key1)); //"key1Value"
```


*\* es6 지원상황 : [https://kangax.github.io/compat-table/es6/*](https://kangax.github.io/compat-table/es6/)*

