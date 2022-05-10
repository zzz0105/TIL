# Vue

## Intro

- Front-End Development
  - HTML, CSS 그리고 JavaScript를 활용해서 <u>DB의 데이터를 볼 수 있게 만들어 줌</u>
    - 이 작업을 통해 사용자(User)는 데이터와 상호작용(Interaction)할 수 있음
  - 대표적인 프론트엔드 프레임워크
    - Vue.js, React, Angular
- Vue.js
  - 사용자 인터페이스(화면)를 만들기 위한 진보적인 자바스크립트 프레임워크
  - 현대적인 tool과 다양한 라이브러리를 통해 SPA(Single Page Application)를 완벽하게 지원
  - [참고] Evan You에 의해 발표(2014)
    - 구글의 Angular 개발자 출신
    - 학사 미술, 미술사 전공 / 석사 디자인 & 테크놀로지 전공
    - 구글 Angular보다 더 가볍고, 간편하게 사용할 수 있는 프레임워크를 만들기 위해 개발
- SPA: Single Page Application(단일 페이지 어플리케이션)
  - What is SPA?
    - 현재 페이지를 동적으로 렌더링함으로써 사용자와 소통하는 웹 애플리케이션
      - 장고는 page가 많았다. (signup/index 등등..) 나중에는 한 장으로 가능
    - 단일 페이지로 구성되며 서버로부터 최초에만 페이지를 다운로드하고, 이후에는 동적으로 DOM을 구성
      - 처음 페이지를 받은 이후부터는 서버로부터 새로운 전체 페이지를 불러오는 것이 아닌, <u>현재 페이지 중 필요한 부분만 동적으로 다시 작성함</u>
    - 연속되는 페이지 간의 사용자 경험(UX)을 향상
      - 모바일 사용량이 증가하고 있는 현재 트래픽의 감소와 속도, 사용성, 반응성의 향상은 매우 중요하기 때문
    - 동작 원리의 일부가 <u>CSR(Client Side Rendering)의 구조</u>를 따름
  - SPA 등장 배경
    - 과거 웹 사이트들은 요청에 따라 매번 새로운 페이지를 응답하는 방식(MPA: Multi Page Application)이었음 
    - 스마트폰이 등장하면서 모바일 최적화의 필요성이 대두됨(모바일 네이티브 앱과 같은 형태의 웹 페이지가 필요해짐)
    - 이러한 문제를 해결하기 위해 Vue.js와 같은 프론트엔드 프레임워크(CSR: Client Side Rendering, SPA: Single Page Application)가 등장 - => CSR(Client Side Rendering), SPA(Single Page Application)의 등장
    - 1개의 웹 페이지에서 여러 동작이 이루어지며 모바일 앱과 비슷한 형태의 사용자 경험을 제공
- CSR: Client Side Rendering
  - What is CSR?
    - 서버에서 화면을 구성하는 SSR 방식과 달리 클라이언트에서 화면을 구성
      - CSR과 SSR은 '<u>누가 HTML을 만드냐</u>'에 따라 구분
    - 최초 요청 시 HTML, CSS, JS 등 데이터를 제외한 각종 리소스를 응답받고 이후 클라이언트에서는 필요한 데이터만 요청해 JS로 DOM을 렌더링하는 방식
    - 즉, 처음엔 뼈대만 받고 <u>브라우저에서</u> 동적으로 DOM을 그림
    - SPA가 사용하는 렌더링 방식
  - CSR 동작 방식
    - 서버에서 html 준다 -> 그 안에 JS 코드있다 -> 브라우저가 Javacript 실행 -> 화면이 그려진다
  - 장점
    1. 서버와 클라이언트 간 트래픽 감소(사용자가 많이 머물수록)	
       - 웹 애플리케이션에 필요한 모든 정적 리소스를 최초에 한 번 다운로드 후 필요한 데이터 갱신
    2. 사용자 경험(UX) 향상
       - 전체 페이지를 다시 렌더링하지 않고 변경되는 부분만을 갱신하기 때문
  - 단점
    1. SSR에 비해 전체 페이지 최종 렌더링 시점이 느림
    2. SEO(검색 엔진-ex)네이버,구글- 최적화)에 어려움이 있음(스파이더 봇이 보면서 정보를 수집할 때 meta데이터만 보는데, 최초 문서에 데이터 마크업이 없기 때문에 어려움이 있다)
- SSR: Server Side Rendering
  - What is SSR?
    - 서버에서 클라이언트에게 보여줄 페이지를 <u>모두 구성</u>하여 전달하는 방식
    - JS 웹 프레임워크 이전에 사용되던 <u>전통적인 렌더링 방식</u> ex) Django
  - SSR 동작 방식
    - 서버가 html 완전 최종본을 만들어내고 사용자에게 넘긴다. (사용자가 볼 수 있음)
      - ex) 장고 템플릿이 html로 바뀌어감.(장고 템플릿 엔진-서버-이 해줌) 
  - 장점
    1. 초기 구동 속도가 빠름
       - 클라이언트가 빠르게 컨텐츠를 볼 수 있음
    2. SEO(검색 엔진 최적화)에 적합
       - DOM에 이미 모든 데이터가 작성되어있기 떄문
  - 단점
    1. 모든 요청마다 새로운 페이지를 구성하여 전달
       - 반복되는 전체 새로고침으로 인해 사용자 경험이 떨어짐
       - 상대적으로 트래픽이 많아 서버의 부담이 클 수 있음
- SSR & CSR
  - 두 방식의 차이는 <u>렌더링의 주체가 누구인가</u>에 따라 결정
  - 즉, 실제 브라우저에 그려질(렌더링) HTML을 <u>서버가 만든다면 SSR, 클라이언트가 만든다면 CSR</u>
  - SSR과 CSR을 단순 비교하여 '어떤 것이 더 좋다'가 아니라, 내 서비스 또는 프로젝트 구성에 맞는 방법을 <u>적절하게 선택</u>하는 것이 중요
    - 비용적 측면으로는 CSR이 유리
      - script를 다 던져주면 브라우저(클라이언트)가 조립해준다. DIY..
  - 예를 들어, Django에서 Axios를 활용한 좋아요/팔로우 로직의 경우 대부분은 Server에서 완성된 HTML을 제공하는 구조(SSR)
  - 단, 특정 요소(좋아요/팔로우)만 JS(AJAX & DOM 조작)를 활용(CSR)
    - AJAX를 활용해 비동기 요청으로 필요한 데이터를 클라이언트에서 서버로 직접 요청을 보내 받아오고 <u>JS를 활용해 DOM을 조작</u>
