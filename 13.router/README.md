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

//////////////////////////////////////////////////////////////////////
1. 정의방법
import Vue from 'vue';
import VueRouter from 'vue-router';

Vue.use(VueRouter);

const router = new VueRouter({
	mode : 'history',
	routes : [
		{path : '', component : '', name : ''}
	]
});

render함수에 router 정의.


2. router path 정의
	└ 파라미터 : to="/user/:id"   =>  /user/[something]


3. navication : <router-link></router-link>
	└ 정확인 주소와 매칭 속성 : exact
	└ 명시는 <router-link>로 하고 렌더링은 <li> 할때 : tag="li"
	└ path 정의 : to="path"
	└ 활성화 class 정의 : active-class="class name"



4. content : <router-view></router-view>
   노출하고 싶은 영역을 알려주는 역할로, 해당 태그가 지정된 영역에 화면이 표시됨.


5. 자바스크립트 지원
	└ 특정페이지로 이동 : this.$router.push('/);
	└ └ Name 으로 이동 : this.$router.push({name : 'home'});
	└ 파라미터값 출력() :
		(단, id값이 변경되면 값이 업데이트 되지 않음.)
		data(){
			return {
				id : this.$route.params.id
			}
		}

	└ 파라미터값 출력2 : 
		(업데이트 되기 위한 방법으로 watch로 감시를 걸어놓음.)
		watch:{
			'$route'(to, from){
				this.id = to.params.id
			}
		}

6. 하위 컴포넌트 정의
	아래와 같이 특정 뎁스에서 하위 뎁스를 children으로 정의할 수 있음.
	{path : '', component : '', children : [
		{path : '', component : ''},
		{path : '', component : ''}
	]};

7. name 속성으로 이동
router 설정에서 component name을 지정하고
<router-link :to="{name : [name]}"></router-link> 태그에
name과 parameter를 설정할 수 있음.


8. params 속성으로 이동
<router-link :to="{name : [name], params : {id : $route.params.id}}"></router-link>


9. query 속성 사용.
<router-link :to="{name : [name], params : {id : $route.params.id}, query:{locale : 'ko', q:100}}"></router-link>


10. Multiple Router Views
	//html
	<router-view name="header-top"></router-view>
	<router-view></router-view>
	<router-view name="header-bottom"></router-view>

	//router
	{path : '/', name : 'home', components : {
        default : Home,
        'header-top' : Header
    }}


11. 리다이렉트
{path : '/redirect-me', redirect : {name : 'home'}}
{path : '*', redirect : '/'}

12. 기타
- 페이지전환 애니메이션
- hash값(페이지 이동) 무시
- 페이지전환 높이설정 가능.
- router.beforeEch((to, from, next)=>{});
- router.beforeEnter((to, from, next)=>{});
- router.beforeLeave((to, from, next)=>{});
- 컴포넌트 안에서 사용 할때
	- beforeRouteEnter(to, from, next){}
	- beforeRouteLeave(to, from, next){}
- 지연된 로딩 대처 : 코드분할()



