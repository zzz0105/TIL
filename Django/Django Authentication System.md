# Django 사용자 인증 및 권한

## The Django Authentication System

- django.contrib.auth에 Django contrib module로 제공

- 필수 구성은 settings.py에 이미 포함되어 있으며 INSTALLED_APPS 설정에 나열된 아래 두 항목으로 구성됨. -> 별도 추가 작업 필요 없다.

  1. django.contib.auth

     인증 프레임워크의 핵심과 기본 모델을 포함

  2. django.contrib.contenttypes

     사용자가 생성한 모델과 권한을 연결할 수 있음

- Django 인증 시스템은 **인증**(Authentication)과 **권한**(Authorization) 부여를 함께 제공하며, 이런 기능이 어느 정도 결합되어 일반적으로 인증시스템이라고 한다.
  - Authentication(인증)
    - 신원 확인
    - 사용자가 자신이 누구인지 확인하는것
  - Authorization(권한, 허가)
    - 권한 부여
    - 인증된 사용자가 수행할 수 있는 작업을 결정

### 두번째 앱 생성하기

```bash
$ python manage.py startapp accounts
```

- 앱 이름이 반드시 accounts일 필요는 없으나, auth와 관련해 Django 내부적으로 accounts라는 이름으로 사용되고 있기 때문에 되도록  **accounts로 지정하는 것을 권장**



## 쿠키와 세션

### HTTP

- Hyper Text Transfer Protocol

  - HTML 문서와 같은 리소스(자원, 데이터)들을 가져올 수 있도록 해주는 프로토콜(규약, 규칙)
  - 웹에서 이루어지는 모든 데이터 교환의 기초
  - 클라이언트 - 서버 프로토콜이기도 함

- 특징

  - 비연결지향(connectionless)
    - 서버는 요청에 대한 응답을 보낸 후 연결을 끊음
  - 무상태(stateless)
    - 연결을 끊는 순간 클라이언트와 서버 간의 통신이 끝나며 상태 정보가 유지되지 않음
    - 클라이언트와 서버가 주고 받는 메세지들은 서로 완전히 독립적임

  **클라이언트와 서버의 지속적인 관계를 유지하기 위해**(ex.로그인 상태) **쿠키와 세션이 존재**

### 쿠키(Cookie)

- **서버가** 사용자의 웹 브라우저에 **전송**하는 작은 데이터 조각
- 사용자가 웹사이트를 방문할 경우 해당 웹사이트의 서버를 통해 사용자의 <u>컴퓨터에 설치</u>(placed-on. 배치한다)되는 **작은 기록 정보 파일**
  - 브라우저(클라이언트)는 쿠키를 로컬에 **KEY-VALUE**의 데이터 형식으로 저장
  - 이렇게 쿠키를 저장해놓았다가, **동일한 서버에 재요청 시 매번** <u>저장된 쿠키를 함께 전송</u>

[참고] 소프트웨어가 아니기 때문에 프로그램처럼 실행될 수 없으며 악성코드로 설치할 수 없지만, 사용자의 행동을 추적하거나 쿠키를 훔쳐 해당 사용자의 계정 접근 권한을 획득할 수도 있음

- HTTP 쿠키는 상태가 있는 **세션**을 만들어 줌
- 쿠키는 두 요청이 동일한 브라우저에서 들어왔는지 아닌지를 판단할 때 주로 사용
  - 이를 이용해 사용자의 <u>로그인 상태를 유지</u>할 수 있음
  - <u>상태가 없는(stateless)</u> HTTP 프로토콜에서 <u>상태 정보를 기억</u>시켜주기 때문

**-> 웹 페이지에 접속하면 요청한 웹 페이지를 받으며 <u>쿠키를 저장</u>하고, 클라이언트가 같은 서버에 <u>재 요청시 요청과 함께 쿠키도 함께 전송</u>**

#### 쿠키의 사용 목적

1. 세션 관리(Session managament)
   - 로그인, 아이디 자동 완성, 공지 하루 안보기, 팝업 체크, 장바구니 등의 정보 관리
2. 개인화(Personalization)
   - 사용자 선호, 테마 등의 설정
3. 트래킹(Tracking)
   - 사용자 행동을 기록 및 분석

#### 쿠키 lifetime(수명)