- [참고] SEO: Search Engine Optimization(검색 엔진 최적화)
  - What is SEO?
    - 웹 페이지 검색 엔진이 자료를 수집하고 순위를 매기는 방식에 맞게 웹 페이지를 구성해서 검색 결과의 상위에 노출될 수 있도록 하는 작업
    - 인터넷 마케팅 방법 중 하나
    - 구글의 등장 이후 검색엔진들이 컨텐츠의 신뢰도를 파악하는 기초 지표로 사용됨
      - 다른 웹 사이트에서 얼마나 인용되었나를 반영
      - 결국 타 사이트에서 인용되는 횟수를 늘리는 방향으로 최적화
  - SEO 대응
    - Vue.js 또는 React 등의 SPA 프레임워크는 SSR을 지원하는 SEO 대응 기술이 이미 존재
      - SEO 대응이 필요한 페이지에 대해서는 선별적 SEO 대응 가능
    - 혹은 추가로 별도의 프레임워크를 사용하기도 함
      - Nuxt.js
        - Vue.js 응용 프로그램을 만들기 위한 프레임워크
        - SSR 지원
      - Next.js
        - React 응용 프로그램을 만들기 위한 프레임워크
        - SSR 지원
- Vue.js 역할
  - Vue를 사용하지 않았을 때
    - Django(서버)에서는 렌더링 준비가 끝난 HTML이 그대로 브라우저로 오고, 그걸 렌더링해서 보여줌
      - MTV는 Django에...
  - Vue를 사용할 때
    - Django(서버)에서 JSON만 보냄. 일은 브라우저가 한다.(Vue는 템플릿 역할을 한다)
      - Django에서는 MV만 한다(모델과 뷰. === 데이터베이스와 중간 관리자 ==> DRF로 가겠다~)



## Why Vue.js?

- 현대 웹 페이지는 페이지 규모가 계속해서 커지고 있으며, 그만큼 사용하는 데이터도 늘어나고 사용자와의 상호작용도 많이 이루어짐

- 결국 Vanilla JS 만으로는 관리하기 어려움
  - ex) 페이스북 친구가 이름을 수정했을 때
    - 화면상에서 변경되어야 하는 것들: 타임라인의 이름, 페이스북 메세지 상의 이름, 내 주소록에서의 친구 이름 등
    
      => 페이스북이 React를 개발한 이유
  
- Django 좋아요 with 바닐라 JS 예시

  - 코드의 반복. 선택한다(-무엇을) /  선택(-잡는다) -> 이벤트 등록 -> 변경
  - 명령형 프로그래밍. 극한의 백지상태라서 <u>하나하나 다 설정</u>해줘야함
  - 선택해야하는 데이터와 동시에 변경되어야 하는 요소가 많아진다면? -> **불필요한 코드의 반복** 
    => 이걸 뷰로 한 번에 관리 가능(data가 바뀜 -> DOM re-render)

- Vanilla JS vs Vue.js
  
  - Vanilla JS
    - 한 유저가 작성한 게시글이 DOM 상에 100개 존재
    - 이 유저가 닉네임을 변경하면, DB의 Update와 별도로 DOM 상의 <u>100개의 작성자 이름이 모두 수정</u>되어야 함
    - '모든 요소'를 선택해서 '이벤트'를 등록하고 값을 변경해야 함
  - Vue.js
    - **DOM과 Data가 연결**되어 있고 Data를 변경하면 이에 연결된 DOM은 <u>알아서 변경</u>(reactive)
    - 즉, 우리가 신경써야할 것은 오직 **Data에 대한 관리(DX -Developer Exp- 향상)**



## Concepts of Vue.js

- MVVM Pattern

  - 애플리케이션 로직을 UI로부터 분리하기 위해 설계된 디자인 패턴

  - 구성 요소

    1. Model

       > Vue에서 Model은 JavaScript **Object**다.

       - Object === {key:value}
       - Model은 Vue Instance 내부에서 **data**라는 이름으로 존재
       - 이 data가 바뀌면 View(DOM)가 반응

    2. View

       >  Vue에서 View는 **DOM(HTML)**이다

       - Data의 변화에 따라서 바뀌는 대상

    3. View Model

       > Vue에서 ViewModel은 모든 Vue Instance이다

       - DOM과 Data의 중개자
       - View와 Model 사이에서 Data와 DOM에 관련된 모든 일을 처리
       - ViewModel을 활용해 Data를 얼마만큼 잘 처리해서 보여줄 것인지(DOM)를 고민하는 것

### Vue Version 2 vs 3

> Official main version === Vue 3

- Vue 3
  - 2022년 2월부터 vue 프레임워크의 기본 버전이 3.x로 전환
  - CDN or npm을 통한 설치 시 자동으로 Vue 3로 설정
- Vue 2
  - 실무에서 여전히 Vue 2가 많이 사용됨(legacy code)
  - Vue 2의 생태계(문서, 튜토리얼, 자료, QnA 등)가 더 성숙함
  - 코어/커뮤니티 라이브러리의 호환 역시 Vue 2가 더 안정적
- 참고자료가 많은 Vue2로 학습 후, Vue 3로 이전(migration)하는 게 가장 효과적



## Quick Start of Vue.js

- Django & Vue.js 코드 작성 순서

  - Django

    > 데이터의 흐름

    - url -> views -> template

  - Vue.js

    > **Data가 변화하면 DOM이 변경**

    1. Data 로직 작성
    2. DOM 작성

