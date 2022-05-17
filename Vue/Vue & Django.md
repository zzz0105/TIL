# Vue & Django

## Server & Client

- Server: 정보제공

  > DB와 통신하며 데이터를 CRUD
  >
  > 요청을 보낸 Client에게 이러한 정보를 응답

  - 클라이언트에게 '정보', '서비스'를 제공하는 컴퓨터 시스템
  - 정보 & 서비스
    - Django를 통해 응답한 template(HTML)
    - DRF를 통해 응답한 JSON

- Client: 정보 요청 & 표현

  > Server에게 정보(데이터) 요청
  >
  > 응답 받은 정보를 잘 가공하여 화면에 보여줌

  - 서버에게 그 서버가 맡는(서버가 제공하는) 서비스를 요청하고, **서비스 요청**을 위해 필요한 인자를 **서버가 요구하는 방식에 맞게 제공**하며, 서버로부터 반환되는 응답을 **사용자에게 적절한 방식으로 표현**하는 기능을 가진 시스템
  - ex. 브라우저, Postman 등
    - Client(Postman)가 서버에 올바른 요청을 제공하면, Server(Django rest framework)에서 Json으로 응답

## Start Project Model + Serializer

```bash
$ python -m venv venv
$ source venv/Scripts/activate
$ pip install django djangorestframework
$ pip freeze > requirements.txt
$ django-admin startproject pjt .
$ touch .gitignore	#django, venv, visualstudiocode, python
$ python manage,py startapp accounts
$ python manage,py startapp articles	
```

```python
#settings.py
INSTALLED_APPS=[
    'accounts',
    'articles',
    'rest_framework'
    ...
]
...
AUTH_USER_MODEL = 'accounts.User'
```

```python
#accounts/models.py
from django.db import models
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    pass


#articles/models.py
from django.db import models
from django.conf import settings

class Article(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='articles')
    title = models.CharField(max_length=100)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    like_users = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='like_articles')

class Comment(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='comments')
    article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
    content = models.CharField(max_length=200)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    
#pjt/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/v1/articles/', include('articles.urls')),
    path('api/v1/accounts/', include('accounts.urls')),
    path('api/v1/accounts/', include('dj_rest_auth.urls')),
    path('api/v1/accounts/signup/', include('dj_rest_auth.registration.urls')),
]


#accounts/urls.py
from django.urls import path
from . import views

app_name = 'accounts'

urlpatterns = [
    path('profile/<username>/', views.profile),
]


#articles/urls.py
from django.urls import path
from . import views

app_name = 'articles'

urlpatterns = [
    # articles
    path('', views.article_list_or_create),
    path('<int:article_pk>/', views.article_detail_or_update_or_delete),
    path('<int:article_pk>/like/', views.like_article),
    # comments
    path('<int:article_pk>/comments/', views.create_comment),
    path('<int:article_pk>/comments/<int:comment_pk>/', views.comment_update_or_delete)
]
```

```bash
$ python manage.py makemigrations
$ python manage.py migrate
$ python manage.py createsuperuser	#관리자계정 만들기
```

```python
#serializers.py 양이 너무 많으니 serializers 폴더에 나눠서 만든다
#articles/serializers/article.py
from rest_framework import serializers
from django.contrib.auth import get_user_model

from ..models import Article	#이 위치에서 models.py를 접근해야함 -> ..
from .comment import CommentSerializer

User = get_user_model()

class ArticleSerializer(serializers.ModelSerializer):
    
    class UserSerializer(serializers.ModelSerializer):	#user를 추가로 serialize.
        class Meta:
            model = User
            fields = ('pk', 'username')	

    comments = CommentSerializer(many=True, read_only=True)
    user = UserSerializer(read_only=True)
    like_users = UserSerializer(read_only=True, many=True)

    class Meta:
        model = Article
        fields = ('pk', 'user', 'title', 'content', 'comments', 'like_users')	#어떤 항목이 나갈지

# Article List Read
class ArticleListSerializer(serializers.ModelSerializer):
    class UserSerializer(serializers.ModelSerializer):
        class Meta:
            model = User
            fields = ('pk', 'username')

    user = UserSerializer(read_only=True)
    # queryset annotate (views에서 채워주기)
    comment_count = serializers.IntegerField()
    like_count = serializers.IntegerField()

    class Meta:
        model = Article
        fields = ('pk', 'user', 'title', 'comment_count', 'like_count')

#articles/serializers/comment.py
from rest_framework import serializers
from django.contrib.auth import get_user_model
from ..models import Comment

User = get_user_model()

# CUD => validation		/		R => Data serializing
class CommentSerializer(serializers.ModelSerializer):
    
    class UserSerializer(serializers.ModelSerializer):
        class Meta:
            model = User
            fields = ('pk', 'username')

    user = UserSerializer(read_only=True)

    class Meta:
        model = Comment
        fields = ('pk', 'user', 'content', 'article',)
        read_only_fields = ('article', )	#어떤 게시글에 이 댓글이 달려있는지
```