- 쿠키의 수명은 두 가지 방법으로 정의할 수 있음

  1. Session cookies

     - 현재 세션이 종료되면 삭제됨

     - 브라우저가 "현재 세션(current session)"이 종료되는 시기를 정의

       [참고] 일부 브라우저는 다시 시작할 때 세션 복원(session restoring)을 사용해 세션 쿠키가 오래 지속될 수 있도록 함

  2. Persistent cookies(or Permanent cookies)

     - Expires 속성에 지정된 날짜 혹은 Max-Age 속성에 지정된 기간이 지나면 삭제

### 세션(Session)

- 사이트와 특정 브라우저 사이의 "상태(state)"를 유지시키는 것
- 클라이언트가 서버에 접속하면 서버가 특정 **session id**를 발급하고, 클라이언트는 발급받은 session id를 쿠키에 저장
  - 클라이언트가 다시 서버에 접속하면 요청과 함께 (session id가 저장된) 쿠키를 서버에 전달
  - 쿠키는 요청 때마다 서버에 함께 전송되므로 <u>서버에서 session id를 확인</u>해 알맞은 로직을 처리
- <u>ID는 세션을 구별</u>하기 위해 필요하며, <u>쿠키에는 ID만 저장</u>함

#### Session in Django

- Django의 세션은 <u>미들웨어</u>를 통해 구현됨

  - [참고] MIDDLEWARE
    - HTTP 요청과 응답 처리 중간에서 작동하는 시스템(hooks)
    - Django는 HTTP 요청이 들어오면 <u>미들웨어를 거쳐</u> 해당 **URL**에 등록되어 있는 view로 연결해주고, HTTP <u>응답 역시 미들웨어를 거쳐서 내보냄</u>
    - 주로 데이터 관리, 애플리케이션 서비스, 메시징, 인증 및 API 관리를 담당

- Django는 **database**-backed sessions 저장 방식을 기본 값으로 사용

  ​	[참고] 설정을 통해 cashed, file-based, cookie-based 방식으로 변경 가능

- Django는 특정 session id를 포함하는 쿠키를 사용해서 각각의 브라우저와 사이트가 연결된 세션을 알아냄

  - 세션 정보는 Django DB의 **django_session** 테이블에 저장됨

- 모든 것을 세션으로 사용하려고 하면 사용자가 많을 때 서버에 부하가 걸릴 수 있다.

##### Authentication System in MIDDLEWARE

> settings.py의 MIDDLEWARE를 수정할 필요 없다

- SessionMiddleware
  
  - 요청 전반에 걸쳐 세션을 관리
- AUthenticationMiddleware
  
  - 세션을 사용하여 사용자를 요청과 연결
  
  

## 로그인

- 로그인은 <u>session을 Create</u>하는 로직과 같음
- Django는 우리가 session의 메커니즘에 생각하지 않게끔 도움을 줌
- 이를 위해 인증에 관한 built-in forms를 제공

### AuthenticationForm

- 사용자 로그인을 위한 form 
- request를 첫번째 인자로 취함

#### login 함수

- login(request, user,backend=None)

  - 현재 세션에 연결하려는 <u>인증된 사용자가 있는 경우</u> login() 함수가 필요
  - 사용자를 로그인하며 view함수에서 사용됨
  - HttpRequest 객체와 User 객체가 필요
  - Django의 session framework를 사용하여 세션에 user의 ID를 저장(=로그인)

```python
from django.shortcuts import render,redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login
from django.views.decorators.http import require_http_methods

@require_http_methods(['GET', 'POST'])
def login(request):	
	if request.method == 'POST':
		form = AuthenticationForm(request, request.POST) #사전 인증절차 진행. Form 상속. 
        #로그인은 DB에 저장되지 않으므로 ModelForm을 쓰지 않는다. 로그인은 session create.
		if form.is_valid():	
            auth_login(request, form.get_user()) #form.get_user(): 인증된 유저 객체가 return
            #실제 로그인 진행. session이 만들어진다
           	return redirect('articles:index')
	else:
		form = AuthenticationForm()	#사용자 이름 / 비밀번호 
	context = {
		'form' : form
	}
return render(request, 'accounts/login.html', context)
```

### Authentication data in templates