- Vue 기초 코드

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue Quick Start</title>
  </head>
  <body>
    <!-- 2. 선언적 렌더링 -->
    <h2>선언적 렌더링</h2>	//View
    <div id="app1"> 
      {{  message  }}
    </div>
      
    <!-- 3. 엘리멘트 속성 바인딩 -->
    <h2>Element 속성 바인딩</h2>
    <div id="app2"> 
      {{  message  }}
    </div>    
      
    <!-- 4. 조건 -->
    <h2>조건</h2>
    <div id="app3"> 
      <p v-if="seen">보인다</p> <!-- v-: 디렉티브. 뷰한테 일 시키는 일 -->
    </div> 
      
    <!-- 5. 반복 -->
    <h2>반복</h2>
    <div id="app4">
  	<ol>
        <li v-for="todo in todos">
          {{  todo.text  }}
        </li>
      </ol>    
    </div>
      
    <!-- 6. 사용자 입력 핸들링 -->
    <h2>사용자 입력 핸들링</h2>
    <div id="app5"> 
      <p>{{  message  }}</p>
      <input v-model="message" type="text">	<!-- 알아서 동기화됨 -->
      <button v-on:click="reversedMessage">로구꺼</button>	<!--  클릭하면 이벤트 발생  -->
    </div>
      
    <!-- 1. Vue CDN -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      // 2. 선언적 렌더링
  	const app1 = new Vue({	//ViewModel
          el: '#app1',	//element. app1과 묶이게 된다
          data: {	//Model
              message: "안녕하세요 Vue"
          }	
      })
      
      // 3. 엘리먼트 속성 바인딩
  	const app2 = new Vue({
          el: '#app2',
          data:{
              message: `이 메세지는 ${new Data()}에 로드됨`
          }
      })
      
      // 4. 조건
  	const app3 = new Vue({
          el: '#app3',
          date:{
              seen: true,	//보이냐
          }
      })
      
      // 5. 반복
  	const app4 = new Vue({
          el:'#app4',
          data:{
              todos: {
                  {text: 'js복습'},
              	{text: 'vue 배우기'}
              }
          }
      })
      
      // 6. 사용자 입력 핸들링
      const app5 = new Vue({
          el: '#app5',
          data:{
              message: '안녕하세요'
          },
          methods:{	//this 어케 동작..? 실제 동작할 때는 뷰가 정리해서 해준다(프록시). this는 메서드가 속한 객체를 의미. 메서드 화살표 함수로 바뀌면 안됨~메서드 축약해서 쓸 수 있다(: function 생략)
              reversedMessage: function () {	//메세지 뒤집기
                  this.message = this.message.split('').reverse().join('')
              }
          }
      })
    </script>
  </body>
  </html>
  ```

   

## Basic Syntax

- Vue instance

  ```html
  <div id="app">
    {{  message  }}
    {{  greeting()  }}
  </div>
  <script>
  const app = new Vue(	//object
    {  //options
    el: '#app',
    data: {
  	message: 'Hello',
    },
    methods: {
        greeting: function () {
          const newMessage = this.message + '!'
          console.log(newMessage)
          return newMessage
      }
    }
  })
  </script>
  ```

  - 모든 Vue 앱은 Vue 함수로 <u>새 인스턴스를 만드는 것부터</u> 시작
  - Vue 인스턴스를 생성할 때는 Options 객체를 전달해야 함
  - 여러 Options들을 사용하여 원하는 동작을 구현
  - Vue Instance === Vue Component
  - options/DOM
    1. el
       - Vue 인스턴스에 <u>연결(마운트)</u>할 기존 DOM 요소가 필요
       - CSS 선택자 문자열 혹은 HTML Element로 작성
       - new를 이용한 인스턴스 <u>생성 때만 사용</u>
    2. data
       - Vue 인스턴스의 객체
       - Vue 인스턴스의 상태 데이터를 <u>정의</u>하는 곳
       - Vue template에서 interpolation을 통해 접근 가능
       - v-bind, v-on과 같은 <u>directive에서도 사용 가능</u>
       - Vue 객체 내 다른 함수에서 <u>this 키워드를 통해 접근 가능</u>
    3. methods
       - Vue 인스턴스에 <u>추가할 메서드</u>
       - Vue template에서 <u>interpolation을 통해 접근 가능</u>
       - v-on과 같은 <u>directive에서도 사용 가능</u>
       - Vue 객체 내 다른 함수에서 <u>this 키워드를 통해 접근 가능</u>
         - this 키워드: Vue 함수 객체 내에서 <u>vue 인스턴스</u>를 가리킴. data와 method 정의에서는 화살표 함수를 사용하면 안된다
       - **[주의]**
         - **화살표 함수를 메서드를 정의하는데 사용하면 안 됨**
           - 화살표 함수가 부모 컨텍스트를 <u>바인딩</u>하기 때문에, <u>'this'는 Vue 인스턴스가 아님.</u>

### Template Syntax

> 렌더링된 DOM을 기본 Vue 인스턴스의 데이터에 선언적으로 바인딩할 수 있는 HTML 기반 템플릿 구문을 사용

1. Interpolation(보간법, 값 대입): Vue 인스턴스의 데이터를 HTML 템플릿에 표현하기 위함

   ```html
   <!-- 1. Text  --> 
   <span>메세지: {{  msg  }}</span>
   
   <!-- 2. Raw HTML  -->
   <span v-html="rawHtml"></span>
   
   <!-- 3. Attributes -->
   <div v-bind:id="dynamicId"></div>
   
   <!-- 4. JS 표현식 -->
   {{  number + 1  }}
   {{  message.split('').reverse().join('')  }}
   ```

2. Directive(지시문. 동적 전달인자)

   - **v-** 접두사가 있는 특수 속성
   - 속성 값은 단일 JS 표현식이 됨 = 변수명만 쓴다(v-for는 예외)
   - 표현식의 값이 변경될 때 반응적으로 DOM에 적용하는 역할을 함
   - **전달인자(Arguments)**
     
     - :(콜론)을 통해 전달인자를 받을수도 있음
   - **수식어(Modifiers)**
     - .(점)으로 표시되는 특수 접미사
     - directive를 특별한 방법으로 바인딩해야 함을 나타냄

   - 종류

     - v-text

       ```html
       <div id="app">
         <p>{{ message }}</p>
         <p v-text="message"></p>
       </div>

       <script>
         const app = new Vue({
       	el: '#app',
       	data: {
       	  message: 'Hello'
       	}
         })
       </script>
       ```
       
     - 엘리먼트의 textContent를 업데이트
       
        - 내부적으로 interpolation 문법이 v-text로 컴파일 됨
        
      - v-html

        ```html
        <div id="app">
          <p v-html="message"></p>	
        </div>
          
        <script>
          const app = new Vue({
        	el: '#app',
        	data: {
        	  message: '<strong>강함</strong>'
        	}
          })
          </script>
        ```

        - 엘리먼트의 innerHTML을 업데이트
          - XSS 공격에 취약할 수 있음
          - 임의로 사용자로부터 입력받은 내용은 v-html에 **'절대' 사용 금지**

      - v-show

        ```html
        <div id="app">
          <p v-show="isTrue">TRUE</p>
          <p v-show="isFalse">FALSE</p>
        </div>
        
        <script>
          const app = new Vue({
            el: '#app',
            data: {
              isTrue: true,
              isFalse: false,
            }
          })
        </script>
        ```

        - 조건부 렌더링 중 하나. true일 때 보인다
        - 요소는 항상 렌더링되고 <u>DOM에 남아있음</u>
        - 단순히 엘리먼트에 display CSS 속성을 **토글**하는 것

      - v-if, v-else-if, v-else

        ```html
        <div id="app">
          <p v-if="seen">seen is TRUE</p>
            
          <p v-if="myType === 'A'">A</p>
          <p v-else-if="myType === 'B'">B</p>
          <p v-else-if="myType === 'C'">C</p>
          <p v-else>NOT A/B/C</p>
        </div>
        
        <script>
          const app = new Vue({
            el: '#app',
            data: {
              seen: false,
              myType: 'A',
            }
          })
        </script>
        ```

        - 조건부 렌더링 중 하나
        - 조건에 따라 요소를 렌더링
        - directive의 표현식이 true일 때만 렌더링
        - 엘리먼트 및 포함된 directive는 토글하는 동안 삭제되고 다시 작성됨
        - 출력화면에 안보임(DOM에 없음)을 표현하기 위해 console에 주석(\<!---->)이 표시된다
        - 브라우저가 파싱할 때 위에서 아래로 내려오며 해석함. 그래서 위 코드의 경우 처음에 다 보이고, 브라우저가 script까지 본 이후에야 원하는 대로 표시된다.

      - v-show와 v-if 비교

        - v-show(Expensive initial load, cheap toggle)
          - CSS display 속성을 hidden으로 만들어 토글
          - 실제로 <u>렌더링은 되지만 눈에서 보이지 않는 것</u>이기 때문에 딱 한 번만 렌더링이 되는 경우라면 v-if에 비해 상대적으로 렌더링 비용이 높음
          - 하지만, **자주 변경되는 요소**라면 한 번 렌더링 된 이후부터는 보여주는지에 대한 여부만 판단하면 되기 때문에 토글 비용이 적음
        - v-if(cheap initial load, expensive  toggle)
          - 전달인자가 false인 경우 <u>렌더링 되지 않음</u>
          - 화면에서 보이지 않을 뿐만 아니라 렌더링 자체가 되지 않기 때문에 렌더링 비용이 낮음
          - 하지만, 자주 변경되는 요소의 경우 다시 렌더링 해야하므로 비용이 증가할 수 있음

      - v-for

        ```html
        <div id="app">
          <h2>String</h2>
          <div v-for="char in myStr">
            {{ char }}
          </div>
          <h2>Array</h2>
          <div v-for="fruit in fruits">
            {{ fruit }}
          </div>
          <div v-for="(fruit, idx) in fruits" :key="idx">
            {{ idx }} => {{ fruit }} 
          </div>
          <!--key에 bind 안걸어주고 key="idx"라고 하면 Duplicated keys detected 오류 발생-->	
            
          <div v-for="todo in todos" :key="`todo-${todo.id}`">
            <p>{{ todo.title }} => {{ todo.completed }}</p>
          </div>
        
          <h2>Object</h2>
          <div v-for="value in myObj">
            {{ value }}
          </div>
          <div v-for="(value, key) in myObj">
            {{ key }} => {{ value }}
          </div>
        </div>
        
        <script>
          const app = new Vue({
            el: '#app',
            data: {
              myStr: 'Hello World!',
              fruits: ['apple', 'banana', 'coconut'],
              todos: [
                { id: 1, title: 'todo1', completed: true },
                { id: 2, title: 'todo2', completed: false },
                { id: 3, title: 'todo3', completed: true },
              ],
              myObj: {
                name: 'kim',
                age: 100,
              }
            }
          }) 
        </script>
        ```

        - 원본 데이터를 기반으로 엘리먼트 또는 템플릿 블록을 여러 번 렌더링
        - **item in items** 구문 사용
        - item 위치의 변수를 각 요소에서 사용할 수 있음
          - 객체의 경우는 key
        - v-for 사용 시 반드시 <u>**key 속성**을 각 요소에 작성</u>
        - v-if와 함께 사용하는 경우 v-for가 우선순위가 더 높음
          - <u>단, 가능하면 v-if와 v-for를 동시에 사용하지 말 것</u>

      - v-on

        ```html
        <div id="app">
            <!-- 메서드 핸들러 -->
            <button v-on:click="alertHello">Button</button>
            <button @click="alertHello">Button</button>
            <!-- 기본 동작 방지 -->
            <form action="" @submit.prevent="alertHello">
              <button>GoGo</button>
            </form>
        
            <!-- 키 별칭을 이용한 키 입력 수식어 -->
            <input type="text" @keyup.enter="log"> <!--첫번째 인자가 event-->
            <!-- cb 함수에서 특수문법 () -->
            <input type="text" @keyup.enter="log('s')"> <!--첫번째 인자로 's' 넘김-->
            
            <p>{{ message }}</p>
            <button @click="changeMessage">change message</button>
          </div>
          
          <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
          <script>
            const app = new Vue({
              el: '#app',
              // 값
              data: {
                message: 'Hello Vue',
              },
              // 행동(함수)
              methods: {
                alertHello: function () {
                  alert('hello')
                },
                log: function (something) {
                  console.log(something)
                },
                changeMessage() {
                  this.message = 'New message!!!'
                },
              }
        
            })
          </script>
        ```

        - 엘리먼트에 이벤트 리스너를 연결
        - 이벤트 유형은 전달인자로 표시함
        - 특정 이벤트가 발생했을 때, 주어진 코드가 실행됨
        - 약어(Shorthand)
          - **@**
            - v-on: click -> @click

      - v-bind

        ```html
        <head>
          <style>
            .active {
              color: red;
            }
        
            .my-background-color {
              background-color: yellow;
            }
          </style>
        </head>
        <body>
          <div id="app">
            <!-- 속성 바인딩 -->
            <img v-bind:src="imageSrc" :alt="altMsg">	<!--실제 data의 텍스트와 연결-->
            <img :src="imageSrc" alt="altMsg">
            <hr>	<!-- v-bind: === : -->
        
            <!-- 클래스 바인딩 -->
            <div :class="{ active: isRed }"> <!--{ active: if isRed } 느낌. 종속되어 있음-->
              클래스 바인딩
            </div>
        
            <h3 :class="[activeRed, myBackground]">	<!--key값으로 bind-->
              hello vue
            </h3>
            <hr>
        
            <!-- 스타일 바인딩 -->
            <p :style="{ fontSize: fontSize + 'px' }">
              this is paragraph
            </p>
          </div>
          
          <script>
            const app = new Vue({
              el: '#app',
              data: {
                fontSize: 16,
                altMsg: 'this is image',
                imageSrc: 'https://picsum.photos/200/300/',
                isRed: true,
                activeRed: 'active',
                myBackground: 'my-background-color',
              }
            })
            const myName = 'asdf'
          </script>
        </body>
        ```

        - <u>HTML 요소의 속성에 Vue의 상태 데이터를 값으로 할당</u>
        - Object 형태로 사용하면 value가 true인 key가 class 바인딩 값으로 할당
        - 약어(Shorthand)
          - **:**(콜론)
            - v-bind: href -> :href

      - v-model

        ```html
        <body>
          <div id="app">
            <h2>Input -> Data 단방향</h2>
            <p>{{ msg1 }}</p>
            <input type="text" @input="onInputChange">	<!--input tag에 변화가 있으면 동작-->
            <hr>
            <h2>Input <-> Data 양방향</h2>
            <p>{{ msg2 }}</p>
            <input type="text" v-model="msg2">
            <hr>
            check! <input id="box" type="checkbox" v-model="checked">
            <label for="box">{{ checked }}</label>
          </div>
        
          <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
          <script>
            const app = new Vue({
              el: '#app',
              data: {
                msg1: '111',
                msg2: '222',
                checked: true,
              },
              methods: {
                onInputChange (event) {
                  this.msg1 = event.target.value
                }
              },
            })
          </script>
        </body>
        ```

        - HTML form 요소(<u>input</u>)의 값과 <u>data</u>를 **양방향 바인딩**
        - 수식어
          - .lazy
            - input 대신 change 이벤트 이후에 동기화
          - .number
            - 문자열을 숫자로 변경
          - .trim
            - 입력에 대한 trim을 진행

- Options/Data - 'computed'

  ```html
  <body>
    <div id="app">
      <input v-model="r" type="text">
      <p>{{ r }}</p>
      <p>{{ area }}</p>
      <p>{{ perim }}</p>
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      const app = new Vue({
        el: '#app',
        data: {
          r: 2,
        },
        computed: {	//data에 의존하는 계산된 값
          area: function () {
            return this.r ** 2 * 3.14
          },
          perim: function () {
            return this.r * 2 * 3.14
          }
        }
      })
    </script>
  </body>
  ```

  - 데이터를 기반으로 하는 계산된 속성
  - 함수의 형태로 정의하지만 함수가 아닌 <u>함수의 반환 **값**이 바인딩</u> 됨
  - 종속된 데이터에 따라 저장(캐싱)됨
  - **종속된 데이터가 변경될 때만 함수를 실행**
  - 즉, 어떤 데이터에도 의존하지 않는 computed 속성의 경우 <u>절대로 업데이트되지 않음</u>
  - 반드시 **반환 값**이 있어야 함

- computed & methods

  - computed 속성 대신 methods에 함수를 정의할 수도 있음
    - 최종 결과에 대해 두 가지 접근 방식은 서로 동일
  - 차이점은 computed 속성은 종속 대상을 따라 저장(캐싱)됨
  - 즉, computed는 종속된 대상이 변경되지 않는 한 computed에 작성된 함수를 여러 번 호출해도 계산을 다시 하지 않고 <u>계산되어 있던 결과를 반환</u>. data를 통한 값을 **얻음**.(setter 함수들)
  - 이에 비해 methods를 호출하면 렌더링을 다시 할 때마다 항상 함수를 실행. 주로 data를 **바꾸**는 로직(getter 함수들).

- Options/Data - 'watch'

  ```html
  <body>
    <div id="app">
      <p>{{ num }}</p>
      <button @click="num += 1">add 1</button>
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      const app = new Vue({
        el: '#app',
        data: {
          num: 2,
        },
        watch: {
          num: function () {
            console.log(`${this.num}이 변경되었습니다.`)
          }
        },
      })
    </script>
  </body>
  ```

  - 데이터를 감시
  - 데이터에 변화가 일어났을 때 실행되는 함수

- computed & watch

  - computed

    > 특정 값이 변동하면 해당 값을 다시 계산해서 보여준다(<u>능동적</u>)
    >
    > 주로 사용됨

    - 특정 데이터를 <u>직접적으로 사용/가공하여</u> 다른 값으로 만들 때 사용
    - 속성은 계산해야 하는 목표 데이터를 정의하는 방식으로 소프트웨어 공학에서 이야기하는 '**선언형** 프로그래밍' 방식

  - watch

    > 특정 값이 변동하면 다른 작업을 한다.

    - 특정 데이터의 변화 상황에 맞춰 다른 data 등이 바뀌어야 할 때 주로 사용
    - <u>감시할 데이터를 지정</u>하고 그 데이터가 바뀌면 특정 함수를 실행하는 방식
    - 안에 들어있는 함수의 계산된 결과를 변수처럼 쓴다. <u>각각 직접</u> 정의.
    - 소프트웨어 공학에서 이야기하는 '**명령형** 프로그래밍' 방식
    - 특정 대상이 변경되었을 때 콜백 함수를 실행시키기 위한 트리거

  - computed와 watch는 어떤 것이 더 우수한 것이 아닌 사용하는 목적과 상황이 다름

- 선언형 & 명령형

  - 선언형 프로그래밍: 계산해야 하는 목표 데이터를 정의(computed)
  - 명령형 프로그래밍: 데이터가 바뀌면 특정 함수를 실행해(watch)

- Options/Assets - 'filter'

  ```html
  <body>
    <div id="app">
      {{ numbers | getOddNumbers | getUnderTen }}
      {{ getOddAndUnderTen }}
    </div>
  
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      const app = new Vue({
        el: '#app',
        data: {
          numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
        },
        filters: {
          getOddNumbers(array) {
            return array.filter(num => num % 2)
          },
          getUnderTen(array) {
            return array.filter(num => num < 10)
          }
        },
        // w/ computed
        computed: {
          getOddAndUnderTen() {
            return this.numbers.filter(num => num % 2 && num < 10)
          }
        }
      })
    </script>
  </body>
  ```

  - **텍스트 형식화**를 적용할 수 있는 필터
  - interpolation 혹은 v-bind를 이용할 때 사용 가능
  - 필터는 자파스크립트 표현식 마지막에 '|'(파이프)와 함께 추가되어야 함
  - 이어서 사용(chaining) 가능

### Lifecycle Hooks

- What is Lifecycle Hooks?
  - 각 Vue 인스턴스는 생성될 때 일련의 초기화 단계를 거침
    - 예를 들어 데이터 관찰 설정이 필요한 경우, 인스턴스를 DOM에 마운트하는 경우, 데이터가 변경되어 DOM을 업데이트하는 경우 등
  - 그 과정에서 사용자 정의 로직을 실행할 수 있는 Lifecycle Hooks도 호출됨
  - 공식문서를 통해 각 라이프사이클 훅의 상세 동작을 참고
  
- 예시

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <body>
    <div id="app">
      <img v-if="imgSrc" :src="imgSrc" alt="sample img">	<!-- imgSrc에 값이 들어올 때 보인다 -->
      <button @click="getImg">GetDog</button>
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      const API_URL = 'https://dog.ceo/api/breeds/image/random'
      const app = new Vue({
        el: '#app',
        data: {
          imgSrc: '',
        },
        methods: {
          getImg: function () {
            axios.get(API_URL)
              .then(response => {	//성공했을 때
                this.imgSrc = response.data.message	//data 변경
              })
          }
        },
        created: function () {	//view instance가 생성될 때 실행
          this.getImg()			// 외부 API에서 초기 데이터 받아오기
        }
      })
    </script>
  </body>
  </html>
  ```

  - 예를 들어 created hook은 vue 인스턴스가 생성된 후에 호출됨
  - created를 사용해 애플리케이션의 초기데이터를 API 요청을 통해 불러올 수 있음