## CORS

- SOP(: Same-Origin Policy)

  > 동일 출처 정책

  - <u>특정 출처(origin. 내 문서의 URL)에서 불러온 문서나 스크립트</u>가 다른 출처에서 가져온 리소스와 상호작용하는 것을 <u>제한</u>하는 보안 방식
  - 잠재적으로 해로울 수 있는 문서를 분리함으로써 공격받을 수 있는 경로를 줄임

- Origin(출처)

  - 두 URL의 Protocol, Port, Host가 모두 같아야 동일한 출처라 할 수 있음

  - 예시

    - http://localhost:3000/post/3

      - http: Scheme/Protocol
      - localhost: Host
      - 3000: Port
      - post/3: Path

      Scheme/Protocol,Host,Port가 모두 같아야 Same origin!

    - 경로(path)만 다름(동일출처) => 성공

    - 프로토콜/포트/호스트 다름 => 실패

- CORS(: Cross-Origin Resoucr Sharing)

  > 교차 출처 리소스 공유

  - **추가 HTTP header를 사용**하여, 특정 출처에서 실행중인 웹 애플리케이션이 **다른 출처의 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제**
  - 리소스가 자신의 출처와 다를 때 교차 출처 HTTP 요청을 실행
  - 보안 상의 이유로 브라우저는 교차 출처 HTTP 요청을 제한(SOP)
    - 예를 들어 XMLHttpRequest는 SOP를 따름
  - 다른 출처의 리소스를 불러오려면 그 출처에서 **올바른 CORS header를 포함한 응답을 반환**해야 함(= server request의 헤더에 추가해서 보내면 client가 막지 않는다)

- CORS Policy

  - 교차 출처 리소스 공유 정책
  - 다른 출처에서 온 리소스를 고유하는 것에 대한 정책
  - SOP와 반대

  (cf. POSTMAN의 경우 브라우저가 아니라서 정책에 대한 내용이 없다.)

- 교차 출처 접근 허용하기

  - CORS를 사용해 교차 출처 접근을 허용하기
  - CORS를 HTTP의 일부로, 어떤 호스트에서 자신의 컨텐츠를 불러갈 수 있는지 **서버에 지정할 수 있는 방법**

- Why CORS?

  1. 브라우저 & 웹 애플리케이션 보호
     - 악의적인 사이트의 데이터를 가져오지 않도록 사전 차단
     - 응답으로 받는 자원에 대한 최소한의 검증
     - 서버는 정상적으로 응답하지만 브라우저에서 차단
  2. Server의 자원 관리
     - 누가 해당 리소스에 접근할 수 있는지 관리 가능

- How CORS?

  - CORS 표준에 의해 추가된 **HTTP Header**를 통해 이를 통제
  - CORS HTTP 응답 헤더 예시
    - Access-Control-Allow-Origin~~/Access-Control-Allow-Credentials/Access-Control-Allow-Headers/Access-Control-Allow-Methods~~

- Access-Control-Allow-Origin 응답 헤더

  - 이 응답이 주어진 출처로부터 요청 코드와 공유될 수 있는지를 나타냄
  - 예시
    - Access-Control-Allow-Origin: *
    - 브라우저 리소스에 접근하는 임의의 origin으로부터 요청을 허용한다고 알리는 응답에 포함
    - *: 모든 도메인에서 접근할 수 있음을 의미(와일드카드)
    - \* 외에 특정 origin 하나를 명시할 수 있음

