vue 
	=> actions에 정의된 메소드를 dispath로 호출 
	=> mutations에 정의된 메소드를 commit로 호출
store > state => data
store > mutations (methods 에 정의)
	=> state 값을 변경하기 위한 역할 (상태변화를 추적하는데 주안점을 둠.)
	=> state 값을 동기적으로 변경하기 위해 commit을 사용 (commit은 외부에서 사용하는 것임.)
	=> commit 대신에, 컴포넌트의 메소드를 mapping하여 사용할수 있음(mapMutations)
	=> actions으로 받은 data를 state에 정의 (actions에서 정의한 이름으로 값정의)
store > actions 
	=> 비동기 mutations 로직을 위한 역할
	=> setTimeout() 이나 서버와의 http 통신 처리 같이 결과를 받아올 타이밍이 예측되지 않은 로직은 Actions 에 선언
	=> 메소드를 선언 (vue에서 사용할 메소드 이름)
	=> commit으로 mutation(사용될 이름을 정의)에 값을 전달(상태변화를 관리하기 위해 mutations를 이용)
	=> action에 정의된 메소드를 dispath로 호출
store > getters (computed 에 정의)
	=> state값을 받아오기 위한 역할
	=> 컴포넌트 내부의 computed에 mapGetters를 정의하여 사용할 수 있음.
	=> getters에 정의한 메소드를 호출할 때는 직접 호출할수 있음 ( this.$store.getters.정의된메소드) 
	=> 단, 컴포넌트의 다른 computed 정의와 같이 사용하기 위해 ...mapGetters로 정의필요.
	=> ...mapGetters 이 ...문법은 es6이므로 babel stage-2와 babel preset이 필요.