## SFC(Single File Component)

- Component 

  - 기본 HTML 엘리먼트를 확장하여 재사용 가능한 코드를 캡슐화하는데 도움을 줌(부품)
  - CS에서는 다시 사용할 수 있는 범용성을 위해 개발된 소프트웨어 구성 요소를 의미
  - 즉, 컴포넌트는 유지보수를 쉽게 만들어 줄 뿐만 아니라, <u>재사용성</u>의 측면에서도 매우 강력한 기능을 제공

  **Vue 컴포넌트 === Vue 인스턴스**

- SFC: Single File Component

  - Vue의 컴포넌트 기반 개발의 핵심 특징
  - 하나의 컴포넌트는 .vue 확장자를 가진 하나의 파일 안에서 작성되는 코드의 결과물
  - 화면의 특정 영역에 대한 <u>HTMl, CSS, JavaScript 코드를 하나의 파일(.vue)에서 관리</u>
  - 즉, .vue 확장자를 가진 싱글 파일 컴포넌트를 통해 개발하는 방식

  **Vue 컴포넌트 === Vue 인스턴스 === .vue 파일**

- Component 예시

  - 단일 파일 관리
    - 단일 파일에서의 개발
      - 처음 개발을 시작할 때는 크게 신경쓸 것이 없기 때문에 쉽게 개발 가능
      - 하지만 코드의 양이 많아지면 변수 관리가 힘들어지고 유지보수에 많은 비용 발생
  - 한 화면을 구성하는 여러 컴포넌트
    - 각 기능 별로 파일을 나눠서 개발
      - 처음 개발을 준비하는 단계에서 시간 소요가 증가
      - 하지만 이후 변수 관리가 용이하며 기능 별로 유지 & 보수 비용 감소

