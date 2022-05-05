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
        - 단순히 엘리먼트에 display CSS 속성을 <u>토글</u>하는 것

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
        - item in items 구문 사용
        - item 위치의 변수를 각 요소에서 사용할 수 있음
          - 객체의 경우는 key
        - v-for 사용 시 반드시 <u>key 속성을 각 요소에 작성</u>
        - v-if와 함께 사용하는 경우 v-for가 우선순위가 더 높음
          - 단, 가능하면 v-if와 v-for를 동시에 사용하지 말 것

      - v-on

        - 엘리먼트에 이벤트 리스너를 연결
        - 이벤트 유형은 전달인자로 표시함
        - 특정 이벤트가 발생했을 때, 주어진 코드가 실행됨
        - 약어(Shorthand)
          - @
          - v-on: click -> @click

      - v-bind

        - HTML 요소의 속성에 Vue의 상태 데이터를 값으로 할당
        - Object 형태로 사용하면 value가 true인 key가 class 바인딩 값으로 할당
        - 약어(Shorthand)
          - :(콜론)
          - v-bind: href -> :href

      - v-model

        - HTML form 요소의 값과 data를 양방향 바인딩
        - 수식어
          - .lazy
            - input 대신 change 이벤트 이후에 동기화
          - .number
            - 문자열을 숫자로 변경
          - .trim
            - 입력에 대한 trim을 진행

- Options/Data - 'computed'

  - 데이터를 기반으로 하는 계산된 속성
  - 함수의 형태로 정의하지만 함수가 아닌 함수의 반환 값이 바인딩 됨
  - 종속된 데이터에 따라 저장(캐싱)됨
  - **종속된 데이터가 변경될 때만 함수를 실행**
  - 즉, 어떤 데이터에도 의존하지 않는 computed 속성의 경우 절대로 업데이트되지 않음
  - 반드시 반환 값이 있어야 함

- computed & methods

  - computed 속성 대신 methods에 함수를 정의할 수도 있음
    - 최종 결과에 대해 두 가지 접근 방식은 서로 동일
  - 차이점은 computed 속성은 종속 대상을 따라 저장(캐싱)됨
  - 즉, computed는 종속된 대상이 변경되지 않는 한 computed에 작성된 함수를 여러 번 호출해도 계산을 다시 하지 않고 계산되어 있던 결과를 반환
  - 이에 비해 methods를 호출하면 렌더링을 다시 할 때마다 항상 함수를 실행

- Options/Data - 'watch'

  - 데이터를 감시
  - 데이터에 변화가 일어났을 때 실행되는 함수

- computed & watch

  - computed

    > 특정 값이 변동하면 해당 값을 다시 계산해서 보여준다

    - 특정 데이터를 직접적으로 사용/가공하여 다른 값으로 만들 때 사용
    - 속성은 계산해야 하는 목표 데이터를 정의하는 방식으로 소프트웨어 공학에서 이야기하는 '선언형 프로그래밍' 방식

  - watch

    > 특정 값이 변동하면 다른 작업을 한다.

    - 특정 데이터의 변화 상황에 맞춰 다른 data 등이 바뀌어야 할 때 주로 사용
    - 감시할 데이터를 지정하고 그 데이터가 바뀌면 특정 함수를 실행하는 방식
    - 소프트웨어 공학에서 이야기하는 '명령형 프로그래밍' 방식
    - 특정 대상이 변경되었을 때 콜백 함수를 실행시키기 위한 트리거

  - computed와 watch는 어떤 것이 더 우수한 것이 아닌 사용하는 목적과 상황이 다름

- 선언형 & 명령형

  - 선언형 프로그래밍: 계산해야 하는 목표 데이터를 정의(computed)
  - 명령형 프로그래밍: 데이터가 바뀌면 특정 함수를 실행해(watch)

- Options/Assets - 'filter'

  - 텍스트 형식화를 적용할 수 있는 필터
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
  - 예를 들어 created hook은 vue 인스턴스가 생성된 후에 호출됨
  - created를 사용해 애플리케이션의 초기데이터를 API 요청을 통해 불러올 수 있음