- CORS 시나리오

  1. https://localhost:8080 (Vue.js)의 웹 컨텐츠가 https://github.com (Django)의 도메인의 컨텐츠를 호출하기를 원함
  2. 요청 헤더의 Origin을 보면 localhost:8080으로부터 요청이 왔다는 것을 알 수 있음
  3. 서버는 이에 대한 응답으로 Access-Control-Allow-Origin 헤더를 다시 전송
     - 서버는 CORS Policy와 직접적인 연관이 없고 그저 요청에 응답
  4. 만약 서버 리소스 소유자가 오직 localhost:8080의 요청에 대해서만 리소스에 대한 접근을 허용하려는 경우 *가 아닌 Access-Control-Allow-Origin: localhost:8080을 전송해야 함

- django-cors-headers 라이브러리

  - 응답에 CORS header를 추가해주는 라이브러리
  - 다른 출처에서 보내는 Django 애플리케이션에 대한 브라우저 내 요청을 허용함
  - DJango App이 header 정보에 CORS를 설정한 상태로 응답을 줄 수 있게 해주며, 이 설정을 통해 브라우저는 다른 origin에서 요청을 보내는 것이 가능해짐

  ```bash
  $ pip install django-cors-headers
  ```

  ```python
  #settings.py
  INSTALLED_APPS = [
      ...,
      'corsheaders',
      ...
  ]
  
  MIDDLEWARE = [
      ...
      'corsheaders.middleware.CorsMiddleware',	#CommonMiddleware보다 위에 위치(위에 있을수록 좋음)
      ...
      'django.middleware.common.CommonMiddleware'
  ]
  
  CORS_ALLOWED_ORIGINS = [		#교차 출처 자원 공유 허용할 Domain 등록
      'http://localhost:8080'		#Vue local host
  ]
  
  CORS_ALLOW_ALL_ORIGINS = True	#모두에게 교차 출처 허용
  ```

  

## Authentication & Authorization

- Authentication

  > 인증, 입증. 자신이라고 주장하는 사용자가 **누구인지 확인**하는 행위.

  - 모든 보안 프로세스의 첫 번째 단계(가장 기본 요소)
  - 즉, 내가 누구인지를 확인하는 과정
    - Credentials(비밀번호, 얼굴인식) 검증
  - Django의 게시판 서비스 로그인
  - 인증 이후에 횐득하는 권한: 생성, 수정, 삭제
  - 401 Unauthorized
    - 비록 HTTP 표준에서는 "미승인(unauthorized)"을 하고 있지만, 의미상 이 응답은 "비인증(unauthenticated)"을 의미

- Authorization

  > 권한 부여, 허가. 사용자에게 특정 리소스 또는 기능에 대한 **액세스 권한을 부여**하는 과정(절차)

  - 유저가 자원에 접근할 수 있는지 여부 확인. 규칙/규정에 의해 접근할 수 있는지 확인
  - 보안 환경에서 권한 부여는 항상 인증을 따라야 함
    - 예를 들어, 사용자는 조직에 대한 액세스 권한을 부여 받기 전에 먼저 자신의 ID가 진짜인지 먼저 확인해야 함
  - 서류의 등급, 웹 페이지에서 글을 조회&삭제&수정할 수 있는 방법, 제한 구역
    - <u>인증이 되었어도 모든 권한을 부여 받는 것은 아님</u>
  - Django의 일반유저 vs 관리자 유저
  - 인증 이후에 부여되는 권한: 로그인 후 글 작성 여부
  - 403 Forbidden
    - 401과 다른 점은 서버는 클라이언트가 누구인지 알고 있음

- Authentication and authorization work together

  - 회원 가입을 하고 로그인을 하면 할 수 있는 권한 생성
    - 인증 이후에 권한인 따라오는 경우가 많음
  - 단, 모든 인증을 거쳐도 권한이 동일하게 부여되는 것은 아님
    - Django에서 로그인을 했더라도(인증) 다른 사람의 글까지 수정/삭제가 가능하진 않음(권한)
  - 세션, 토큰, 제 3자를 활용하는 등의 다양한 인증 방식이 존재