- Vue Component 구조 예시

  - 한 화면 안에서도 기능 별로 각기 다른 컴포넌트가 존재
    - 하나의 컴포넌트는 여러 개의 하위 컴포넌트를 가질 수 있음
    - Vue는 컴포넌트 기반의 개발 환경 제공
  - Vue 컴포넌트는 **const app = new Vue({...})**의 app을 의미하며 이는 Vue 인스턴스
    - 여기서 오해하면 안되는 것은 컴포넌트 기반의 개발이 **반드시 파일 단위로 구분되어야 하는 것은 아님**
    - 단일 .html 파일 안에서도 여러 개의 컴포넌트를 만들어 개발 가능

- [정리]

  - Vue 컴포넌트는 Vue 인스턴스(new Vue({}))이기도 함
  - Vue 인스턴스는 .vue 파일 안에 작성된 코드의 집합
  - HTML, CSS, 그리고 JavaScript를 .vue라는 확장자를 가진 파일 안에서 관리하며 개발



## Vue CLI

- Vue CLI

  - Vue.js 개발을 위한 표준 도구
  - 프로젝트의 구성을 도와주는 역할을 하며 Vue 개발 생태계에서 표준 tool 기준을 목표로 함
  - 확장 플러그인, GUI, Babel 등 다양한 tool 제공

