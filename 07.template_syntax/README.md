#Template Syntax
* v-text
* v-html
* v-show
* v-if, v-else-if, v-else
* v-for
* v-on
* v-bind
* v-model
* v-pre
* v-cloak
* v-once

```html
<template>
    <div>
        <!-- 보간법 : 데이터바인딩 1 -->
        <div>{{msg}}</div>

        <!-- 위 보간법과 동일한 결과 : 데이터바인딩 2 -->
        <div v-text="msg"></div>
        
        <!-- 담고 싶은 데이터를 string이 아닌 html형식으로 출력함. -->
        <div v-html></div>
        
        <!-- ok 값이 true이면 영역이 노출되고, false이면 style="display:none"으로 가려짐. -->
        <div v-show="ok">{{msg}}</div>
        
        <!-- who 값에 맞는 데이터를 노출함(조건에 맞지 않은 영역은 DOM에 포함되지 않음.) -->
        <div v-if="who == 'girl'">영희</div>
        <div v-else-if="who == 'boy'">철수</div>
        <div v-else>바둑이</div>

        <!-- 배열의 길이만큼 값을 뿌려줌. value, key, index의 값을 사용할수 있음. -->
        <!-- v-for와 v-if가 함께 사용될때, v-for의 우선순위가 높음. -->
        <!-- 2.2.0 이상에서 v-for는 key 가 필수 -->
        <ul>
            <li v-for="(fruit, key, index) in fruits" :key="index">{{fruit}}</li>
        </ul>
        
        <!-- 이벤트를 사용할때, v-on를 사용. 약어는 @ -->
        <!-- 키보드 및 마우스 이벤트 모두 정의 가능 -->
        <!-- 이벤트의 수식어를 사용할 수 있음. -->
        <button v-on:click="message()"></button>
        <button @click="message()"></button> <!-- //약어사용-->
        <button v-on:click.prevent="message()"></button>
    </div>
</template>
```
```javascript
export default {
    data : function(){
        return {
            msg : 'Hello World!!',
            ok : true,
            who : 'girl', //or 'boy' or 'dog'
            fruits : ['apple', 'banana', 'orange'],
        }
    },
    methods : {
        message : function(){
            alert(this.msg);
        }
    }
}
```