- context processors
  - 템플릿이 렌더링될 때 <u>자동으로 호출 가능</u>한 컨텍스트 데이터 목록
  - 작성된 프로세서는 RequestContext에서 사용 가능한 변수로 포함됨
- Users
  - 템플릿 RequestContext를 렌더링할 때, 현재 로그인한 사용자를 나타내는 **auth.User 인스턴스**(또는 클라이언트가 로그인하지 않은 경우 AnonymousUser 인스턴스)는 템플릿 변수 **{{ user }}**에 저장됨



## 로그아웃

> session을 삭제하는 것

### logout 함수

- logout(request)
  - HttpRequest 객체를 인자로 받고 반환 값이 없음
  - 사용자가 로그인하지 않은 경우 오류를 발생시키지 않음
  - 현재 요청에 대한 <u>session data를 DB에서 완전히 삭제</u>하고, 클라이언트의 쿠키에서도 session id가 삭제됨
  - 이는 다른 사람이 동일한 웹 브라우저를 사용하여 로그인하고, **이전 사용자의 세션 데이터에 엑세스하는 것을 방지하기 위함**

```python
from django.shortcuts import redirect
from django.contrib.auth import logout as auth_logout
from django.views.decorators.http import require_POST

@require_POST
def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```



## 로그인 사용자에 대한 접근 제한

### Limiting access to logged-in users

- 로그인 사용자에 대한 엑세스 제한 방법

  1. The raw way

     - **is_authenticated** attribute

       - User model의 속성(attributes) 중 하나
       - 모든 User 인스턴스에 대해 항상 **True**인 읽기 전용 속성(AnonymousUser에 대해서는 항상 **False**)
       - <u>사용자가 인증되었는지 여부</u>를 알 수 있는 방법
       - 일반적으로 request.user에서 이 속성을 사용하여, 미들웨어의 'django.contrib.auth.middleware.AuthenticationMiddleware'를 통과했는지 확인
       - 단, <u>권한(permission)과는 관련이 없으며</u>, 사용자가 활성화 상태(active)이거나 유효한 세션(valid session)을 가지고 있는지도 확인하지 않음

       ```django
       <!-- base.html -->
       <body>
           <div class="container">
               {% if request.user.is_authenticated %}
               	<h3>hello, {{ user }}</h3>
               	<form action='{% url 'accounts:logout' %}' method="POST"> 
                   <!--action 없으면 현재 주소로 요청보냄-->
                       {% csrf_token %}
                       <input type="submit" value="Logout">
               	</form>
               {% else %}
               	<a href="{% url 'accounts:login' %}">Login</a>
               {% endif %}
               {% block content %}
               {% endblock %}
           </div>
       </body>
       ```
       ```python
       from django.shortcuts import render,redirect
       from django.contrib.auth.forms import AuthenticationForm
       from django.contrib.auth import login as auth_login
       from django.contrib.auth import logout as auth_logout
       from django.views.decorators.http import require_http_methods, require_POST
              
       @require_http_methods(['GET', 'POST'])
       def login(request):	
           if request.user.is_authenticated:	#인증된 사용자가 다시 로그인 못하도록
               return redirect('articles:index')
              	if request.method =='POST':
              		form = AuthenticationForm(request, request.POST) 
              		if form.is_valid():
                       auth_login(request, form.get_user()) 
                       return redirect('articles:index')
              	else:
              		form = AuthenticationForm()	
              	context = {
              		'form': form
              	}
              return render(request, 'accounts/login.html', context)
              
       @require_POST
       def logout(request):
           if request.user.is_authenticated:	#인증된 사용자만 로그아웃할 수 있도록
               auth_logout(request)
               return redirect('articles:index')
       ```
  
2. The login_required decorator
  
     - 사용자가 로그인되어 있지 않으면, **settings.LOGIN_URL**에 설정된 문자열 기반 절대 경로로 redirect함
       - LOGIN_URL의 <u>기본 값은 '/accounts/login/'</u>
       - 두 번째 app 이름을 accounts로 했던 이유 중 하나
     - 사용자가 로그인되어 있으면 정상적으로 view 함수를 실행
     - 인증 성공 시 사용자가 redirect되어야하는 경로는 "next"라는 <u>쿼리 문자열 매개 변수</u>에 저장됨
     - ex) /accounts/login?next=/articles/create/
     
     ```python
     from django.contrib.auth.decorators import login_required
     
     @login_required	#로그인되어있는지. 로그인되어있지 않으면 /accounts/login/으로 redirect
     def create(request):	#로그인되어 있지 않으면 create의 view함수를  호출할 수 없다.
         pass
   ```