- Node.js

  - 자바스크립트를 브라우저가 아닌 환경에서도 구동할 수 있도록 하는 자바스크립트 런타임 <u>환경</u>
    - 브라우저 밖을 벗어날 수 없던 자바스크립트 언어의 태생적 한계를 해결
  - Chrome VS 엔진을 제공하여 여러 OS 환경에서 실행할 수 이쓴 환경을 제공
  - 즉, 단순히 브라우저만 조작할 수 있던 자바스크립트를 SSR 아키텍처에서도 사용할 수 있도록 함
  - [참고] 2009년 Ryan Dahl에 의해 발표

- NPM(Node Package Manage)

  - 자바스크립트 언어를 위한 패키지 관리자
    - Python에 pip가 있다면 <u>Node.js에는 NPM</u>
    - pip와 마찬가지로 다양한 의존성 패키지를 관리
  - Node.js의 기본 패키지 관리자
  - Node.js 설치 시 함께 설치됨

- Vue CLI Quick Start

  ```bash
  $ npm install -g @vue/cli	#1. 설치(global)
  $ vue --version				#2. 버전 확인
  
  #vscode terminal로 진행 - 대화형으로 진행 시 편리함
  $ vue create my-first-app	#3. 프로젝트 생성
  #3-1. npm 레지스트리 변경(환경에 따라 나오지 않을 수 있음)
  
  #4. Vue 버전 선택 (Vue2)
  #5. 프로젝트 생성 성공
  $ cd my-first-app/	#6. 프로젝트 디렉토리 이동
  $ npm run serve 	#7. 서버 실행	(ctrl+c로 서버 종료)
  ```



### Babel & Webpack

- Babel: JavaScript <u>compiler</u>
  - 자바스크립트의 ECMAScript 2015+ 코드를 <u>이전 버전으로 번역/변환</u>해주는 도구
  - 과거 자바스크립트의 파편화와 표준화의 영향으로 코드의 스펙트럼이 매우 다양
    - 이때문에 최신 문법을 사용해도 이전 브라라우저 혹은 환경에서 동작하지 않는 상황이 발생
  - 원시 코드(최신 버전)을 목적 코드(구 버전)로 옮기는 번역가가 등장하면서 개발자는 더 이상 내 코드가 특정 브라우저에서 동작하지 않는 상황에 대해 크게 고민하지 않을 수 있게 됨
- Webpack: static module bundler
  - 모듈 간의 <u>의존성 문제를 해결</u>하기 위한 도구
  - 프로젝트에 필요한 모든 모듈을 매핑하고 내부적으로 종속성 그래프를 빌드함
- Static **Module** Bundler
  - 모듈은 단지 파일 하나를 의미 (ex. js 파일 하나 === 모듈 하나)
  - 배경
    - 브라우저만 조작할 수 있었던 시기의 자바스크립트는 모듈 관련 문법이 없이 사용됨
    - 하지만 JS와 애플리케이션이 복잡해지고 크기가 커지자 전역 scope를 공유하는 형태의 기존 개발 방식의 한계점이 드러남
    - 그래서 **라이브러리**를 만들어 필요한 모듈을 언제든지 불러오거나 코드를 **모듈 단위**로 작성하는 등의 다양한  시도가 이루어짐
  - 에러 모듈 시스템 
    - ESM(ECMA Script Module)_사실상 표준
    - AMD(Asynchronous Module Definition)
    - CommonJS
    - UMD(Universal Module Definition)
  - 모듈 의존성 문제
    - 모듈의 수가 많아지고 라이브러리 혹은 모듈 간의 **의존성(연결성)이 깊어지면서** 특정한 곳에서 발생한 문제가 <u>어떤 모듈 간의 문제인지 파악하기 어려움</u>
    - 즉, <u>Webpack</u>은 이 모듈 간의 <u>의존성 문제를 해결</u>하기 위해 등장
- Static Module **Bundler**
  - **<u>모듈 의존성 문제를 해결</u>**해주는 작업을 **Bundling**이라 함
  - 이러한 일을 해주는 도구가 Bundler이고, <u>Webpack은 다양한 Bundler 중 하나</u>
  - <u>여러 모듈을 하나로 묶어주고 묶인 파일은 하나(혹은 여러 개)로 합쳐짐</u>
  - Bundling된 결과물은 더 이상 순서에 영향을 받지 않고 동작하게 됨
  - snowpack, parcel, rollup.js 등의 webpack 이외에도 다양한 모듈 번들러 존재
  - **Vue CLI는 이러한 Babel, Webpack에 대한 초기 설정이 자동으로 되어 있음**
