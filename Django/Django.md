# Django:Template, View, Routing

> Django: Python Web framework

## Web Framework

- Web: World Wide Web의 약자. 인터넷에 연결된 컴퓨터를 통해 정보를 공유할 수 있는 전 세계적인 정보 공간. 인터넷 공간
  - Static  web page(정적 웹 페이지)  (=Flat page)
    - 서버에 미리 저장된 파일이 사용장게 그대로 전달되는 웹 페이지. 
    - 요청 받은 경우 서버는 **추가적인 처리 과정 없이** 클라이언트에게 응답을 보냄 => **모든 사용자에게 같은 결과를 보냄**
      - 클라이언트는 네트워크를 통해 data를 얻기 위해 서버라는 원격 서버에 접속할 수 있다.
        - 클라이언트의 종류: 데스크탑, 스마트폰, **웹 브라우저**(크롬)
        - 서버 구축하는 Framework: Django
        - 클라이언트가 서버에 요청했을 때, URL요청이 왔을 때(urls.py), 작업을 해서(views.py), HTML 응답(Template)
      - 클라이언트  --요청-->  서버
      - 서버  --응답-->  클라이언트
    - <u>HTML, CSS, JavaScript</u>로 작성된다.
  - Dynamic web page
    - 웹 페이지에 대한 요청을 받은 경우 서버는 **추가적인 처리 과정** 이후 클라이언트에게 응답을 보냄
    - 동적 웹 페이지는 **방문자와 상호작용**하기 때문에 **페이지 내용은 그때그때 다름**
    - 서버 사이드 프로그래밍 언어(<u>Python, Java, C++ 등</u>)이 사용됨. 파일을 처리하고 데이터베이스와의 상호작용(저장, 수정, 삭제, 조회)이 이루어짐

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
  - 인스타그램, 스포티파이, 드롭박스 등

- Framework Architecture

  - MVC(Model-View-controller) Design Pattern
    - 소프트웨어 공학에서 사용되는 디자인 패턴 중 하나
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

- 가상환경 생성 및  활성화 > django 설치 > 프로젝트 생성 > 서버 켜서 로켓 확인하기  > (ctrl+c로 서버 끄고) 앱 생성 > 앱등록
  
  - 가상환경을 쓰는 이유: 프로젝트 별로 pip로 설치되는 패키지를 독립적으로 관리하기 위함
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
      - 변수명은 영어, 숫자, _ 조합으로 구성될 수 있으 밑줄로는 시작할 수 없다. 공백이나 구두점 또한 사용 불가
      - .을 사용하여 변수 속성에 접근
      - render의 세번째 인자로 {'key' : value}와 같이 **딕셔너리 형태**로 넘겨주며, 여기서 정의한 **key**에 해당하는 문자열이 template에서 사용 가능한 **변수명**

      ```django
      #변수
      {{ variable }}
      
      #1
      def greeting(request):
      	return render(request, 'greetings.html', { 'name' : 'chun', 'age' : 'three' })
      #greetings.html
      <p>
           안녕하세요 저는 {{name}}입니다!
      </p>
      
      #2
      def greeting(request):
      	favorite = ['bread', 'cake', 'meat']
      	info ={
      		'name' : 'Chun', 'age' : 'three'
      	}
      	context = { 'favorite': favorite, info' : info }
      	#왼쪽의 키로 접근하는 것
      	return render(request, 'greetings.html',context)
      #greetings.html 
      <p>
          안녕하세요 저는 {{info.name}}입니다!
          제가 좋아하는 것은 {{favorite}}입니다~		 #리스트로 출력된다
          제가 제일 좋아하는 것은 {{favorite.0}}입니다	#bread
      </p>
      ```

    - Filters

      - 표시할 변수를 수정할 때 사용 ex. 소문자로 출력하기
      - 60개의 built-in template filter를 제공
      - chained가 가능하며 일부 필터는 인자를 받기도 함

      ```django
      #Filter
      {{ variable|filter }}
      
      #1
      #greetings.html
      <p>
          안녕하세요 저는 {{info.name|lower}}입니다!
          제가 좋아하는 것은 {{favorite}}입니다~		 #리스트로 출력된다
          제가 제일 좋아하는 것은 {{favorite.0}}입니다	#bread
      </p>
      
      #2
      #urls.py
      urlpatterns=[
      	path('meal/', views.meal)
      ]
      #views.py
      import random
      def meal(requests):
      	foods=['chicken', 'hamburger', 'bulgogi']
      	pick = random.choice(foods)
      	context={'pick'=pick}
      	return render(request, 'meal.html', context)
      #meal.html
      <body>
          <h1>
              오늘 저녁은 {{pick}}!
          </h1>
          <a href='/index/'>back</a>
      </body>
      ```

      

## HTML Form

## URL