### "next" query string parameter

- 로그인이 정상적으로 진행되면 <u>기존에 요청했던 주소로</u> redirect하기 위해 마치 주소를 keep해주는 것
  - next parameter가 있는 현재 url로 요청을 보내야하기 때문에 action을 비워둔다
- 단, 별도로 처리해주지 않으면 우리가 view에 설정한 redirect 경로로 이동하게 됨

```python
from django.shortcuts import render,redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login
from django.views.decorators.http import require_http_methods

@require_http_methods(['GET', 'POST'])
def login(request):	
    if request.user.is_authenticated:	#인증된 사용자가 다시 로그인 못하도록
        return redirect('articles:index')
	if request.method == 'POST':
		form = AuthenticationForm(request, request.POST) 
		if form.is_valid():	
            auth_login(request, form.get_user()) 
           	return redirect(request.GET.get('next')  or 'articles:index')
	else:
		form = AuthenticationForm()	
	context = {
		'form' : form
	}
return render(request, 'accounts/login.html', context)
```

### 두 데코레이터로 인해 발생하는 구조적 문제와 해결

- 비로그인 상태에서 글 삭제 시도(POST) -> redirect로 이동한 로그인 페이지에서 로그인 시도  -> 405(Method Not Allowed) status code 확인
- @require_POST 작성된 함수에 @login_required를 함께 사용하는 경우 에러 **발생**
- 로그인 이후  "next" 매개변수를 따라 해당 함수로 다시 redirect되는데, 이 때 @require_POST 때문에 405 에러가 발생하게 됨
  - next 주소(=articles/1/delete/)에 redirect GET 방식으로 감
- 문제
  1. redirect 과정에서 POST 데이터의 손실
  2. redirect 요청은 POST 방식이 불가능하기 때문에 GET 방식으로 요청됨
- 해결: login_required는 GET method request를 처리할 수 있는 view 함수에서만 사용해야함. 처음에 @require_POST로 method를 확인하고, request.user.is_authenticated로 로그인되었는지 확인



## 회원가입(Create)

### UserCreationForm

- 주어진 username과 password로 권한이 없는 새 user를 생성하는 ModelForm
- 3개의 필드를 가진다.
  1. username(from the user model)
  2. password1
  3. password2(비밀번호 확인용)

```python
#accounts/urls.py
app_name = 'accounts'
urlpatterns = [
    path('signup/', views.signup, name='signup'),
]

#accounts/views.py
from django.contrib.auth.forms import UserCreationForm
from django.views.decorators.http import require_http_methods

@require_http_methods(['GET', 'POST'])
def signup(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()	#회원가입 후 자동로그인
            auth_login(request, user)
            return redirect('articles:index')
    else:
        form = UserCreationForm()
    context = {
        'form' : form,
    }
    return render(request, 'accounts/signup.html', context)
```

```django
<!--accounts/signup.html-->
{% extends 'base.html' %}
{% block content %}
	<h1>회원가입</h1>
	<form action="{% url 'accounts:signup' %}" method="POST">
        {% csrf_token %}
        {{ form.as_p }}
        <input type="submit">
	</form>
{% endblock %}
```



## 회원탈퇴(Delete)

- DB에서 사용자를 삭제하는 것과 같음.

```python
#accounts/urls.py
app_name = 'accounts'
urlpatterns = [
    path('delete/', views.delete, name='delete'),
]

#accounts/views.py
from django.views.decorators.http import require_POST

@require_POST
def delete(request):
    if request.user.is_authenticated:
        request.user.delete()	#회원 탈퇴 후 로그아웃 함수 호출
        auth_logout(request)
    return redirect('articles:index')
```

```django
<!--templates/base.html-->
<form action="{% url 'accounts:delete' %}" method="POST">
      {% csrf_token %}
      <input type="submit" value="회원탈퇴">
</form>
```



## 회원정보 수정(Update)

### UserChangeForm