- Vue 프로젝트 구조
  - node_modules
    - node.js 환경의 여러 의존성 모듈. (용량이 크다)
    - django의 venv. 
  - public/index.html
    - Vue 앱의 뼈대가 되는 파일
    - 실제 제공되는 단일 html 파일
  - src/  (작업공간)
    - assets/
      - webpack에 의해 빌드된 정적 파일
    - components/
      - 하위 컴포넌트들이 위치
    - App.vue
      - 최상위(루트) 컴포넌트. 캔버스
    - main.js
      - webpack이 빌드를 시작할 때 가장 먼저 불러오는 entry point
      - 실제 단일 파일에서 DOM과 data를 <u>연결</u>했던 것과 동일한 작업이 이루어지는 곳
      - Vue 전역에서 활용할 모듈을 등록할 수 있는 파일
  - babel.config.js
    - babel 관련 설정이 작성된 파일
  - package.json
    - 프로젝트의 종속성 목록과 지원되는 브라우저에 대한 구성 옵션이 포함 (알아서 써준다)
    - django의 requirements.txt
  - package-lock.json
    - node_modules에 설치되는 모듈과 관련된 모든 의존성을 설정 및 관리
    - 팀원 및 배포 환경에서 정확히 동일한 종속성을 설치하도록 보장하는 표현
    - 사용할 패키지의 버전을 고정
    - 개발 과정 간의 의존성 패키지 충돌 방지



## Pass props & Emit event

- 컴포넌트 작성
  - Vue app은 자연스럽게 중첩된 컴포넌트 트리로 구성됨
  - 컴포넌트 간 부모-자식 관계가 구성되며 이들 사이에 필연적으로 의사 소통이 필요함
  - 부모는 자식에게 데이터를 전달(pass props)하며, 자식은 자신에게 일어난 일을 부모에게 알림(emit event)
    - 부모와 자식이 명확하게 정의된 인터페이스를 통해 격리된 상태를 유지할 수 있음
  - **props는 아래로, event는 위로**
  - 부모는 props를 통해 자식에게 데이터를 전달하고, 자식은 events를 통해 부모에게 메세지를 보냄
- 컴포넌트 구조
  1. 템플릿(HTML)
     - HTML의 body 부분
     - 각 컴포넌트를 작성
  2. 스크립트(JavaScript)
     - JavaScript가 작성되는 곳
     - 컴포넌트 정보, 데이터, 메서드 등 vue 인스턴스를 구성하는 대부분이 작성 됨
  3. 스타일(CSS)
     - CSS가 작성되며 컴포넌트의 스타일을 담당
- 컴포넌트 등록 3단계
  1. 불러오기(import)
  2. 등록하기(register)
  3. 보여주기(print)

### Props

- props는 부모(상위) 컴포넌트의 정보를 전달하기 위한 사용자 지정 특성
- 자식(하위) 컴포넌트는 props 옵션을 사용하여 수신하는 props를 명시적으로 선언해야 함
- 즉, 데이터는 props 옵션을 사용하여 자식 컴포넌트로 전달됨
- **[주의]**
  - 모든 컴포넌트 인스턴스에는 자체 격리된 범위가 있음
  - 즉, 자식 컴포넌트의 템플릿에서 상위 데이터를 직접 참조할 수 없음

- Static Props 작성
  - 자식 컴포넌트(About.vue)에서 보낼 prop 데이터 선언
  - 작성법: prop-data-name="value"
  - 수신할 prop 데이터를 명시적으로 선언 후 사용

- Dynamic Props 작성
  - v-bind directive를 사용해 부모의 데이터의 props를 동적으로 바인딩
  - 부모에서 데이터가 업데이트될 때마다 자식 데이터로도 전달됨
  - 마찬가지로 수신할 prop 데이터를 명시적으로 선언 후 사용
- Props 이름 컨벤션
  - during declaration(선언 시): camelCase
  - in template(HTML): kebab-case
- **컴포넌트의 data는 반드시 함수여야 함**
  - 기본적으로 각 인스턴스는 모두 같은 data 객체를 공유하므로 새로운 data 객체를 반환(return)하여야 함
- Props 시 자주하는 실수
  - Static 구문을 사용하여 숫자를 전달하려고 시도하는 것
  - 실제 JavaScript 숫자를 전달하려면 값이 JavaScript 표현식으로 평가되도록 v-bind를 사용해야함
- 단방향 데이터 흐름
  - 모든 props는 하위 속성과 상위 속성 사이의 **단방향** 바인딩을 형성
  - 부모의 속성이 변경되면 자식 속성에게 전달되지만, 반대 방향으로는 안됨
    - 자식 요소가 의도치 않게 부모 요소의 상태를 변경하여 앱의 데이터 흐름을 이해하기 어렵게 만드는 일을 방지
  - 부모 컴포넌트가 업데이트될 때마다 자식 요소의 모든 prop들이 최신 값으로 업데이트됨

### Emit event

> Listening to Child Components Events

- $emit(eventName)
  - 현재 인스턴스에서 이벤트를 트리거
  - 추가 인자는 리스너의 콜백 함수로 전달
- 부모 컴포넌트는 자식 컴포넌트가 사용되는 템플릿에서 v-on을 사용하여 자식 컴포넌트가 보낸 이벤트를 청취(v-on을 이용한 사용자 지정 이벤트)
- Emit event 작성
  - 현재 인스턴스에서 $emit 인스턴스 메서드를 사용해 child-input-change 이벤트를 트리거
  - 부모 컴포넌트(App.vue)는 자식 컴포넌트(About.vue)가 사용되는 템플릿에서 v-on directive를 사용하여 자식 컴포넌트가 보낸 이벤트(child-input-change)를 청취
- event 이름 컨벤션
  - 컴포넌트 및 props와는 달리, 이벤트는 자동 대소문자 변환을 제공하지 않음
  - HTML의 대소문자 구분을 위해 DOM 템플릿의 v-on 이벤트 리스너는 항상 자동으로 소문자 변환되기 때문에 v-on:myEvent는 자동으로 v-on:myevent로 변환
  - 이러한 이유로 이름에는 **항상 kebab-case를 사용하는 것을 권장**



## Vue Router

- What is Vue Router?

  - "Vue.js 공식 라우터"
- 라우트(route)에 <u>컴포넌트를 매핑</u>한 후, <u>어떤 주소에서 렌더링할 지</u> 알려줌
    - URL을 통한 하이퍼링크 이동하지 않는다. 마치 URL로 인해 화면이 바뀐 것처럼 행동
- SPA 상에서 라우팅을 쉽게 개발할 수 있는 기능을 제공
  - [참고] router
- 위치에 대한 최적의 경로를 지정하며, 이 경로를 따라 데이터를 다음 장치로 전향시키는 장치
  
- Vue Router 시작하기

  ```bash
  $ vue create my-router-app #1. 프로젝트 생성 및 이동(앱 안에서 앱 만들지 않기)
  $ vue add router	#2. Vue Router plugin설치(Vue CLI 환경)
  '''[주의]기존 프로젝트를 진행하고 있던 도중에 추가하게 되면 App Vue를 덮어쓰므로, 프로젝트 내에서 다음 명령을 실행하기 전에 필요한 경우 파일을 백업(커밋)해야 함'''
  #3. commit 여부 -> Yes
  #4. History mode 사용 여부 -> Yes
  ```

