# Django

> [Django](https://docs.djangoproject.com/ko/4.0/intro/): Python Web framework

## Web Framework

- Web: World Wide Web의 약자. 인터넷에 연결된 컴퓨터를 통해 정보를 공유할 수 있는 전 세계적인 정보 공간. 인터넷 공간
  - Static  web page(정적 웹 페이지)  (=Flat page)
    - 서버에 미리 저장된 파일이 사용장게 그대로 전달되는 웹 페이지. 
    - 요청 받은 경우 서버는 **추가적인 처리 과정 없이** 클라이언트에게 응답을 보냄 => **모든 사용자에게 같은 결과를 보냄**
      - 클라이언트는 네트워크를 통해 data를 얻기 위해 서버라는 원격 서버에 접속할 수 있다.
        - 클라이언트의 종류: 데스크탑, 스마트폰, **웹 브라우저**(크롬)
        - 서버 구축하는 Framework: Django
        - 클라이언트가 서버에 요청했을 때, URL요청이 왔을 때(urls.py), 작업을 해서(views.py), HTML 응답(Template)
      - 클라이언트  --요청(URL)-->  서버
      - 서버  --응답(문서-JSON, HTML...-)-->  클라이언트
    - <u>HTML, CSS, JavaScript</u>로 작성된다.
  - Dynamic web page
    - 웹 페이지에 대한 요청을 받은 경우 서버는 **추가적인 처리 과정** 이후 클라이언트에게 응답을 보냄
    - 동적 웹 페이지는 **방문자와 상호작용**하기 때문에 **페이지 내용은 그때그때 다름**
    - 서버 사이드 프로그래밍 언어(<u>Python, Java, C++ 등</u>)이 사용됨. 파일을 처리하고 데이터베이스와의 상호작용(저장, 수정, 삭제, 조회)이 이루어짐
  - 웹의 동작 원리
    1. 사용자가 브라우저에 웹 주소를 입력하면 브라우저는 DNS 서버로 가서 웹사이트가 있는 서버의 진짜 주소를 찾는다.
       - dns 서버: 웹 사이트를 위한 주소록. 브라우저에 입력하는 웹주소(ex. mozilla.org) 를 웹사이트의 실제 주소(IP. ex. 63.245.217.105)에 맞춰주는 특별한 서버
    2.  브라우저는 서버에게 웹사이트의 사본을 클라이언트에게 보내달라는 HTTP 요청 메세지를 서버로 전송. 
       - 메세지, 그리고 클라이언트와 서버 사이에 전송된 모든 데이터는 TCP/IP 연결을 통해서 전송됨.
         - TCP/IP: 전송 제어 규약과 인터넷 규약. 인터넷으로 통신하는 데 있어 가장 기반이 되는프로토콜
    3. 이 메세지를 받은 서버는 올바른 요청이면 승인하고, "200 OK"(코드의 동작 결과) 메세지를 클라이언트에게 전송. 
    4. 서버는 웹사이트의 파일들을 데이터 패킷이라 불리는 작은 일련의 덩어리들로 브라우저에 전송하기 시작
    5. 브라우저는 이 작은 덩어리들을 완전한 웹 사이트로 조립하고, 화면에 표시한다

- Frame work (= Applicatiion framework)
  - 프로그래밍에서 특정 운영 체제를 위한 응용 프로그램 표준 구조를 구현하는 **클래스와 라이브러리 모임**
  - <u>재사용할 수 있는 수많은 코드</u>를 프레임워크로 통합함으로써 개발자가 새로운 애플리케이션을 위한 표준 코드를 다시 작성하지 않아도 같이 사용할 수 있도록 도움

- Web framework

  - 웹 페이지를 개발하는 과정에서 겪는 어려움을 줄이는 것이 주 목적
    - 데이터베이스 연동, 템플릿 형태의 표준, 세션 관리, 코드 재사용 등의 기능을 포함
  - 동적인 웹 페이지나, 웹 애플리케이션, 웹 서비스 개발 보조용으로 만들어지는 Application framework의 일종

- Django 사용해야 하는 이유

  - 검증된 파이썬 기반 Web famework.
  - 대규모 서비스에도 안정적. 오랫동안 세계적인 기업들에 의해 사용됨.
    - Instagram, Spotify, dropbox 등

- Framework Architecture

  - MVC(Model-View-controller) Design Pattern
    - 소프트웨어 공학에서 사용되는 디자인 패턴 중 하나
      - 디자인패턴: 객체 지향 프로그래밍 설계를 할 때 자주 발생하는 문제들을 피하기 위해 사용되는 패턴. 의사소통 수단의 일종
    - 사용자 인터페이스로부터 프로그램 로직을 분리하여 애플리케이션의 시각적 요소나 이면에서 실행되는 부분을 서로 영향 없이 쉽게 고칠 수 있는 애플리케이션을 만들 수 있음
    - Django에서는 MTV(Model-Template-View) Pattern이라고 함

- MTV Pattern

  - Model
    - 응용프로그램의 데이터 구조를 정의하고 데이터베이스의 기록을 관리(**추가, 수정, 삭제)**
  - Template
    - 파일의 구조나 레이아웃을 정의
    - 실제 내용을 보여주는 데 사용(<u>presentation</u>)
  - **View**
    - HTTP 요청을 **수신**하고 HTTP 응답을 **반환**. Control tower의 역할.
    - <u>Model</u>을 통해 요청을 충족시키는데 필요한 데이터에 접근
    - <u>template</u>에게 응답의 서식 설정을 맡김

  ![image-20220302092539990](Django.assets/image-20220302092539990.png)



## Django Intro

- 가상환경 생성(python -m venv 가상환경이름) 및  활성화(source 가상환경이름/Scripts/activate) 
  -> django 설치(pip install django==3.2.12) 
  -> 프로젝트 생성(django-admin startproject 프로젝트명 .) 
  -> 서버 켜서(python manage.py runsever) 로켓 확인하기  
  -> (ctrl+c로 서버 끄고) 앱 생성(python manage.py startapp 앱이름) 
-> 앱등록(settings.py의 INSTALLED_APPS 리스트에 추가)
  
- 가상환경을 쓰는 이유: 프로젝트 별로 pip로 설치되는 패키지를 독립적으로 관리하기 위함
  
- requirements.txt에 쓰여있는 모든 패키지 설치하는 방법:
  
    ```bash
    pip install -r requirements.txt
  ```
  
- Project
  - Appliction(앱)의 집합
  - 프로젝트에는 여러 앱이 포함될 수 있다. (앱은 여러 프로젝트에 있을 수 있다.)
  - 프로젝트 구조
    - __ init  __.py
      - Python에게 이 디렉토리를 하나의 Python 패키지로 다루도록 지시
      - 건들지 말기
      
    - asgi.py
      - Asynchronous Server Gateway Interface
      - Django 애플리케이션이 비동기식 웹 서버에 연결 및 소통하는 것을 도움
      
    - settings,py
      
      - 애플리케이션의 모든 설정을 포함
      
      ```python
      LANGUAGE_CODE = 'ko-kr'
      TIME_ZONE = 'Asia/Seoul'
      USE_I18N = True	#번역 시스템 활성화 여부
      USE_L10N = True	#현지화 데이터 형식 사용 여부
    USE_TZ = True	#시간대 인식 여부 설정
      ```
      
    - urls.py
      - 사이트의 url과 적절한 views의 연결을 지정
      - HTTP request를 받는다
      
    - wsgi.py
      - Web Server Gateway Interface
      - Django 애플리케이션이 웹 서버와 연결 및 소통하는 것을 도움
      
    - manage.py
      - Django 프로젝트와 다양한 방법으로 상호작용하는 커맨드라인 유틸리티
      - ex. runserver
  
- Application
  - 앱은 실제 요청을 처리하고 페이지를 보여주고 하는 등의 역할을 담당
  - 하나의 프로젝트는 여러 앱을 가짐.
    - application 이름은  일반적으로  복수형으로 한다.
  - 일반적으로 앱은 하나의 역할 및 기능 단위로 작성함
  - Application 구조
    - admin.py
      - 관리자용 페이지 설정
    - apps.py
      - 앱의 정보가 작성된 곳
    - models.py
      - 앱에서 사용하는 Model을 정의하는 곳
    - tests.py
      - 프로젝트의 테스트 코드를 작성하는 곳
    - views.py
      - view 함수들이 정의되는 곳
        - view함수는 무조건 **request** 인자 하나 꼭 받아야 한다.
  - 앱 등록을 해서 Django에서 인식할 수 있도록 해야한다.
    - settings.py의 INSTALLED_APPS에 추가해주자
    - 주의사항
      - 반드시 앱 생성 후 등록!!
        - 먼저 등록하고 생성하려면 앱이 생성되지 않는다
      - 등록의 순서: Local apps - Third party apps - django apps
  
  +. 데이터 흐름에 맞춰 URL VIEW TEMPLATE 순으로 작성한다



## 요청과 응답

- URLs
  - HTTP 요청(request)을 알맞은 view로 전달
- Templates
  - 실제 내용을 보여주는데 사용되는 파일
  - 파일의 구조나 레이아웃을 정의
  - Templates 파일 경로의 기본값: app폴더 안의 templates 폴더



## Template

- Django Template

  - 데이터 표현을 제어하는 도구이자 **표현**에 관련된 로직

- Django Template Language(DTL)

  - Django Template에서 사용하는 built-in system
    - 조건, 반복, 변수, 치환, 필터 등의 기능을 제공하나 파이썬 코드로 실행되는 것이 아님
      - HTML은 markup언어이기에 위 기능을 제공하지 않는다.
    - 단순히 Python이 HTML에 포함된 것이 아니며, 프로그래밍적 로직이 아니라 **프레젠테이션을 표현하기 위한 것**

  - 문법

    - Variable

      - <u>render()</u>를 사용하여 views.py에서 정의한 <u>변수</u>를 **template 파일로 넘겨 사용**
      - 변수명은 영어, 숫자, _ 조합으로 구성될 수 있으나 밑줄로는 시작할 수 없다. 공백이나 구두점 또한 사용 불가
      - .을 사용하여 변수 속성에 접근
      - render의 세번째 인자로 {'key' : value}와 같이 **딕셔너리 형태**로 넘겨주며, 여기서 정의한 **key**에 해당하는 문자열이 template에서 사용 가능한 **변수명**

      ```django
      {#변수#}
      {{ variable }}
      
      {#1#}
      def greeting(request):
      	return render(request, 'greetings.html', { 'name' : 'chun', 'age' : 'three' })
      {#greetings.html#}
      <p>
           안녕하세요 저는 {{name}}입니다!
      </p>
      
      {#2#}
      def greeting(request):
      	favorite = ['bread', 'cake', 'meat']
      	info ={
      		'name' : 'Chun', 'age' : 'three'
      	}
      	context = { 'favorite': favorite, info' : info }
      	#왼쪽의 키로 접근하는 것
      	return render(request, 'greetings.html',context)
      {#greetings.html#}
      <p>
          안녕하세요 저는 {{info.name}}입니다!
          제가 좋아하는 것은 {{favorite}}입니다~		 #리스트로 출력된다
          제가 제일 좋아하는 것은 {{favorite.0}}입니다	#bread
      </p>
      ```

    - Filters

      - 표시할 변수를 수정할 때 사용 
      
        - ex. lower: 소문자로 출력하기 

          ​	  length: 길이
      
          ​      join:', ': 리스트에 있는 요소들을 합쳐준다
      
          ​	- 괄호 없음 유의!!
      
      - 60개의 built-in template filter를 제공
      
      - chained가 가능하며 일부 필터는 인자를 받기도 함
      
        - chained: 여러 필터를 같이 쓰는 것. 변수|필터|필터
        - 인자는 콜론(:) 이후에 받는다
      
      ```django
      {#Filter#}
      {{ variable|filter }}
      
      {#1#}
      {#greetings.html#}
      <p>
          안녕하세요 저는 {{info.name|lower}}입니다!
          제가 좋아하는 것은 {{favorite}}입니다~		 #리스트로 출력된다
          제가 제일 좋아하는 것은 {{favorite.0}}입니다	#bread
      </p>
      
      {#2#}
      #urls.py
      urlpatterns=[path('meal/', views.meal)]
      {#views.py#}
      import random
      def meal(requests):
      	foods=['chicken', 'hamburger', 'bulgogi']
    	pick = random.choice(foods)
      	context={
      		'foods' = foods,
      		'pick' = pick,		
      	}
      	return render(request, 'meal.html', context)
      {#meal.html#}
      <body>
          <h1>
              저녁 후보: {{foods|join:', '}}
              오늘 저녁은 {{pick}}!
          </h1>
          <a href='/index/'>back</a>
      </body>
      ```
      
    - Tags

      - 출력 텍스트를 만들거나, 반복 또는 논리를 수행하여 제어 흐름을 만드는 등 변수보다 복잡한 일들을 수행
      - 일부 태그는 **시작과 종료 태그**가 필요
        - for, if, comment 등
      - 약 24개의 built-in template tags 제공

      ```django
      {#Tags#}
      {% tag %}
      
      {#meal.html#}
      <p>menus</p>
      <ul>
          {% for food in foods %}
          	<li>{{food}}</li>
          {% endfor %}
      </ul>
      
      {#built-in template tags#}
      {{forloop.counter}}	{# 앞에 숫자 붙여준다. 1. 2. 3. ... #}
      {{forloop.first}}	{# 첫 바퀴일 때 실행 #}
      {% empty %}			{# 리스트가 비었을 때 #}
      {% lorem 3 w %}		{# lorem 중 세 단어. w 대신 p 쓰면 세 문단. random이 추가: 임의로 선택된 것 온다. #}
      {{4|add:6}}			{# 결과로 10이 출력되며, add 이외의 연산은 없다!! #}
      {% now "DATETIME_FORMAT" %}{# 현재 날짜와 시간 표현 #}
      ```

- Template inheritance(템플릿 상속)

  - 코드의 재사용성에 초점을 맞춤
  - 템플릿 상속을 사용하면 사이트의 모든 공통 요소를 포함하고, 하위 템플릿이 재정의(**override**)할 수 있는 블록을 정의하는 기본 '**skeleton**' 템플릿을 만들 수 있음
    - 장고 프로젝트를 가진 최상단 폴더(BASE_DIRS)에 templates 폴더를 만들고 그 안에 skeleton 템플릿을 위한 base.html을 만든다. 그 후 꼭!! settings.py의 templates의 DIRS 리스트에 경로 추가해주기. BASE_DIR/'templates'
      - 객체지향적으로 주소가 썼기 때문에 구동되는 운영체제에 맞춰 번역이 된다.
  - tags
    - {% extends '부모템플릿의 이름' %}: 자식(하위) 템플릿이 부모 템플릿을 확장한다는 것을 알림. 반드시 템플릿 최상단에 작성되어야 함
    - {% block content(이름) %} {%endblock content(이름) %}: 하위 템플릿에서 재지정(overridden)할 수 있는 블록을 정의. => 하위 템플릿이 채울 수 있는 공간

- Template Tag

  - {% include '_nav.html' %}: base에서 load하기 위함. 템플릿을 로드하고 현재 페이지로 렌더링. 템플릿 내에 다른 템플릿을 포함하는 방법.
    - 파일명 앞의 _는 단순히 include되는 템플릿이라는 것을 분류하기 위함. 특수 기능이나 규칙 포함되는 것이 아니다.

- Django template system(Django 설계 철학)

  - 표현과 로직(view)을 분리 => 템플릿 시스템은 표현을 제어하는 도구이자 표현에 관련된 로직일 뿐.
  - 중복을 배제 => 상속의 기초



## HTML Form

- HTML "Form" element
  - 웹에서 사용자의 정보를 입력하는 여러 방식을 제공하고, 사용자로부터 할당된 데이터를 서버로 전송하는 역할을 담당
  - 핵심 속성
    - action: 입력 데이터가 전송될 URL 지정
    - method: 입력 데이터 전달 방식 지정. GET/POST
- HTML "input" element
  - 사용자로부터 데이터를 입력 받기 위해 사용
  - type 속성에 따라 동작 방식이 달라짐
  - 핵심 속성
    - name
      - 중복 가능, 양식을 제출했을 때 name이라는 **이름**에 설정된 값을 넘겨서 **값을 가져올 수 있음**
      - 주요 용도는 GET/POST 방식으로 서버에 전달하는 파라미터로 매핑하는 것
      - GET 방식에서는 URL에서 ?key=value&key=value 형식으로 데이터 전달
- HTML "label" element
  - 사용자 인터페이스 항목에 대한 설명을 나타냄
  - label을 input 요소와 연결하기
    1. input에 id 속성 부여
    2. label에는 input의 id와 동일한 값의 for 속성이 필요
  - label과 input 요소 연결의 주요 이점
    - 시각적인 기능 뿐만 아니라 화면 리더기에서 label을 읽어 사용자가 입력해야 하는 텍스트가 무엇인지 더 쉽게 이해할 수 있도록 돕는 프로그래밍적 이점도 있음
    - label을 클릭해서 input에 초점을 맞추거나 활성화 시킬 수 있음
- HTML "for" attribute
  - for 속성의 값과 일치하는 id를 가진 문서의 첫  번째 요소를 제어
    - 연결된 요소가 labelable elements인 경우 이 요소에 대한 labeled control이 됨
  - "labelable elements"
    - label 요소와 연결할 수 있는 요소
    - button, input(not hidden type), select, textarea...
- HTML "id" attribute
  - 전체 문서에서 고유해야하는 식별자를 정의. label for 연결.
  - 사용목적: linking, scripting, styling 시 요소를 식별
- HTTP(HyperText Transfer Protocol)
  - 웹에서 이루어지는 모든 데이터 교환의 기초
  - 주어진 리소스가 수행할 작업을 나타내는 request methods를 정의
  - HTTP request method 종류: GET, POST, PUT, DELETE 등
  - HTTP request method - "GET"
    - 서버로부터 정보를 조회하는데 사용.
    - 데이터를 서버로 전송할 때 body가 아닌 Query String Parameters를 통해 전송
    - 우리는 서버에 요청을 하면 HTML 문서 파일 한 장을 받는데, 이 때 사용하는 요청의 방식이 GET

```django
{# urls.py #}
from django.urls import path
...
urlpatterns = [
	path('throw/', views.throw),
	path('catch/', views.catch)
]

{# views.py #}
from django.shortcuts import render
...
def throw(request):
	return render(request,'throw.html')
def catch(request):
	message = request.GET.get('message')	{# get: 키 값 없을 때 None 출력 #}
	context={
		'message' : message
 	}
	return render(request,'catch.html', context)

{# throw.html #}
{% extends 'base.html' %}
	<h1>Throw</h1>
	<form action="#" method="#">
        <label for="message">Throw</label>
        <input type="text" id="message" name="message">
        <input type="submit">
</form>
{% endblock %}

{# catch.html #}
{% extends 'base.html' %}
{% block content %}
	<h1>Catch</h1>
	<h2>여기서 {{message}}를 받았어~</h2>
    <a href="/throw/"> 다시 던지기</a>	
{# /throw/는 앞의 /는 상대경로, 뒤의 /는 관용적 표현 #}
{% endblock %}
```



## URL

- Django URLs

  - Dispatcher(발송자, 운항 관리자)로서의 URL
  - 웹 어플리케이션은 URL을 통한 클라이언트의 요청에서부터 시작됨

- Variable Routing

  - URL 주소를 변수로 사용하는 것

  - URL의 일부를 변수로 지정하여 view 함수의 인자로 넘길 수 있음

    => 변수 값에 따라 하나의 path()에 여러 페이지를 연결시킬 수 있음

  ```django
  path('accounts/user/<int:user_pk>/',...)
      accounts/user/1	{# 1번 user 관련 페이지 #} 
      accounts/user/2	{# 2번 user 관련 페이지 #} 
  path('blog/<int:id>/', views.blog)
  ```

- URL Path converters

  - str
    - '/'를 제외하고 비어 있지 않은 모든 문자열과 매치
    - 작성하지 않을 경우 기본 값
  - int
    - 0 또는 양의 정수와 매치
  - slug
    - ASCII 문자 또는 숫자, 하이픈 및 밑줄 문자로 구성된 모든 슬러그 문자열과 매치
  - ~~uuid/path~~

  ```django
  {# urls.py #}
  from django.urls import path
  ...
  urlpatterns = [
  	path('hello/<name>{#1#}', views.hello),	{# str은 생략 가능 #}
  ]
  
  {# views.py #}
  from django.shortcuts import render
  ...
  def hello(request,name{#1#}):
  	context={
  		'name'{#2#} : name{#1#}
   	}
  	return render(request,'hello.html', context)
  
  {# hello.html #}
  {% extends 'base.html' %}	{# 항상 최상단에 와야한다 #}
  {% block content %}
  	<h1>안녕, {{name}}{#2#}</h1>
  {% endblock %}
  ```

- App URL mapping

  - app의 view 함수가 많아짐 -> 사용하는 path() 증가, app 또한 더 많이 작성됨 
    (프로젝트의 urls.py에서 모두 관리하는 것은 프로젝트 유지보수에 좋지 않음)
    => **각각의 앱 안에 urls.py을 생성**하고 프로젝트 urls.py에서 각 앱의 urls.py 파일로 **URL 매핑을 위탁**

    ```python
    {# firstpjt/urls.py #}
    from django.contrib import admin
    from django.urls import path, include
    urlpatterns  = [
    	path('admin/', admin.site.urls),
        path('articles/', include('articles.urls')),
        path('pages/', include('pages.urls'))
    ]
    ```

  - url pattern은 언제든지 다른 URLconf 모듈을 포함할 수 있음

  - include()

    - 다른 URLconf(app1/urls.py)들을 참조할 수 있도록 도움
    - 함수 include()를 만나게 되면, URL의 그 시점까지 일치하는 부분을 잘라내고, 남은 문자열 부분을 후속 처리를 위해 include된 URLconf로 전달
    - django는 명시적 상대경로(from module import ..)를 권장

- Naming URL patterns

  - 이제는 링크에 url을 직접 작성하는 것이 아니라 path()함수의 name 인자를 정의해서 사용
  - Django Template Tag 중 하나인 url 태그를 사용해서 path() 함수에 작성한 name을 사용할 수 있음
  - url 설정에 정의된 특정한 경로들의 의존성을 제거할  수 있음

  ```django
  path('index/', view.index, name='index')
  
  <a href="{% url 'index' %}">메인 페이지</a>
  ```

  - 주어진 URL 패턴 이름 및 선택적 매개 변수와 일치하는 절대 경로 주소를 반환
  - 템플릿에 URL을 하드 코딩하지 않고도 DRY 원칙을 위반하지 않으면서 링크를 출력하는 방법



## Namespace

- 객체를 구분할 수 있는 범위를 나타내는 말. 일반적으로 하나의 이름 공간에서는 하나의 이름이 단 하나의 객체만을 가리키게 된다.

- 모든 변수명과 함수명 등이 모두 겹치지 않게 정의하는 것은 어렵다.

- 문제점

  1. articles 앱의 index 페이지에서 두번째 앱 pages의 index로 이동하는 하이퍼링크를 클릭 시 현재 페이지로 이동 => url namespace
  2. pages 앱 index url로 이동해도 articles 앱의 index 페이지가 출력됨 => Template namespace

  => 약속된 경로 앞에는 쓰지 않기 때문에 발생. 서버가 켜지면 템플릿들을 모아서 보게 되는데, 앱을 <u>등록한 순서대로</u> 선택하게 된다.

- 해결책

  1. 서로 다른 앱의 같은 이름을 가진 url name은 **이름공간**을 설정해서 구분

     - urls.py에 "app_name" attribute 값 작성 후 참조.

  2. templates, static 등 django는 정해진 경로 <u>하나로</u> 모아서 보기 때문에 중간에 **폴더를 임의로 만들어주어** 이름 공간을 물리적으로 설정

     - 관행적으로 앱 이름과 같은 폴더를 templates 안에 만들어주고 기존의 템플릿들을 모두 넣어준다.

     - 경로의 변화: articles/templates/index.html -> articles/templates/**articles**/index.html

       - 장고와 약속된 경로는 articles/templates까지. 그 뒤부터 읽음.

         => **articles**가 templates의 이름공간 역할을 한다.

       ```python
       #urls.py
       #전
       def index(request):
           return render(request, 'index.html')
       #물리적으로 이름공간 설정 후
       def index(request):
           return render(request, 'articles/index.html')
       ```

```python
# settings.py
...
TEMPLATES = [
	{
		...
		'DIRS': [BASE_DIR/'templates',]
		...
	}
]

# pjt/urls.py
urlpatterns=[
	path('pages/', include('pages.urls'))
]

# articles/urls.py
from . import views
app_name='articles'
urlpatterns=[
	path('/index', views.index, name='index')
]

# pages/urls.py
from django.urls import path
from . import views	# 명시적인 상대경로
app_name='pages'
urlpatterns=[
	path('index/', views.index, name='index')
]

# pages/views.py
def index(request):
	return render(request, 'index.html')

# pages/templates/index.html
# 참조 : 어떤 앱의 url인지 붙여준다
{% extends 'base.html' %}
{% block content %}
	<a href="{% url 'pages:index' %}"></a>
	<h1>두번째 앱의 index</h1>
{% endblock %}
```



## Static files

- 웹 서버와 정적 파일

  - 웹서버: 특정 위치(URL)에 있는 자원(resource - data -)을 요청(HTTP request)을 받아서 제공(serving)하는 응답(HTTP response)을 처리하는 것을 기본 동작으로 한다.

    => 자원과 접근 가능한 주소가 정적으로 연결된 관계.

    => 웹 서버는 요청 받은 URL로 서버에 존재하는 **정적 자원**(statuc resource)을 제공

- Static file
  - 응답할 때 별도의 처리 없이, 사용자의 요청에 따라 내용이 바뀌는 것이 아니라 파일 내용을 **그대로** 보여주면 되는 파일.
  - 파일 자체가 고정되어있고, 서비스 중에도 추가되거나 변경되지 않고 고정되어 있음.

### Static file의 구성

1. django.contrib.staticfiles가 INSTALLED_APPS에 포함되어 있는지 확인
2. settings.py에서 STATIC_URL을 정의
3. 템플릿에서 static 템플릿 태그를 사용하여 지정된 상대경로에 대한 URL을 빌드
4. 앱의 static 디렉토리에 정적 파일을 저장.

```django
{% load static %}
<img src="{% static 'my_app/example.jpg' %}" alt="img">
{# app/static 폴더에 이미지 넣기 #}
{# app/static 안에 app 폴더를 만들어 물리적으로 공간 설정해주어 문제가 생기지 않도록 한다. #}
```

* The staticfiles app
  * STATICFILES_DIRS
    - 'app/static/' 디렉토리 경로(기본 경로)를 사용하는 것 외에 추가적인 정적 파일 경로 목록을 정의하는 리스트
    - 추가 파일 디렉토리에 대한 전체 경로를 포함하는 문자열 목록으로 작성되어야 함
    
  * STATIC_URL

    * STATIC_ROOT에 있는 정적 파일을 **참조**할 때 사용할 **URL**
      - <u>개발 단계</u>에서는 실제 정적 파일들이 저장되어 있는 'app/static' 경로(**기본 경로**) 및 STATICFILES_DIRS에 정의된 **추가 경로**들을 탐색함
    - 실제 파일이나 디렉토리가 아니며, **URL로만 존재**
    * <u>비어 있지 않은 값</u>으로 설정 한다면 **반드시 슬래시(/)로** 끝나야 함
      - 장고는 trailing comma와 end slash를 지킨다

  * STATIC_ROOT

    * collectstatic이 배포를 위해 정적 파일을 수집하는 디렉토리의 절대 경로

      * collectstatic: STATIC_ROOT에 정적 파일을 수집

    * django 프로젝트에서 사용하는 **모든 정적 파일을 한 곳에 모아 넣는 경로**

    * 개발 과정에서 settings.py의 DEBUG 값이 True로 설정되어 있으면 해당 값은 작용되지 않음

      * 직접 작성하지 않으면 django 프로젝트에서는 settings.py에 작성되어 있지 않음

        +. 장고의 상태는 개발 단계와 배포 단계로 나누어져 있다.

      ​	- 배포: 외부로 서비스 하기 위해 이 장고 프로젝트를 서버로 올리는 과정. DEBUG 값을 False로 바꾼다(에러 화면이 불친절해진다)

    * 실 서비스 환경(배포 환경)에서 django의 모든 정적 파일을 다른 웹 서버가 직접 제공하기 위함

    ```python
    {# settings.py #}
    STATICFILES_DIRS=[
    	BASE_DIR/'static',
    ]
    STATIC_URL = '/static/'
    ```

### Django template tag

- load
  - 사용자 정의 템플릿 태그 세트를 로드(static은 빌트인 태그가 아니기 때문. static 쓸 때 로드해주어야 한다)
  - 로드하는 라이브러리, 패키지에 등록된 모든 태그와 필터를 불러옴
- static
  - STATIC_ROOT에 저장된 정적 파일에 연결

```django
{# articles/static/에 이미지 저장 #}
{# 기본 #}
{% load static %}
<img src="{% static 'ex.jpg' %}" alt='img'>

{# 이름 공간 설정 위해 추가 파일 생성. articles/static/articles/에 이미지 저장 #}
{% load static %}
<img src="{% static 'articles/ex.jpg' %}" alt='img'>

{# 다른 공간의 정적 파일을 가져와야 한다면? 경로를 추가하기 위해 설정하기 #}
{# settings.py #}
STATICFILES_DIRS = [BASE_DIR / 'static']
{# 최상단에 static 폴더 만든다 #}
{# base.html #}
{% load static %}
<link rel="stylesheet" href="{% static 'style.css' %}"
```



## Model

- 웹 애플리케이션의 데이터를 **구조화**하고 **조작**하기 위한 도구

- 단일한 데이터에 대한 정보를 가짐.
  - 사용자가 저장하는 데이터들의 필수적인 필드들과 동작들을 포함

- 저장된 데이터베이스의 **레이아웃**
- <u>Django</u>는 model을 통해 **데이터에 접속하고 관리**.
- 일반적으로 **각각의 model**은 **하나의 데이터베이스 테이블에 매핑됨.**

### Database

- 데이터베이스(DB): 체계화된 데이터의 모임
- 쿼리(Query)
  - 데이터를 **조회**하기 위한 명령어/조건에 맞는 데이터를 **추출하거나 조작**하는 명령어
  - Query를 날린다 = DB를 조작한다.

#### Database의 기본 구조

- 스키마(Schema): 데이터베이스에서 제약조건(자료의 구조, 표현방법, 관계 등)에 관련한 전반적인 명세를 기술한 것
- 테이블: 열과 행의 모델을 사용해 조직된 데이터 요소들의 집합. SQL 데이터베이스에서는 테이블을 관계라고도 한다.
  - 열(column): 필드, 속성
    - 각 열에는 고유한 데이터 형식이 지정
  - 행(row): 레코드, 튜플
    - 테이블의 데이터 저장됨
    - 기본키: 각 행의 고유값으로, PK(Primary Key)라고 한다. <u>반드시 설정</u>하여야하며, 데이터베이스 관리 및 관계 설정 시 주요하게 활용된다.



## ORM

> Object-Relational-Mapping

- 객체 지향 프로그래밍 언어를 사용하여 **호환되지 않는 유형의 시스템 간**(<u>Django-SQL</u>)에 **데이터를 변환**하는 프로그래밍 기술
- OOP 프로그래밍에서 RDBMS를 연동할 때, 데이터베이스와 객체 지향 프로그래밍 언어 간의 **호환되지 않는 데이터를 변환**하는 프로그래밍 기법
- Django에서는 내장 Django ORM을 사용
- 장점
  - SQL을 잘 알지 못해도 DB 조작 가능
  - SQL의 정차적 접근이 아닌 **객체 지향적 접근**으로 인한 높은 **생산성**(웹 개발의 속도를 높이는 것 - 현대 웹 프레임워크의 요점)
- 단점
  - ORM 만으로 완전한 서비스를 구현하기 어려운 경우가 있음.

### models.py 작성

```python
class Article(models.Model):
    title = models.CharField(max_length=10)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

- 각 모델은 django.models.Model 클래스의 서브 클래스로 표현됨

  - django.db.models 모듈의 Model 클래스를 상속받음

- models 모듈을 통해 어떠한 타입의 DB 컬럼을 정의할 것인지 정의

  - title, content는 모델의 필드를 나타냄
  - 각 **필드**는 **클래스 속성**으로 지정됨.
  - 각 **속성**은 각 데이터베이스의 **열**에 매핑.

- 사용 모델 필드

  - CharField(max_length=None, **options)

    - 길이의 제한이 있는 문자열을 넣을 때. max_length는 필수 인자
    - **필드의 최대 길이(문자)**, 데이터베이스 레벨과 Django의 유효성검사(값 검증)에서 활용

  - TextField(**options)

    - 글자의 수가 많을 때 사용
    - max_length 적용 시 자동 양식 필드인 textarea <u>위젯에 반영</u>은 되지만 <u>모델과 데이터베이스 수준에는 **적용되지 않음**</u>

  - DateTimeField options(DateField options와 동일한 추가 인자 사용_ DateTimeField는 DateField의 서브 클래스이기 때문)

    - auto_now_add
      - **최초 생성** 일자
      - Django ORM이 **최초 insert**(테이블에 데이터 입력)시에만 현재 날짜와 시간으로 갱신.
    - auto_now
      - **최종 수정** 일자
      - Django ORM이 save할 때마다 현재 날짜와 시간으로 갱신

    

## Migrations

- Django가 model에 생긴 변화를 반영하는 방법

- 명령어

  - makemigrations	$ python manage.py makemigrations

    - model을 **변경**한 것에 기반한 **새로운 migration**(설계도 개념)을 **만들 때** 사용. 추가로 모델 필드 작성할 때 makemigrations 진행해야함!
    - migrations/0001_initial.py 생성 확인

  - migrate                   $ python manage.py migrate

    - migration을 **DB에 반영**하기 위해 사용
    - 모델에서의 <u>변경 사항들과 DB의 스키마</u>가 **동기화**를 이룸
    - 0001_initial.py 설계도를 실제 DB에 반영

  - sqlmigrate              $ python manage.py sqlmigrate app_name 0001

    - migration에 대한 **SQL 구문**을 보기 위해 사용
    - migration이 SQL 문으로 <u>어떻게 해석되어서 동작할지</u> 미리 확인할 수 있음

  - showmigrations    $ python manage.py showmigrations

    - 프로젝트 <u>전체</u>의 **migration 상태를 확인**하기 위해 사용
    - migration 파일들의 migrate 여부를 확인할 수 있음

    

## Database API

- DB를 조작하기 위한 도구
- Django가 기본적으로 ORM을 제공함에 따른 것으로 **DB를 편하게 조작**할 수 있도록 돕는다.
- Model을 만들면 Django는 <u>객체들을 만들고 읽고 수정하고 지울 수 있는</u> **database-abstract API(=database-access API)**를 **자동으로 만듬**

### DB API 구문 - Making Queries

- Article.objects.all()	=> Class Name.Manager.QuerySet API
  - Manager
    - Django 모델에 **데이터베이스 query 작업이 제공**되는 <u>인터페이스</u>
    - 기본적으로 모든 Django 모델 클래스에 **objects**라는 <u>Manager 추가</u>
  - QuerySet
    - 데이터베이스로부터 전달받은 객체 목록
    - queryset 안의 객체는 0개, 1개, 혹은 여러개일 수 있다
    - 데이터베이스로부터 <u>조회, 필터, 정렬 등을 수행</u>할 수 있다

### Django shell

- 일반 Python shell을 통해서는 장고 프로젝트 환경에 접근할 수 없음

- 따라서 장고 프로젝트 설정이 load된 Python shell을 활용해 DB API 구문 테스트 진행

  - Django-extensions 라이브러리의 기능 중 하나인 shell_plus 사용해서 진행
  - ipython, django-extensions 설치 후 settings.py에서 앱 등록 후 shell_plus 진행

  

## CRUD

- 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리기능인 Create, Read, Update, Delete를 묶어서 일컫는 말

### Create

- 방법1) 인스턴스 생성 후 인스턴스 변수 설정

```shell
article = Article()			#Article(class)로부터 Article(instance)
article.title = 'first'		#인스턴스 변수에 값을 할당
article.content = 'django'
article.save()				
```

- 방법2) 초기 값과 함께 인스턴스 생성

```shell
article = Article(title='second', content='django')
article.save()
```

- 방법3) QuerySet API - create() 사용

```shell
Article.objects.create(title='third', content='django')
#바로 쿼리 표현식 리턴
```

- save 메서드

  - 객체를 데이터베이스에 저장
  - 데이터 생성 시 save()를 호출하기 전에는 객체의 ID 값이 무엇인지 알 수 없음(ID 값은 Django가 아니라 **DB에서 계산되기 때문**)
  - 단순히 모델을 인스턴스화 하는 것은 DB에 영향을 미치지 않는다. => **반드시 save()**해야함!

- str 메서드

  ```python
  class Article(models.Model):
      title = models.CharField(max_length=10)
      content = models.TextField()
      created_at = models.DateTimeField(auto_now_add=True)
      updated_at = models.DateTimeField(auto_now=True)
      
      def __str__(self):
          return self.title
  ```

  - 표준 파이썬 클래스의 메소드인 str()을 정의하여 각각의 object가 사람이 읽을 수 있는 **문자열을 반환(return)하도록** 할 수 있음
  - **작성 후 반드시 shell_plus 재시작해야 반영됨**

### Read

- DB에 앤스턴스 객체를 얻기 위한 쿼리문 날리기

```shell
>>> Article.objects.all()	#전체 article 객체 조회
<QuerySet []>	#레코드가 하나만 있으면 인스턴스 객체로, 두 개 이상이면 쿼리셋으로 리턴
```

- QuerySet API method의 종류

  - Methods that **return new querysets**
  - Methods that **do not return querysets**

- QuerySet API method

  - all(): 현재 QuerySet의 **복사본을 반환**

  - get()

    - 주어진 lookup 매개변수와 **일치**하는 객체를 반환
    - <u>객체를 찾을 수 없으면</u> **DoesNotExist 예외**를 발생. <u>둘 이상의 객체</u>를 찾으면 **MultipleObjectsReturned 예외**를 발생 시킴
      - 위와 같은 특징으로 인해 PK와 같이 고유성을 보장하는 조회에서 사용해야 함

  - filter()

    ```shell
    >>> Ariticle.objects.filter(content='django')
    <QuerySet [<Article:first>,<Article:second>,<Article:third>]>
    ```

    - 주어진 lookup 매개변수와 일치하는 객체를 포함하는 **새 QuerySet을 반환**

- Field lookups

  ```shell
  Article.objects.filter(pk__gt=2)
  Article.objects.filter(content__contains='an')
  ```

  - 조회 시 특정 검색 조건을 지정
  - QuerySet 메서드 filter(), exclude() 및 get()에 대한 키워드 인수로 지정됨

+. 게시글 정렬 순서 변경

```python
def index(request):
    #1 DB로 부터 받은 쿼리셋을 파이썬이 변경
    articles=Article.objects.all()[::-1]
    #2 처음부터 내림차순으로 쿼리셋을 받는다(DB가 조작)
    articles=Article.objects.order_by('-pk')
```

### Update

```shell
article.title='bye'	#값 변경 후 저장
article.save()
```

- article 인스턴스 객체의 인스턴스 변수의 값을 변경 후 저장

### Delete

```shell
>>> article = Article.objects.get(pk=1)
>>> article.delete()
(1, {'articles.Article':1})
```

- QuerySet의 **모든 행에 대해** SQL 삭제 쿼리를 수행하고, <u>삭제된 객체 수와 객체 유형 당 삭제 수가 포함</u>된 **딕셔너리를 반환**



## Admin Site

### Automatic admin interface

- 사용자가 아닌 서버의 관리자가 활용하기 위한 페이지
- Model class를 admin.py에 등록하고 관리
- django.contrib.auth 모듈에서 제공됨
- record 생성 여부 확인에 매우 유용하며, 직접 record를 삽입할 수도 있음

### admin 생성

```bash
$ python manage.py createsuperuser
```

- 관리자 계정 생성 후 서버를 실행한 다음 '/admin'으로 가서 관리자 페이지 로그인
  - 계정만 만든 경우 Django 관리자 화면에서 아무것도 보이지 않음
- 내가 만든 Model을 보기 위해서는 admin.py에 작성하여 Django 서버에 등록
- [주의] auth에 관련된 기본 테이블이 생성되지 않으면 관리자 계정을 생성할 수 없음

### admin 등록

```python
#articles/admin.py
from django.contrib import admin
from .models import Article

#admin site에 register하겠다
admin.site.register(Article)
```

- admin.py는 관리자 사이트에 Article 객체가 관리자 인터페이스를 가지고 있다는 것을 알려주는 것
- models.py에 정의한 __ str __의 형태로 객체가 표현됨

### ModelAdmin options

```python
#articles/admin.py
from django.contrib import admin
from .models import Article

class ArticleAdmin(admin.ModelAdmin):
    list_display=('pk','title','content',)

admin.site.register(Article, ArticleAdmin)
```

- list_display: models.py 정의한 각각의 속성(칼럼)들의 값(레코드)을 admin 페이지에 출력하도록 설정



## CRUD with views

### HTTP method

- HTTP request method - "GET"
  - 특정 리소스를 가져오도록 요청할 때 사용
  - 반드시 데이터를 가져올 때만 사용해야 함.
  - DB에 변화를 주지 않음
  - CRUD에서 R 역할

* HTTP request method - "POST"
  * 서버로 데이터를 전송할 때 사용
  * 리소스를 생성/변경하기 위해 데이터를 HTTP body에 담아 전송.
  * 서버에 변경사항을 만듦
  * CRUD에서 C, U, D 역할 담당

### 사이트 간 요청 위조(CSRF)

> Cross-site request forgery

- 웹 애플리케이션 취약점 중 하나로 사용자가 자신의 의지와 무관하게 **공격자가 의도한 행동**을 하여 특정 웹페이지를 보안에 취약하게 하거나 수정, 삭제 등의 작업을 하게 만드는 **공격 방법**
- Django는 CSRF에 대항하여 middleware와 template tag를 제공
  - middleware: 공통 서비스 및 기능을 애플리케이션에 제공하는 소프트웨어. 데이터 관리, 인증 및 API 관리 등을 처리
  - 공격방어를 위한 middleware는 settings.py의 MIDDLEWARE에 작성되어 있다.

#### CSRF 공격 방어

- Security Token 사용 방식(CSRF Token)
  - 사용자의 데이터에 임의의 난수 값을 부여해, 매 요청마다 해당 난수 값을 포함시켜 전송시키도록 함
  - 이후 서버에서 요청을 받을 때마다 전달된 token의 값이 유효한지 검증
  - 데이터 변경이 가능한 POST, PATCH, DELETE Method 등에 적용(GET 제외)

#### csrf_token template tag

{% csrf_token %}

* CSRF 보호에 사용됨
* input type이 hidden으로 작성됨. value는 Django에서 생성한 hash값으로 설정됨
* 해당 태그 <u>없이</u> 요청을 보낸다면 Django 서버는 <u>403 forbidden</u>을 응답

### redirect

- 새 URL로 요청을 보냄.
- 브라우저는 현재 경로에 따라 전체 URL 자체를 재구성
  - return redirect('articles:index')

### Variable Routing

- 글의 번호를 활용해 각각의 페이지를 따로 구현해야하는 경우 사용

  ```python
  #articles/urls.py
  path('< int:pk >/', views.detail, name='detail')
  
  #articles/views.py
  def detail(request,pk):
      article=Article.objects.get(pk=pk)
      #왼쪽pk는 DB에 저장된 레코드의 pk(id), 오른쪽pk는 variable routing을 통해 받은 pk
      return render(request,'articles/detail.html',{'article':article})
  ```