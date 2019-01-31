#VUE INSTANCE

new Vue 생성자를 통해, 화면 단위로 사용될 data 및 함수, 라이프사이클 등을 정의 함.  

\* 주의 : data : function(){ return {}} 와 같이 data 속성을 정의 하지않으면, 모든 컴포넌트에서 데이터 조작이 가능해지므로 해당 컴포넌트의 스코프로 지정해야 함.

```javascript
var vm = new Vue({
    data : function(){
        return {
            message : 'hi'
        }
    },
    components : {

    },
    methods : {
        welcome : function(){
            console.log(this.message);
        }
    },
    computed : {
        hi : function(){
            return this.message;
        }
    },
    watch:{
        message : function(value){
            this.message = value + " world!!";
        }
    },
    created : function(){},
    mounted : function(){}
    //something to do...
});
```