- Vue Router로 인한 변화

  - App.vue 코드 (router 관련 코드 자동으로 작성해줌)
  - router/index.js 생성
  - views 디렉토리 생성

- Vue Router 요소

  - index.js
    
    - 라우트에 관련된 정보 및 설정이 작성되는 곳
      - url 패턴, 별칭, 렌더링할 컴포넌트. 
      - django의 urlpatterns와 비슷하다
    
  - App.vue의 \<router-link>

    ```vue
    <router-link to="/">Home</router-link>
    <router-link :to="{ name: 'home' }">Home</router-link>
    ```

    - 사용자 네비게이션을 가능하게 하는 <u>컴포넌트</u>
    - 목표 경로는 'to' prop으로 지정됨
    - HTML5 히스토리 모드에서 router-link는 클릭 이벤트를 차단하여 브라우저가 페이지를 <u>다시 로드하지 않도록 함</u>
    - a 태그지만 우리가 알고 있는 GET 요청을 보내는 a 태그와 조금 다르게, 기본 GET 요청을 보내는 <u>이벤트를 제거한 형태</u>로 구성됨

  - App.vue의 \<router-view>
    
    - 주어진 라우트에 대해 <u>일치하는 컴포넌트를 렌더링</u>하는 컴포넌트
    - 실제 component가 DOM에 부착되어 보이는 자리를 의미
    - router-link를 클릭하면 해당 경로와 연결되어 있는 index.js에 정의한 컴포넌트가 위치

- History mode

  - HTML History API를 사용해서 router를 구현한 것
  - <u>브라우저의 히스토리는 남기지만 실제 페이지는 이동하지 않는 기능을 지원</u>
  - 즉, 페이지를 다시 로드하지 않고 URL을 탐색할 수 있음
    - SPA의 단점 중 하나인 "URL이 변경되지 않는다"를 해결
  - [참고] History API
    - DOM의 Window 객체는 history 객체를 통해 브라우저의 세션 기록에 접근할 수 있는 방법을 제공
    - history 객체는 사용자를 자신의 방문 기록 앞과 뒤로 보내거나, 기록의 특정 지점으로 이동하는 등 유용한 메서드와 속성을 가짐

- Vue Router

  1. Named Routes
     - 이름을 가지는 라우트
     - 명명된 경로로 이동하려면 객체를 vue-router 컴포넌트 요소의 prop에 전달
  2. 프로그래밍 방식 네비게이션
     - \<router-link>를 사용하여 선언적 탐색을 위한 a 태그를 만드는 것 외에도, router의 인스턴스 메서드를 사용하여 프로그래밍 방식으로 같은 작업을 수행할 수 있음
       - 선언적 방식: \<router-link to="...">
       - 프로그래밍 방식: $router.push(...)
       
     - Vue 인스턴스 내부에서 라우터 인스턴스에 <u>$router</u>로 접근할 수 있음

     - 따라서 다른 URL로 이동하려면 <u>this.**$router**.push</u>를 호출할 수 있음
       
       - 이 메서드는 새로운 항목을 히스토리 스택에 넣기 때문에 사용자가 브라우저의 뒤로 가기 버튼을 클릭하면 이전 URL로 이동하게 됨
       
     - \<router-link>를 클릭할 때 내부적으로 호출되는 메서드이므로 \<router-link :to="...">를 클릭하면, <u>router.push(...)</u>를 호출하는 것과 같음

     - 작성할 수 있는 인자 예시

       ```vue
       <script>
       	router.push('home')	//literal string path. url에 string(home)을 붙임
           router.push({path:'home'})	//object
           router.push({name:'user', params: {userId:'123'}})	//named route
           router.push({path:'register', query:{plan:'private'}})	
           //with query, resulting in /reguster?plan=private
       </script>
       ```
  3. Dynamic Route Matching
     - 동적 인자 전달

     - 주어진 패턴을 가진 라우트를 동일한 컴보넌트에 매핑해야 하는 경우

     - 예를 들어 모든 User에 대해 동일한 레이아웃을 가지지만, 다른 User ID로 렌더링 되어야 하는 User 컴포넌트 예시

       ```vue
       <!--UserProfile.vue-->
       <template>
       	<p>
               당신의 id는 {{user.userId}}
           </p>
       </template>
       <script>
       export default {
           name:'UserProfile',
           data: function () {
               return {
                   user: this.$route.params,
               }
           }
       }
       </script>
       
       <!--router/index.js-->
       <script>
       	const routes = [
               {
                   path: '/user/:userId',
                   name: 'User',
                   component: User
               }
           ]
       </script>
       ```

     - 동적 인자는 :(콜론)으로 시작

     - 컴포넌트에서 this.$route.params로 사용가능

       | pattern                            | matched path       | $route.params                 |
       | ---------------------------------- | ------------------ | ----------------------------- |
       | /user/:userName                    | /user/jo           | {username: 'jo'}              |
       | /user/:userName/article/:articleId | /user/jo/article/2 | {username:'jo', articleId: 2} |

- components와 views

  - 기본적으로 작성된 구조에서 components 폴더와  views 폴더 내부에 각기 다른 컴포넌트가 존재하게 됨
  - 컴포넌트를 작성해 갈 때 정해진 구조가 있는 것은 아니며, 주로 아래와 같이 구조화하여 활용함
    - App.vue
      - 최상위 컴포넌트
    - views/
      - router(index.js)에 매핑되는 컴포넌트를 모아두는 폴더
      - ex) App 컴포넌트 내부에 AboutView & HomeView 컴포넌트 등록
    - components/
      - route에 매핑된 컴포넌트 내부에 작성하는 컴포넌트를 모아두는 폴더
      - ex) Home 컴포넌트 내부에 HelloWorld 컴포넌트 등록

- Vue Router가 필요한 이유

  1. SPA 등장 이전
     - 서버가 모든 라우팅을 통제
     - 요청 경로에 맞는 HTML를 제공
  2. SPA 등장 이후
     - 서버는 <u>index.html 하나</u>만 제공
     - 이후 모든 처리는 HTML 위에서 JS 코드를 활용해 진행
     - 즉, 요청에 대한 처리를 더 이상 <u>서버가 하지 않음</u>(할 필요가 없어짐)
  3. 라우팅 처리 차이
     - SSR
       - 라우팅에 대한 결정권을 서버가 가짐
     - CSR
       - 클라이언트는 더 이상 서버로 요청을 보내지 않고 응답받은 HTML 문서 안에서 주소가 변경되면 특정 주소에 맞는 컴포넌트를 렌더링
       - 라우팅에 대한 결정권을 클라이언트가 가짐
     - 결국 Vue Router는 라우팅의 결정권을 가진 Vue.js에서 라우팅을 편리하게 할 수 있는 Tool을 제공해주는 라이브러리