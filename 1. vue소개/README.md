#VUE 소개

##VUE 란?
SPA(Single Page Application) 개발을 위한 JAVASCRIPT 프레임웍 중에 하나로,
MVVM 패턴의 뷰모델(ViewModel) 레이어에 해당하는 화면(view)단 라이브러리.
![mvvm](../images/view_viewmodel_model.png)  

##특징
* 점진적으로 적용할 수 있게 설계
* Angular와 React 보다 가볍고 빠름  
* vue.js에는 컨트롤러가 없다. (초기화 메서드로 커스텀로직 수행)  
* vue는 Angular와 React의 몇가지의 특징을 착안하여 만들어진 언어. 
    * Angular  
        * data binding간의 데이터는 양방향(2way) 통신을 함.  
    * React  
        * component간의 통신은 단방향(1way) 통신을 함.  
        * Virtual Dom 렌더링 [자세히 알아보기](/zzangsuni/vue/src/master/05.vue_dom/)  


##MVVM 이란?
Backend 로직과 Client(마크업&스타일) 의 분리를 위한 구조로, MVC패턴 방식에서 기인함.  
화면앞단의 동작 관련 로직과 뒷단의 DB데이터 처리 및 서버 로직을 분리하고, 뒷단에서 넘어온  
데이터를 Model에 담아 View로 넘겨주는 중간 지점임.