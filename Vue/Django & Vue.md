# Django & Vue

## Django

### Server & Client

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

### Start Project Model + Serializer

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

# articles/views.py
...
@api_view(['GET', 'POST'])
def article_list_or_create(request):
	#함수화시켜서 가독성 증가
    def article_list():
        articles = Article.objects.annotate(	# comment 개수 추가
            comment_count=Count('comments', distinct=True),
            like_count=Count('like_users', distinct=True)
        ).order_by('-pk')
        serializer = ArticleListSerializer(articles, many=True)
        return Response(serializer.data)
    
    def create_article():
        serializer = ArticleSerializer(data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save(user=request.user)
            return Response(serializer.data, status=status.HTTP_201_CREATED)

    if request.method == 'GET':
        return article_list()
    elif request.method == 'POST':
        return create_article()
...
       
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



### CORS

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

  

### Authentication & Authorization

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



### DRF Authentication

- 다양한 인증 방식
  1. Session Based
  2. Token Based
     - Basic Token
     - JWT
  3. Oauth
     - google
     - facebook
     - github
     - ...

- Basic Token Authentication(session cookie 방식과 비슷)
  1. client에서 로그인 시도. Server에 username과 password가 담긴 JSON data를 올바르게 보낸다.
  2. table에서 username과 password를 같은지 대조한다. 같다면 새로운 테이블에 user의 id와 token값을 저장한다. 응답으로 token 값을 준다.
  3. client는 받은 token 값을 저장한다. 앞으로 요청을 보낼 때마다 요청 헤더의 Authorization에 'Token <토큰값>'을 보내준다.
  4. server에서는 받은 token 값을 token 테이블에서 확인 후 응답을 보낸다.

- JWT

  > JSON Web Token. JWT.IO allows you to decode, verify and generate JWT.

  - JSON 포맷을 활용하여 요소 간 안전하게 정보를 교환하기 위한 표준 포맷

  - 암호화 알고리즘에 의한 <u>디지털 서명</u>이 되어 있기 떄문에 JWT 자체로 검증 가능

  - JWT 자체가 <u>필요한 정보를 모두 갖기</u> 때문에(self-contained) 이를 검증하기 위한 다른 검증 수단(ex. table)이 필요 없음

  - 사용처: Authentication, Information Exchange

  - 기본 토큰 인증 체계와 달리 JWT 인증 확인은 데이터베이스를 사용하여 토큰의 유효성을 검사할 필요가 없음

    - 즉,  JWT는 데이터베이스에서 유효성 검사가 필요 없음. (JWT 자체가 인증에 필요한 정보를 모두 갖기 때문(self-contained))

      - 이는 세션 혹은 기본 토큰을 기반으로 한 인증과의 핵심 차이점

    - 토큰 탈취(오염)시 서버 측에서 토큰 무효화가 불가능(블랙리스팅 테이블 활용)

      - 매우 짧은 유효기간(5min)과 Refresh 토큰을 활용하여 구현. (복잡도 증가)
      - MSA(Micrio Server Architecture) 구조에서 서버간 인증에 활용

      cf. Basic Token Authentication에서는 테이블에서 탈취된 토큰만 지우면 된다. 의미가 없어짐

    - One Source(JWT) Multi Use 가능

      - 하나의 인증으로 여러 API Server에서 알아볼 수 있다.

- dj-rest-auth & django-allauth 라이브러리

  ```bash
  $ pip install django-allauth	#로그인/로그아웃/검증
  $ pip install dj-rest-auth		#회원가입 기능
  ```

  ```python
  #settings.py
  INSTALLED_APPS = [
      ...
      'rest_framework.authtoken',	#token 기반 auth
      
      #DRF auth
      'dj_rest_auth',	#signup 제외 auth 관련 담당
      'dj_rest_auth.registration',  #signup 담당
  	
      #signup 담당을 위해 필요 
      'allauth', 	#확장하면 소셜 로그인까지 확장 가능
      'allauth.account',
      'allauth.socialaccount',
      ...
      'django.contrib.sites',  # dj-rest-auth signup 필요
      ...
  ]
  
  SITE_ID = 1
  ...
  REST_FRAMEWORK = {	#DRF 인증 관련 설정
      'DEFAULT_AUTHENTICATION_CLASSES': [
          'rest_framework.authentication.TokenAuthentication',
      ],
      'DEFAULT_PERMISSION_CLASSES': [
          #'rest_framework.permissions.AllowAny', 	#모두에게 허용
  
          #인증된 사용자만 모든일이 가능 / 비인증 사용자는 모두 401 Unauthorized
          #view함수에 @login_required 일괄처리. (signup, login은 제외)
          'rest_framework.permissions.IsAuthenticated'
      ]
  }
  #migrate 필요
  
  #pjt/urls.py
  from django.contrib import admin
  from django.urls import path, include
  
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('api/v1/articles/', include('articles.urls')),
      path('api/v1/accounts/', include('accounts.urls')),
      path('api/v1/accounts/', include('dj_rest_auth.urls')),	#위에서 찾는 것이 없으면 여기로 옴
      path('api/v1/accounts/signup/', include('dj_rest_auth.registration.urls')),
  ]
  ```

  - 토큰 값이 오지 않으면 로그인/로그아웃 상태로 전환이 불가능하다
    - 로그인 = 토큰 발생 = authtoken 테이블에 create하는 작업
    - 로그아웃 =  토큰 삭제 = authtoken 테이블에 delete하는 작업
    - authentication = 토큰 검증 = authtoken 테이블에 read하는(비교하는) 작업

  ```python
  #accounts/serializers.py
  from rest_framework import serializers
  from django.contrib.auth import get_user_model
  from articles.models import Article
  
  class ProfileSerializer(serializers.ModelSerializer):
  
      class ArticleSerializer(serializers.ModelSerializer):
          #아래에서 pk값만 받지 않고 한번에 다른 자세한 내용(fields)도 받을 수 있게 한다
          class Meta:
              model = Article
              fields = ('pk', 'title', 'content')	
  
      like_articles = ArticleSerializer(many=True)
      articles = ArticleSerializer(many=True)
  
      class Meta:
          model = get_user_model()
          fields = ('pk', 'username', 'email', 'like_articles', 'articles',)
  
  #accounts/urls.py
  from django.urls import path
  from . import views
  
  app_name = 'accounts'
  
  urlpatterns = [
      path('profile/<username>/', views.profile),
  ]
  
  #accounts/views.py
  from django.shortcuts import get_object_or_404
  from django.contrib.auth import get_user_model
  
  from rest_framework.decorators import api_view
  from rest_framework.response import Response
  
  from .serializers import ProfileSerializer
  
  User = get_user_model()
  
  @api_view(['GET'])
  def profile(request, username):
      user = get_object_or_404(User, username=username)
      serializer = ProfileSerializer(user)
      return Response(serializer.data)
  ```

  

## Vue

```js
//@/api/drf.js
const HOST = 'http://localhost:8000/api/v1/'

const ACCOUNTS = 'accounts/'
const ARTICLES = 'articles/'
const COMMENTS = 'comments/'

export default {
  accounts: {
    login: () => HOST + ACCOUNTS + 'login/',	
    //http://localhost:8000/api/v1//accounts/login/
    logout: () => HOST + ACCOUNTS + 'logout/',
    signup: () => HOST + ACCOUNTS + 'signup/',
    // Token 으로 현재 user 판단
    currentUserInfo: () => HOST + ACCOUNTS + 'user/',
    // username으로 프로필 제공
    profile: username => HOST + ACCOUNTS + 'profile/' + username,
  },
  articles: {
    articles: () => HOST + ARTICLES,
    article: articlePk => HOST + ARTICLES + `${articlePk}/`,
    likeArticle: articlePk => HOST + ARTICLES + `${articlePk}/` + 'like/',
    comments: articlePk => HOST + ARTICLES + `${articlePk}/` + COMMENTS,
    comment: (articlePk, commentPk) =>
      HOST + ARTICLES + `${articlePk}/` + COMMENTS + `${commentPk}/`,
  },
}
```

### Vue router

#### 404 page

- 404 Not Found 시나리오

  1. Vue Router에 등록되지 않은 routes인 경우 ex. /no-such-routes

     ```js
     import Vue from 'vue'
     import VueRouter from 'vue-router'
     // import store from '../store'
     //components는 부품, Views는 url과 매핑
     import LoginView from '@/views/LoginView.vue'
     import ProfileView from '@/views/ProfileView.vue'
     import ArticleListView from '@/views/ArticleListView.vue'
     import NotFound404 from '../views/NotFound404.vue'
     
     Vue.use(VueRouter)
     
     const routes = [	
       {
         path: '/login',
         name: 'login',
         component: LoginView
       },
       	...
       {
         path: '/profile/:username',  //username은 변수
         name: 'profile',
         component: ProfileView,
       },
       {
         path: '/',  	//Home
         name: 'articles',
         component: ArticleListView
       },
     	...
       {
         path: '/404',
         name: 'NotFound404',
         component: NotFound404
       },
       {
         path: '*',	//위에 있는 것 제외한 나머지를 쓰면 404로 간다
         redirect: '/404'
       },
     ]
     ```

     - vue router는 routes 배열에서 순차적으로 URL을 검색
     - 등록되지 않은 모든(*) URL은 /404로 redirection
     - 브라우저에서 NotFound404 컴포넌트 확인

  2. Vue Router에는 등록되어 있지만, 서버에서 해당 리소스를 찾을 수 없는 경우 ex. /articles/455

     ```js
     //SFC(.vue)
     ...
     axios.get(URL)
     	.then(res => {
         ...
     	})
     	.catch(err => {
             console.error(err.response)
             if (err.response.status === 404) {
                 this.$router.push({ name: 'NotFound404'})
             }
         })
     
     //Vuex
     import router from '@/router'
     ...
     axios.get(URL)
     	.then(res => {
         ...
     	})
     	.catch(err => {
             console.error(err.response)
             if (err.response.status === 404) {
                 router.push({ name: 'NotFound404'})
             }
         })
     ```

#### Navigation Guard

- 전역 가드(Global Before Guards)

  ```js
  //@/router/index.js
  const routes = [ ... ]
                  
  const router = new VueRouter({
  	mode: 'history',
      base: process.env.BASE_URL,
      routes
  })
  /*
  router.beforeEach((to, from, next) => {
  	// '/' => '/articles/1'
  })
  */
  /*
  Navigation Guard 설정  (이전 페이지에서 있던 에러 메시지 삭제)
    로그인(Authentication)이 필요 없는 route 이름들 저장(/login, /signup)
    0. router 에서 이동 감지
    1. 현재 이동하고자 하는 페이지가 로그인이 필요한지 확인  
    2. 로그인이 필요한 페이지인데 로그인이 되어있지 않다면 로그인 페이지(/login)로 이동
    3. 로그인이 되어 있다면 원래 이동할 곳으로 이동  
    4. 로그인이 되어있는데 /login, /signup 페이지로 이동한다면 메인 페이지(/)로 이동
  */
  ```

  1. URL을 이동할 때마다, 이동하기 전 모든 경우에 발생
  2. router 객체의 메서드로, 콜백 함수를 인자로 받고 해당 콜백 함수는 3개의 인자를 받음
     1. to: 이동하려는 route의 정보를 담은 객체
     2. from: 직전 route의 정보를 담은 객체
     3. next: 실제 route의 이동을 조작하는 함수
  3. 반드시 마지막에 next()로 route 이동을 실행해야 함

### Vuex

#### Vuex modules

- Module 분리
  1. 단일 파일(@/store/index.js)에 모든 state, getters, mutations, actions를 작성할 경우, App이 커질수록 파일의 크기가 너무 커짐
  2. 기능에 따라 state, getters, mutations, actions를 모듈(파일)로 분리하여 사용

#### namespace

- Module의 이름공간(module space)

  ```js
  //@/store/index.js
  import Vue from 'vue'
  import Vuex from 'vuex'
  
  import articles from './modules/articles'
  import accounts from './modules/accounts'
  
  Vue.use(Vuex)
  
  export default new Vuex.Store({
    modules: { accounts, articles },
  })
  ```

  1. 다른 module에 작성되어 있어도, 실제로는 global namespace에 등록됨
  2. 만약 확실하게 모듈별로 구분하고 싶다면, namespaced: true 옵션을 사용