- 사용자의 정보 및 권한을 변경하기 위해 admin 인터페이스에서 사용되는 ModelForm

#### UserChangeForm 사용 시 문제점

- 일반 사용자가 접근해서는 안될 정보들(fields)까지 모두 수정이 가능해짐
- 따라서 UserChangeForm을 상속받아 CustomUserChangeForm이라는 서브클래스를 작성해 접근 가능한 필드를 조정해야 함

#### get_user_model()

- 현재 프로젝트에서 활성화된 사용자 모델(active user model)을 반환
- Django는 User클래스를 직접 참조하는 대신 django.contrib.auth.get_user_model()을 사용하여 참조해야 한다고 강조

```python
#accounts/urls.py
app_name = 'accounts'
urlpatterns = [
    path('update/', views.update, name='update'),
]

#accounts/views.py
from django.contrib.auth.forms import AuthenticationForm
from django.views.decorators.http import require_http_methods
from .forms import CustomUserChangeForm

def update(request):
    if request.method == "POST":
        form = CustomUserChangeForm(request.POST, instance=request.user)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
    else:
        form = CustomUserChangeForm(instance=request.user)
    context = {
        'form' : form,
    }
    return render(request,'accounts/update.html',context)

#accounts/forms.py
from django.contrib.auth.forms import UserChangeForm
from django.contrib.auth import get_user_model

class CustomUserChangeForm(UserChangeForm):
    class Meta:
        model = get_user_model()	#user 클래스 return
        fields = ('email','first_name','last_name')
        #수정 시 필요한 필드만 선택해서 작성. type: 튜플
```

```django
<!--accounts/update.html-->
{% extends 'base.html' %}
{% block content %}
	<h1>회원정보수정</h1>
	<form action="{% url 'accounts:update' %}" method="POST">
        {% csrf_token %}
        {{ form.as_p }}
        <input type="submit">
	</form>
{% endblock %}
```



## 비밀번호 변경(Update)

### PasswordChangeForm

- 사용자가 비밀번호를 변경할 수 있도록 하는 Form
- 이전 비밀번호를 입력하여 비밀번호를 변경할 수 있도록 함
- 이번 비밀번호를 입력하지 않고 비밀번호를 설정할 수 있는 SetPasswordForm을 상속받는 서브 클래스

```python
#accounts/urls.py
app_name='accounts'
urlpatterns=[
    path('password/', views.change_password, name='change_password'),
]

#accounts/views.py
from django.contrib.auth.forms import PasswordChangeForm
from django.views.decorators.http import require_http_methods
from django.contrib.auth.decorators import login_required

@login_required
@require_http_methods(['GET', 'POST'])
def change_password(request):
    if request.method == "POST":
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
    else:
        form = PasswordChangeForm(request.user)
    context = {
        'form' : form,
    }
    return render(request,'accounts/change_password.html', context)
```

```django
<!--accounts/change_password.html-->
{% extends 'base.html' %}
{% block content %}
	<h1>비밀번호 변경</h1>
	<form action="{% url 'accounts:change_password' %}" method="POST">
        {% csrf_token %}
        {{ form.as_p }}
        <input type="submit">
	</form>
{% endblock %}
```

### 암호 변경 시 세션 무효화 방지

#### update_session_auth_hash(request, user)

- 현재 요청(current request)과 새 session hash가 파생될 업데이트된 사용자 객체를 가져오고, session hash를 적절하게 업데이트
- 비밀번호가 변경되면 기존 세션과의 회원 인증 정보가 일치하지 않게 되어 로그인 상태를 유지할 수 없기 때문
- 암호가 변경되어도 로그아웃되지 않도록 새로운 password hash로 session을 업데이트 함

```python
#accounts/views.py
from django.contrib.auth.forms import PasswordChangeForm, update_session_auth_hash
from django.views.decorators.http import require_http_methods
from django.contrib.auth.decorators import login_required

@login_required
@require_http_methods(['GET', 'POST'])
def change_password(request):
    if request.method == "POST":
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
            form.save()
            update_session_auth_hash(request, form.user)
            return redirect('articles:index')
    else:
        form = PasswordChangeForm(request.user)
    context = {
        'form' : form,
    }
    return render(request,'accounts/change_password.html', context)
```



