# Model Relationship

## Foriegn Key

- 외래 키(외부 키)
- 관계형 데이터베이스에서 <u>한 테이블의 필드</u>(참조함) 중 다른 테이블의 **행**(참조됨)을 <u>식별</u>할 수  있는 키
- 참조하는 테이블에서 속성(필드)에 해당하고, 이는 참조되는 테이블의 <u>기본 키(Primary Key)를 가리킴</u>
- 참조하는 테이블의 외래 키는 참조되는 테이블 <u>행 1개에 대응</u>됨
  
  - 이 때문에 참조한느 테이블에서 참조되는 테이블의 존재하지 않는 행을 참조할 수 없음
- 참조하는 테이블의 행 여러 개가 참조되는 테이블의 동일한 행을 참조할 수 있음
- 게시글(Article)과 댓글(Comment)간의 모델 관계 설정
  - Article **1 : N** Comment
  - Comment의 FK가 Article의 PK(id) 참조함
- Foreign Key 특징
  - 키를 사용하여 부모 테이블(참조됨)의 유일한 값을 참조(참조 무결성)
    - **[참고]** 참조 무결성
      - 데이터베이스 관계 모델에서 관려된 2개의 테이블 간의 **일관성**을 말함
      - 외래키가 선언된 테이블의 외래 키 속성(열)의 값은 그 테이블의 부모가 되는 테이블의 <u>기본 키 값으로 존재</u>해야 함
  - 외래 키의 값이 반드시 부모 테이블의 <u>기본 키일 필요는 없지만</u> **유일한 값**이어야 함 => 완벽하게 보장할 수 있는 것은 PK!

- ForeignKey field

  - A many-to-one relationship

  - 2개의 위치 인자가 반드시 필요

    1. 참조하는 model class
    2. on_delete 욥션
       - <u>외래 키가 참조하는 객체가 사라졌을 때</u> **외래 키를 가진 객체를 어떻게 처리할 지**를 정의
       - Database Integrity(데이터 무결성)을 위해서 매우 중요한 설정
         - **[참고]** 데이터 무결성
           - 데이터의 정확성과 일관성을 유지하고 보증하는 것을 가리키며, 데이터베이스나 RDBMS 시스템의 중요한 기느
           - 무결성 제한의 유형
             1. 개체 무결성(Entity integrity)
                - PK의 개념과 관련
                - 모든 테이블이 PK를 가져야 하며 PK로 선택된 열은 고유한 값이어야 하고 빈 값은 허용치 않음을 규정
             2. <u>참조 무결성(Referential integrity)</u>
                - FK(외래 키) 개념과 관련
                - FK 값이 데이터베이스의 특정 테이블의 PK 값을 참조하는 것
             3. 범위(도메인) 무결성(Domain itegrity)
                - 정의된 형식(범위)에서 관계형 데이터베이스의 모든 칼럼이 선언되도록 규정
       - on-delete 옵션에 사용가능한 값들
         - CASCADE: 부모 객체(참조된 객체)가 삭제 됐을 때 이를 참조하는 객체도 삭제
         - PROTECT, SET_NULL, SET_DEFAULT, SET(), DO_NOTHING, RESTRICT

  - migrate 작업 시 필드 이름에 _id를 추가하여 데이터베이스 열 이름을 만듬

  - **[참고]** 재귀관계(자신과 1:N)

    ```sqlite
    models.ForeignKey('self', on_delete=models.CASCADE)
    ```

  - comment 모델 정의하기

    ```python
    #articles/models.py
    from django.db import models
    
    class Comment(models.Model):
        article = models.ForeignKey(Article, on_delete=models.CASCADE)
        #1:N 관계에서 1을 참조하는 것이므로 소문자 단수형으로 쓴다.
        #article_id로 만들어진다. Django가 자동으로 붙여줌
        #cf. migration 파일에서는 외래키가 가장 밑에 있다
        content = models.CharField(max_length=200)
        created_at = models.DateTimeField(auto_now_add=True)
        updated_at = models.DateTimeField(auto_now=True)
        
        def __str__(self):
            return self.content
    ```

  - Migration

    ```bash
    $ python manage.py makemigrations	#migration 파일 확인
    ```

- 데이터베이스의 ForeignKey 표현

  - 만약 ForeignKey 인스턴스를 abcd로 생성했다면 abcd_id로 만들어짐
  - 하지만 명시적인 모델 관계 파악을 위해 참조하는 클래스 이름의 소문자(단수형)로 작성하는 것이 바람직함(1:N)

- 댓글 생성 해보기

  ```bash
  $ pyhon manage.py shell_plus
  ```

  ```sqlite
  comment = Comment()
  comment.content ='first comment'
  comment.save()			--articles_comment 테이블의 ForeignKeyField, article_id값 누락되어서 에러 발생
  ------
  article = Ariticle.objects.create(title='title', content='content')
  article = Ariticle.object.get(pk=1)	
  article					--<Article:title>
  comment.article = article
  comment.save()
  comment					--<comment: first comment>
  comment.pk				--1
  comment.content			--'first comment'
  comment.article_id		--1 // article_pk로는 값을 접근할 수 없다
  comment.article 		--<Article: title> 
  comment.article.pk		--1
  comment.article.content	--'content'
  ```

- admin site에서 작성된 댓글 확인

  ```python
  #articles/admin.py
  from .models import Article, Comment
  
  admin.site.register(Comment)
  ```

  ```bash
  $ python manage.py createsuperuser
  ```

- 1:N 관계 `related manager`

  - 역참조('comment_set')

    - Article(1) -> Comment(N)
    - article.comment 형태로는 사용할 수 없고, **article.comment_set** manager가 생성됨
    - 게시글에 몇 개의 댓글이 작성되었는지 Django ORM이 보장할 수 없기 때문
      - article은 comment가 있을수도 있고, 없을 수도 있음
      - 실제로 Article 클래스에는 Comment 외의 어떠한 관계도 작성되어 있지 않음

  - 참조('article')

    - Comment(N)  -> Article(1)
    - 댓글의 경우 어떠한 댓글이든 반드시 자신이 참조하고 있는  게시글이 있으므로, comment.article과 같이 접근할 수 있음
    - 실제 ForeignKeyField 또한 Comment 클래스에서 작성됨

  - 연습하기

    - dir() 함수를 통해 article 인스턴스가 사용할 수 있는 모든 속성, 메서드를 직접 확인하기

      ```sqlite
      dir(article)
      ```

    - article의 입장에서 모든 댓글 조회하기(역참조)

      ```sqlite
      article.comment_set.all()
      ```

    - 조회한 모든 댓글 출력하기

      ```sqlite
      comments = article.comment_set.all()
      for comment in comments:
      	print(comment.content)	--first comment
      ```

    -  comment의 입장에서 참조하는 게시글 조회하기(참조)

      ```sqlite
      comment = Comment.objects.get(pk=1)
      comment.article				--<Article: title>
      comment.article.content		--'content'
      comment.article_id			--1
      ```

- ForiegnKey arguments - 'related_name'

  - 역참조 시 사용할 이름('model_set' manager)을 변경할 수 있는 옵션

    ```python
    # articles/models.py
    from django.db import models
    
    class Comment(models.Model):
      article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
    ```

  - 위와 같이 변경하면 <u>article.comment_set은 더이상 사용할 수 없고</u>, **article.comments**로 대체됨
  
  - **[주의]** 역참조 시 사용할 이름 수정 후, <u>migration</u> 과정 필요                                                



### Comment Create

- CommentForm 작성

  ```python
  #articles/forms.py
  from django import forms
  from .models import Article, Comment
  
  class CommentForm(forms.ModelForm):
      class Meta:
          model = Comment
          fields = '__all__'
  ```

- detail 페이지에서 CommentForm 출력

  ```python
  #articles/views.py
  from .forms import ArticleForm, CommentForm
  
  def detail(request, pk):
      article = get_object_or_404(Article,pk=pk)
      comment_form = CommentForm()
      context={
          'article' : article,
          'comment_form' : comment_form
      }
      return render(request, 'articles/detail.html', context)
  ```

  ```django
  <!-- articles/detail.html -->
  {% extends 'base.html' %}
  {% block content %}
  <a href="{% url 'articles:index' %}">back</a>
  <hr>
  <form action="" method="POST">
      {% csrf_token %}
      {{ comment_form }}
      <input type="submit">
  </form>
  ```

  - ForeignKeyField를 작성자가 직접 입력하는 상황이 발생

  - CommentForm에서 외래 키 필드 출력 제외

    ```python
    #articles/forms.py
    class CommentForm(forms.ModelForm):
        class Meta:
            model = Comment
            exclude = ('article',)
    ```

- 댓글 작성 로직

  ```python
  #articles/urls.py
  app_name = 'articles'
  urlpatterns = [
      path('<int:pk>/comments/', views.comments_create, name='comments_create')
  ]
  
  #articles/views.py
  from django.shortcuts import get_object_or_404, redirect
  from django.views.decorators.http import require_POST
  from .forms import CommentForm
  
  @require_POST
  def comments_create(request, pk):
      article = get_object_or_404(Article, pk=pk)
      comment_form = CommentForm(request.POST)
      if comment_form.is_valid():
          comment = comment_form.save(commit=False)
          comment.article = article
          comment.save()
      return redirect('articles:detail', article.pk)
  ```

  ```django
  <!-- articles/detail.html -->
  <form action="{% url 'articles:comments_create' article.pk %}" method="POST">
      {% csrf_token %}
      {{ comment_form }}
      <input type="submit">
  </form>
  ```

- The '**save()**' method
  
  - save(<u>commit=False</u>)
    - Create, but don't save the new instance.
    - 아직 데이터베이스에 저장되지 않은 인스턴스를 반환
    - 저장하기 전에 객체에 대한 사용자 지정 처리를 수행할 때 유용하게 사용



### Comment Read

- 댓글 출력

  - 특정 article에 있는 모든 댓글을 가져온 후 context에 추가

    ```python
    #articles/views.py
    from .models import Article, Comment
    from .forms import CommentForm
    
    def detail(request, pk):
        article = get_object_or_404(Article, pk=pk)
        comment_form = CommentForm()
        comments = article.comment_set.all()
        context = {
            'article' : article,
            'comment_form' : comment_form,
            'comments' : comments
        }
        return render(request, 'articles/detail.html', context)
    ```
  
- detail 페이지에서 댓글 출력
  
    ```django
    <!-- articles/detail.html -->
    {% extends 'base.html' %}
    {% block content %}
    <a href="{% url 'articles:index' %}">back</a>
    <hr>
    <h4>댓글 목록</h4>
    <ul>
        {% for comment in comments %}	<!-- comments = article.comment_set.all() -->
        	<li>{{ comment.content }}</li>
        {% endfor %}
    </ul>
    {% endfor %}
  ```
  
    

### Comment Delete

- 댓글 삭제 후 detail page에서 댓글 삭제 확인

  ```python
  #articles/urls.py
  from django.urls import path
  from . import views
  
  app_name = 'articles'
  urlpatterns=[
      path('<int:article.pk>/comments/<int:comment_pk>/delete/', views.comments_delete, name='comments_delete')
  ]
  
  #articles/views.py
  from django.shortcuts import get_object_or_404, redirect
  from django.views.decorators.http import require_POST
  from .models import Comment
  
  @require_POST
  def comments_delete(request, article_pk, comment_pk):
      comment = get_object_or_404(Comment, pk=comment_pk)
      comment.delete()
      return redirect('articles:detail', article_pk)
  ```

  ```django
  <!-- articles/detail.html -->
  {% extends 'base.html' %}
  {% block content %}
  
  <h4>댓글 목록</h4>
      <ul>
          {% for comment in comments %}
              <li>
                  {{ comment.content }}
                  <form action="{% url 'articles:comments_delete' article.pk comment.pk %}" method="POST" class='d-inline'>
                      {% csrf_token %}
                      <input type="submit" value="DELETE">
                  </form>
              </li>    	
          {% endfor %}
      </ul>
  {% endblock %}
  ```

- 인증된 사용자의 경우만 댓글 작성 및  삭제

  ```python
  #articles/views.py
  from django.shortcuts import get_object_or_404, redirect
  from django.views.decorators.http import require_POST
  from .models import Article, Comment
  from .forms import CommentForm
  
  @require_POST
  def comments_create(request, pk):
      if request.user.is_authenticated:
          article = get_object_or_404(Article, pk=pk)
          comment_form = CommentForm(request.POST)
          if comment_form.is_valid():
              comment = comment_form.save(commit=False)
              comment.article = article
              comment.save()
          return redirect('articles:detail', article.pk)
      return redirect('accounts:login')
  
  @require_POST
  def comments_delete(request, article_pk, comment_pk):
      if request.user.is_authenticated:
          comment = get_object_or_404(Comment, pk=comment_pk)
          comment.delete()
      return redirect('articles:detail', article_pk)
  ```



### Comment 추가사항

- 댓글 개수 출력하기

  ```django
  {% comment %}
  1. {{ comments|length }}
  2. {{ article.comment_set.all|ength }}
  3. {{ comments.count }}
  {% endcomment %}
  <!-- articles/detail.html -->
  <h4>댓글 목록</h4>
  {% if comments %}
  	<p><b>{{ comments|length }}개의 댓글이 있습니다.</b></p>
  {% endif %}
  ```

- 댓글이 없는 경우 대체 컨텐츠 출력(DTL의 for-empty 태그 활용)

  ```django
  <!-- articles/detail.html -->
  <ul>
      {% for comment in comments %}
      <li>
          {{ comment.content }}
          <form action="{% url 'articles:comments_delete' article.pk comment.pk %}" method="POST" class='d-inline'>
              {% csrf_token %}
              <input type="submit" value="DELETE">
          </form>
      </li>  
      {% empty %}
      	<p>댓글이 없어요</p>
      {% endfor %}
  </ul>
  ```

  

## Customizing authentication in Django

### Substituting a custom User model

- User 모델 대체하기

  - 일부 프로젝트에서는 Django의 **내장 User 모델이 제공하는 인증 요구사항이 적절하지 않을 수 있음**
    - ex) username 대신 email을 식별 토큰으로 사용하는 것이 더 적합한 사이트
  - Django는 User를 참조하는데 사용하는 AUTH_USER_MODEL 값을 제공하여, default user model을 **재정의(override)**할 수 있도록 함
  - Django는 새 프로젝트를 시작하는 경우 기본 사용자 모델이 충분하더라도, **커스텀 유저 모델을 설정하는 것을 강력하게 권장**
    - **단, 프로젝트의 모든 migrations 혹은 첫 migrate를 실행하기 전에 이 작업을 마쳐야 함**

- AUTH_USER_MODEL

  - USER를 나타내는데 사용하는 모델
  - 프로젝트가 **진행되는 동안 변경할 수 없음**
  - 프로젝트 시작 시 설정하기 위한 것이며, 참조하는 모델은 첫번째 마이그레이션에서 사용할 수 있어야 함
  - 기본 값: 'auth.User' (auth 앱의 User 모델)
  - **[참고]**  프로젝트 중간에 AUTH_USER_MODEL변경하기
    - 모델 관계에 영향을 미치기 때문에 훨씬 더 어려운 작업이 필요
    - 즉, 중간 변경은 권장하지 않으므로 초기에 설정하는 것을 권장

- Custom User 모델 정의하기

  1. 관리자 권한과 함께 완전한 기능을 갖춘 User 모델을 구현하는 기본 클래스인 AbstractUser를 상속받아 새로운 User 모델 작성

     ```python
     #accounts/models.py
     from django.contrib.auth.models import AbstractUser
     
     class User(AbstractUser):
         pass
     ```

  2. 기존에 Django가 사용하는 User 모델이었던 auth 앱의 User 모델을 accounts 앱의 User 모델을 사용하도록 변경 

     - 변경하지 않을 시 Reverse accessor for 'accounts.User.group' clashes with reverse accessor for 'auth.User.groups'  Error 발생

     ```python
     #settings.py
     AUTH_USER_MODEL = 'accounts.User'
     ```

  3. admin site에 Custom User 모델 등록

     ```python
     #accounts/admin.py
     from django.contrib import admin
     from django.contrib.auth.admin import UserAdmin
     from .models import User
     
     admin.site.register(User, UserAdmin)
     ```

  4. 프로젝트 중간에 진행했기 때문에 데이터베이스를 초기화한 후 마이그레이션 진행.

     - 초기화 방법

       1. db.sqlite3 파일 삭제

       2. migrations 팔 모두 삭제(파일명에 숫자가 붙은 파일만 삭제)

          ```bash
          $ python manage.py makemigrations
          $ python manage.py migrate
          ```

          


### Custom user & Built-in auth forms

- 회원가입 시도 후 'AttributeError(Manager isn't available; 'auth.User' has been swapped for 'accounts.User')' 발생

  - UserCreationForm과 UserChangeForm은 기존 내장 User 모델을 사용한 ModelForm이기 때문에 커스텀 User 모델로 대체해야 함

- Custom Built-in Auth Forms

  - 기존 User 모델을 사용하기 때문에 커스텀 User 모델로 다시 작성하거나 확장해야 하는 forms

    - UserCreationForm
    - UserChangeForm

  - 이처럼 커스텀 User 모델이 AbstractUser의 하위 클래스인 경우 다음과 같은 방식으로 form을 확장

    ```python
    #articles/forms.py
    from django.contrib.auth.forms import UserCreationForm
    from myapp.models import CustomUser
    
    class CustomUserCreationForm(UserCreationForm):
        class Meta:
            model = CustomUser
            fields = UserCreationForm.Meta.fields + ('custom_field')
    ```

- UserCreationForm 확장

  ```python
  #accounts/forms.py
  from django.contrib.auth.forms import UserChangeForm, UserCreationForm
  
  class CustomUserCreationForm(UserCreationForm):
      class Meta(UserCreationForm.Meta):
          model = get_user_model()
          fields = UserCreationForm.Meta.fields 
          #fields = UserCreationForm.Meta.fields + ('email,')와 같이 필드 추가 가능
  ```

- signup view 함수 코드수정

  ```python
  #accounts/views.py
  from .forms import CustomUserChangeForm, CustomUserCreationForm
  
  def signup(request):
      if request.user.is_authenticated:
          return redirect('articles:index')
      
      if request.method == 'POST':
          form = CustomUserCreationForm(request.POST)
          if form.is_valid():
              user = form.save()	
              auth_login(request, user)
              return redirect('articles:index')
      else:
          form = CustomUserCreationForm()
      context = {
          'form' : form,
      }
      return render(request, 'accounts/signup.html', context)
  ```

- get_user_model()

  - 현재 프로젝트에서 활성화된 사용자 모델(active user model)을 반환
    - User 모델을 커스터마이징한 상황에서는 Custom User모델을 반환
  - 이 때문에 Django는 User 클래스를 직접 참조하는 대신 django.contrib.auth.get_user_model()을 사용하여 참조해야 한다고 강조



## 1:N 관계 설정

> 완전한 종속 관계

### User - Article(1:N)

- User 모델 참조하기
  1. settings.AUTH_USER_MODEL
     - User 모델에 대한 외래 키 또는 다대다 관계를 정의할 때 사용해야 함
     - models.py에서 User 모델을 참조할 때 사용
  2. get_user_model()
     - 현재 활성화(active)된 User 모델을 반환
       - 커스터마이징한 User 모델이 있을 경우는 Custom User 모델, 그렇지 않으면 User을 반환
       - User을 직접 참조하지 않는 이유
     - models.py가 아닌 다른 모든 곳에서 유저 모델을 참조할 때 사용

- User와 Article 간 모델 관계 정의 후 migration

  ```python
  #articles/models.py
  from django.db import models
  from django.conf import settings
  
  class Article(models.Model):
      user = models.ForeignKey(settings.AUTH_USER_MODEL, n_delete=models.CASCADE)        
  ```

  ```bash
  $ python manage.py makemigrations
  $ python manage.py migrate
  ```

  - null 값이 허용되지 않는 user_id 필드가 별도의 값 없이 article에 추가되려 하기 때문
  - 1을 입력 후 enter : 현재 화면에서 기본 값을 설정하겠다
  - 1을 입력 후 enter: 기존 테이블에 추가되는 user_id 필드의 값을 1로 설정하겠다

  ```bash
  $ python manage.py migrate
  ```

- 게시글 출력 필드 수정

  - 게시글 작성 페이지에서 불필요한 필드가 출력되는 것을 확인

  - ArticleForm의 출력 필드 수정 후 게시글 작성 재시도

    ```python
    #articles/forms.py
    class ArticleForm(forms.ModelForm):
        class Meta:
            model = Article
            fields = ('title', 'content',)
    ```

  - 게시글 작성 시 NOT NULL constraint failed: articles_article.user_id 에러 발생

    - 게시글 작성 시 작성자 정보(article.user)가 누락되었기 때문

    - CREATE: 게시글 작성 시 작성자 정보(article.user) 추가 후 게시글 작성 재시도

      ```python
      #articles/views.py
      from django.shortcuts import redirect
      from django.views.decorators.http import require_http_methods
      from django.contrib.auth.decorators import login_required
      from .forms import ArticleForm
      
      @login_required
      @require_http_methods(['GET','POST'])
      def create(request):
          if request.method == 'POST':
              form = ArticleForm(request.POST)
              if form.is_valid():
              article = form.save(commit=False)
                  article.user = request.user
              article.save()
                  return redirect('articles:detail', article.pk)
      ```
    
    - DELETE : 자신이 작성한 게시글만 삭제 가능하도록 설정
    
      ```python
      #articles/views.py
      from django.shortcuts import get_object_or_404, redirect
      from django.views.decorators.http import require_POST
      from .models import Article
      @require_POST
      def delete(request, pk):
          article = get_object_or_404(Article, pk=pk)
          if request.user.is_authenticated:
              if request.user == article.user:
                  article.delete()
                  return redirect('articles:index')
              return redirect('articles:index', article.pk)
      ```
      
    - UPDATE: 자신이 작성한 게시글만 수정 가능하도록 설정
    
      ```python
      #articles/views.py
      from django.shortcuts import get_object_or_404, render, redirect
      from django.views.decorators.http import require_http_methods
      from django.contrib.auth.decorators import login_required
      from .models import Article
      from .forms import ArticleForm
      
      @login_required
      @require_http_methods(['GET','POST'])
      def update(request, pk):
          article = get_object_or_404(Article, pk=pk)
      if request.user == article.user:
              if request.method == 'POST':
              form = ArticleForm(request.POST, instance=article)
                  if form.is_valid():
                      form.save()
                      return redirect('articles:detail', article.pk)
              else:
                  form = ArticleForm(instance=article)
          else:
              return redirect('articles:index')
          context = {
              'form':form,
          }
          return render(request, 'articles/update.html', context)
      ```
    
    - READ: 게시글 작성 user가 누구인지 index.html에서 출력하기
    
      ```django
      <!-- articles/index.html -->
      {% extends 'base.html' %}
      {% block content %}
      {% for article in articles %}
      	<p><b>작성자: {{article.user}}</b></p>
      	<p>글 번호: {{article.pk}}</p>
      	<p>글 제목: {{article.title}}</p>
      	<p>글 내용: {{article.content}}</p>
      	<a href="{% url 'articles:detail' article.pk %}">DETAIL</a>
      {% endfor %}
      {% endblock %}
      ```
    
      - READ: 해당 게시글의 작성자가 아니라면, 수정/삭제 버튼을 출력하지 않도록 처리
    
        ```django
        <!-- articles/detail.html -->
        {% if user == article.user %}
        	<a href="{% url 'articles:update' article.pk %}">UPDATE</a>
        	<form action="{% url 'articles:delete' article.pk %}" method="POST">
                {% csrf_token %}
                <input type="submit" value="DELETE">
        	</form>
        {% endif %}
        ```
    
    

### User - Comment (1:N)

- User와 Comment 간 모델 관계 정의 후 migration

  ```python
  #articles/models.py
  from django.db import models
  from django.conf import settings
  
  class Comment(models.Model):
      article = models.ForeignKey(Article, on_delete=models.CASCADE)
      user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
  ```

  ```bash
  $ python manage.py makemigrations
  $ python manage.py migrate
  ```

  - null 값이 허용되지 않는 user_id 필드가 별도의 값 없이 comment에 추가되려 하기 때문
  - 1을 입력 후 enter : 현재 화면에서 기본 값을 설정하겠다
  - 1을 입력 후 enter: 기존 테이블에 추가되는 user_id 필드의 값을 1로 설정하겠다(기존 댓글의 작성자가 모두 1번 user가 됨)

  ```bash
  $ python manage.py migrate
  ```

- 댓글 출력 필드 수정

  - 게시글 작성 페이지에서 불필요한 필드가 출력되는 것을 확인

  - 댓글 작성 시 user ForeignKeyField를 출력하지 않도록 설정

    ```python
    #articles/forms.py
    from django import forms
    from .models import Comment
    
    class CommentForm(forms.ModelForm):
        class Meta:
          model = Comment
            exclude = ('article', 'user')
    ```
  
- 댓글 작성 시 NOT NULL constraint failed: articles_article.user_id 에러 발생
  
  - 댓글 작성 시 작성자 정보(comment.user)가 누락되었기 때문
  
    - CREATE: 댓글 작성 시 작성자 정보(request.user) 추가 후 게시글 작성 재시도
  
      ```python
      #articles/views.py
      from django.shortcuts import get_object_or_404, redirect
      from django.views.decorators.http import require_http_methods
      from django.contrib.auth.decorators import login_required
      from .forms import CommentForm
      
      @login_required
      @require_http_methods(['GET','POST'])
      def comments_create(request, pk):
          if request.user.is_authenticated:
            article = get_object_or_404(Article,pk=pk)
              comment_form = CommentForm(request.POST)
            if comment_form.is_valid():
                comment = comment_form.save(commit=False)
                  comment.article = article
                comment.user = request.user
                  comment.save()
                  return redirect('articles:detail', article.pk)
          return redirect('accounts:login')
      ```
    
    - READ: 비로그인 유저에게는 댓글 form 출력 숨기기
    
      ```django
      <!-- articles/detail.html -->
      {% if request.user.is_authenticated %}    
      	<form action="{% url 'articles:comments_create' article.pk %}" method="POST">
          	{% csrf_token %}        
          	<input type="submit" value="submit">  
      	</form>
          {% else %}    
          	<a href="{% url 'accounts:login' %}">댓글 작성하려면 로그인하세요</a>  
      {% endif %}
      ```
    
    - READ: 댓글 작성자 출력하기
    
      ```django
      <!-- articles/detail.html -->
      {% for comment in comments %}
        <li>
              {{ comment.user }} - {{ comment.content }} 
            <form action="{% url 'articles:comments_delete' article.pk comment.pk %}" method="POST" class="d-inline">
                {% csrf_token %}
              </form>
    	</li>
      {% empty %}
      	<p>댓글 없음</p>		
      {% endfor %}
      ```
    
    - DELETE : 자신이 작성한 댓글만 삭제 버튼을 볼 수 있도록 수정
    
      ```django
      <!-- articles/detail.html -->
      {% for comment in comments %}
          <li>
              {{ comment.content }}
              {% if user == comment.user %}
            	<form action="{% url 'articles:comments_delete' article.pk comment.pk %}" method="POST" class="d-inline">
                  	{% csrf_token %}
                    <input type="submit" value="DELETE">
            	</form>
              {% endif %}
    	</li>
      {% empty %}
      	<p>댓글 없음</p>		
      {% endfor %}
      ```
    
    - DELETE: 자신이 작성한 댓글만 삭제할 수 있도록 수정
    
      ```python
      #articles/views.py
      from django.shortcuts import get_object_or_404, redirect
      from django.views.decorators.http import require_POST
      from .models import Comment
        
      @require_POST
      def comments_delete(request, article_pk, comment_pk):
          if request.user.is_authenticated:
              comment = get_object_or_404(Comment, pk=comment_pk)
              if request.user ==  comment.user:
              	comment.delete()
                  return redirect('articles:detail', article_pk)
      ```
    
      

## M:N 관계 설정

### ManyToManyField

- 다대다(M : N, many-to-many) 관계 설정 시 사용하는 모델 필드

- 하나의 필수 위치인자(M:N 관계로 설정할 모델 클래스)가 필요

- 모델 필드의 RelatedManager를 사용하여 관련 개체를 추가, 제거 또는 만들 수 있음

  - Related Manager

    - 1:N 또는 M:N 관련 컨텍스트에서 사용되는 매니저

    - 같은 이름의 매서드여도 각 <u>관계(1:N, M:N)에 따라 다르게 사용 및 동작</u>

      - **1:N**에서는 target 모델 인스턴스만 사용 가능
      - **M:N** 관계에서는 관련된 두 객체에서 모두 사용 가능

    - 메서드 종류

      - add()

        - 지정된 객체를 관련 객체 집합에 추가
        - 이미 존재하는 관계에 사용하면 관계가 <u>복제되지 않음</u>
        - 모델 인스턴스, 피드 값(PK)을 인자로 허용

        ```python
        doctor1 = Doctor.objects.create(name='justin')
        patient1 = Patient.objects.create(name='tony')
        
        doctor1.patient_set.add(patient1)
        #또는
        patient1.doctors.add(doctor1)
        ```

      - remove()

        - 관련 객체 집합에서 지정된 모델 객체를 제거
        - <u>내부적으로 QuerySet.delete()</u>를 사용하여 관계가 삭제됨
        - 모델 인스턴스, 필드 값(PK)을 인자로 허용

        ```python
        doctor1 = Doctor.objects.get(pk=1)
        patient1 = Patient.objects.get(pk=1)
        
        doctor1.patient_set.remove(patient1)
        #또는
        patient1.doctors.remove(doctor1)
        ```

      - create(), clear(), set() 등

- Arguments

  1. related_name

     - target model(관계 필드를 가지지 않은 모델)이 source model(관계 필드를 가진 모델)을 참조할 때(역참조 시) 사용할 manager의 이름을 설정 -> 역참조 시에 사용하는 manager의 이름을 설정
     - ForeignKey의 related_name과 동일

     ```python
     #예시
     class Patient(models.Model):
         doctors = models.ManyToManyField(Doctor, related_name = 'patients')
         name = models.TextField()
     ```

  2. through

     - <u>중개 테이블을 직접 작성</u>하는 경우, through 옵션을 사용하여 **중개 테이블**을 나타내는 Django 모델을 지정할 수 있음

     - 일반적으로 중개 테이블에 <u>추가 데이터를 사용하는 다대다 관계와 연결</u>하려는 경우(extra data with a many-to-many relationship)에 주로 사용됨

     - 예시

       1. 모델 관계 설정

          ```python
          class Doctor(models.Model):
              name = models.TextField()
              
              def __str__(self):
                  return f'{self.pk}번 의사 {self.name}'
          
          class Patient(models.Model):
              doctors = models.ManyToManyField(Doctor, through='Reservation')
              name = models.TextField()
              
              def __str__(self):
                  return f'{self.pk}번 환자 {self.name}'
              
          class Reservation(models.Model):	#중개 모델. 두 모델과 1:N 관계
              doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
              patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
              symptom = models.TextField()
              reserved_at = models.DateTimeField(auto_now_add=True)
              
              def __str__(self):
                  return f'{self.doctor.pk}번 의사의 {self.patient.pk}번 환자'
          ```

       2. 데이터베이스 초기화 / 마이그레이션 및 shell_plus 실행

          ```bash
          $ python manage.py makemigrations
          $ python manage.py migrate
          
          $ python manage.py shell_plus
          ```

       3. 중개 테이블 확인

          ![image-20220419172459630](Model Relationship.assets/image-20220419172459630.png)

       4. SQLITE에서 의사, 환자, 예약 생성

          ```sqlite
          --의사 1명과 환자 2명 생성
          doctor1 = Doctor.objects.create(name='justin')
          
          patient1 = Patient.objects.create(name='tony')
          
          patient2 = Patient.objects.create(name='harry')
          
          --예약 생성
          reservation1 = Reservation(doctor=doctor1, patient=patient1, symptom = 'headache')
          
          reservation1.save()
          
          doctor1.patient_set.all()
          <QuerySet [<Patient: 1번 환자 tony>]>
          
          patient1.doctors.all()
          <QuerySet [<Doctor: 1번 의사 justin>]>
          ```

       5. 중개 테이블 확인

          ![image-20220419173412804](Model Relationship.assets/image-20220419173412804.png)

       6. SQLITE에서 예약 생성

          ```sqlite
          --through_defaults를 사용해 add(), create() 또는 set()을 사용하여 관계를 생성
          patient2.doctors.add(doctor1, through_defaults={'symptom':'flu'})
          
          doctor1.patient_set.all()
          <QuerySet [<Patient: 1번 환자 tony>, <Patient: 2번 환자 harry>]>
          
          patient2.doctors.all()
          <QuerySet [<Doctor: 1번 의사 justin>]>
          ```

       7. 중개 테이블 확인

          ![image-20220419173822769](Model Relationship.assets/image-20220419173822769.png)

       8. 예약 삭제

          ```sqlite
          doctor1.patient_set.remove(patient1)
          
          patient2.doctors.remove(doctor1)
          ```

  3. symmetrical

     - ManyToManyField가 <u>동일한 모델</u>(on self)을 가리키는 정의에서만 사용
     - symmetrical=True(기본값)일 경우 Django는 person_set 매니저를 추가하지 않음(한 쪽을 추가하면 같이 추가되므로 역참조 매니저 필요 없음)
     - source 모델의 인스턴스가 target 모델의 인스턴스를 참조하면, target 모델 인스턴스도 source 모델 인스턴스를 자동으로 참조하도록 함
       - 즉, <u>내가 당신의 친구라면 당신도 내 친구가 되는 것</u>
       - 대칭을 <u>원하지 않는 경우 False</u>로 설정
       - [Follow 기능 구현](#Follow)에서 다시 확인

     ```python
     from django.db import models
     
     class Person(models.Model):
         friends = models.ManyToManyField('self')
         #friends = models.ManyToManyField('self', symmetrical=False)
     ```

- 데이터베이스에서의 표현

  - Django는 다대다 관계를 나타내는 중개 테이블(앱 이름_클래스이름\_클래스 변수 이름)을 만듦
  - 테이블 이름은 다대다 필드의 이름과 이를 포함하는 모델의 테이블 이름을 조합하여 생성됨
    - 중개 테이블의 필드 생성 규칙

      - source model 및 target model 모델이 <u>다른</u> 경우
        - id
        - <containing_model>_id
        - <other_model>_id
      - ManyToManyField가 <u>동일한 모델</u>을 가리키는 경우
        - id
        - from\_< model >_id
        - to\_< model >_id



#### Like

- User와 Article은 M:N 관계 

1. ManyToManyField 작성 후 마이그레이션 -> 에러 발생

   ```python
   #articles/models.py
   #accounts/models.py에 써도 되긴 함
   
   class Article(models.Model):
       user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
       like_users = models.ManyToManyFiels(settings.AUTH_USER_MODEL)
       #유저 모델 참조 -> settings.AUTH_USER_MODEL
       ...
   ```

   ```bash
   $ python manage.py makemigrations
   ```

   - 에러 발생의 원인

     - like_users 필드 생성 시 자동으로 역참조는 `.article_set` 매니저를 생성. 그러나, 이전 1:N(User:Article) 관계에서 <u>이미 해당 매니저 이름을 사용 중</u>이기 떄문이다.

       - User:Article(1:N 관계)
         - 참조: article.user.all()
         - 역참조: user.article_set.all()
       - User:Article(M:N 관계)
         - 참조: article.like_users.all()
         - 역참조: user.article_set.all

       => User와 관계된 ForeignKey 또는 ManyToManyField 중 하나에 related_name 추가 필요

2. related_name 설정 후 마이그레이션 다시 진행

   ```python
   #articles/models.py
   
   class Article(models.Model):
       user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
       like_users = models.ManyToManyFields(settings.AUTH_USER_MODEL, related_name='like_articles')	#중개 테이블 생성
       ...
   ```

   ```bash
   $ python manage.py makemigrations
   $ python manage.py migrate
   ```

   - 현재 User-Article 간 사용 가능한 DB API
     - article.user: 게시글을 작성한 유저 - 1:N
     - article.like_users: 게시글을 좋아요한 유저 - M:N
     - user.article_set: 유저가 작성한 게시글(역참조) - 1:N
     - user.like_articles: 유저가 좋아요한 게시글(역참조) - M:N

3. 생성된 중개 테이블 확인

   ![image-20220419210316754](Model Relationship.assets/image-20220419210316754.png)

4. url, like view 함수 작성

   ``` python
   # articles/urls.py
   
   urlpatterns = [
       path('<int:article_pk>/likes/', views.likes, name='likes'),
   ]
   
   #articles/views.py
   @require_POST
   def likes(request, article_pk):
       if request.user.is_authenticated:
           article = get_object_or_404(Article, pk=article_pk)
   
           if article.like_users.filter(pk=request.user.pk).exists():
           # if request.user in article.like_users.all():
               article.like_users.remove(request.user)
           else:
               article.like_users.add(request.user)
           return redirect('articles:index')
       return redirect('accounts:login')
   ```

   - QuerySet API - 'exists()'
     - QuerySet에 결과가 포함되어 있으면 True를 반환하고 그렇지 않으면 False를 반환
     - 특히 규모가 큰 QuerySet의 컨텍스트에서 특정 개체 존재 여부와 관련된 검색에 유용
     - 고유한 필드(ex. primary key)가 있는 모델이 QuerySet의 구성원인지 여부를 찾는 가장 효율적인 방법

5. index 페이지에 like 출력 부분 작성

   ```django
   <!-- articles/index.html -->
   
   {% extends 'base.html' %}
   
   {% block content %}
     <h1>Articles</h1>
     {% if request.user.is_authenticated %}
       <a href="{% url 'articles:create' %}">[CREATE]</a>
     {% else %}
       <a href="{% url 'accounts:login' %}">[새 글을 작성하려면 로그인하세요.]</a>
     {% endif %}
     <hr>
     {% for article in articles %}
       <p><b>작성자 : {{ article.user }}</b></p>
       <p>글 번호 : {{ article.pk }}</p>
       <p>글 제목 : {{ article.title }}</p>
       <p>글 내용 : {{ article.content }}</p>
       <div>
         <form action="{% url 'articles:likes' article.pk %}" method="POST">
           {% csrf_token %}
           {% if request.user in article.like_users.all %}
             <input type="submit" value="좋아요 취소">
           {% else %}
             <input type="submit" value="좋아요">
           {% endif %}
         </form>
       </div>
       <p>{{ article.like_users.all|length }} 명이 이 글을 좋아합니다.</p>
       <a href="{% url 'articles:detail' article.pk %}">[DETAIL]</a>
       <hr>
     {% endfor %}
   {% endblock %}
   ```

6. 좋아요 버튼 클릭 후 테이블 확인

   ![image-20220419174423531](Model Relationship.assets/image-20220419174423531.png)



#### Profile Page

1. url, profile view 함수 작성

   ```python
   #accounts/urls.py
   
   urlpatterns = [
       path('<username>/', views.profile, name='profile'),
       '''위에서부터 url pattern을 찾기 때문에, route가 문자열로 시작하는 path함수가 맨 위에 있을 경우 int가 나오지 않는 이상 어떤 경우에도 같은 view 함수로 갈 수 있다. 따라서 route가 문자열로 시작하는 path 함수의 경우 맨 아래에 위치시켜야 한다.'''
   ]
   
   #accounts/views.py
   from django.shortcuts import render, get_object_or_404
   from django.contrib.auth import get_user_model
   
   def profile(request, username):
       User = get_user_model()
       person = get_object_or_404(User, username=username)   
       context = {  
           'person': person,
       }    
       return render(request, 'accounts/profile.html', context)
   ```

2. profile 페이지 작성

   ```django
   <!-- accounts/profile.html -->
   {% extends 'base.html' %}
   {% block content %}
   <h1>{{  person.username  }}님의 프로필</h1>
   <hr>
   <h2>{{  person.username  }}'s 게시글</h2>
   {% for article in person.article_set.all %}
   	<div>{{  article.title  }}</div>
   {% endfor %}
   <hr>
   <h2>{{  person.username  }}'s 댓글</h2>
   {% for comment in person.comment_set.all %}  
   	<div>{{  comment.content  }}</div>
   {% endfor %}
   <hr>
   <a href="{% url 'articles:index' %}">[back]</a>
   {% endblock content %}
   ```

3. base에 프로필 링크 작성

   ```django
   <!-- base.html -->
   <body>
       <div class="container">
           {% if request.user.is_authenticated %}
           	<h3>Hello, {{  user  }}</h3>
           <a href="{% url 'accounts:profile' request.user.username %}">내 프로필 </a>
           <!-- request.user.username 대신 request.user 써도 무방 -->
           ...
       </div>
   </body>
   ```

4. index 페이지에 프로필 링크 작성

   ```django
   <!-- articles/index.html -->
   
   <p>
       <b>작성자: <a href="{% url 'accounts:profile' article.user.username %}"> {{  article.user  }} </a></b>
   </p>
   ```



#### Follow

1. ManyToManyField 작성 후 마이그레이션

   ```python
   #accounts/models.py
   class User(AbstractUser):
       followings = models.ManyToManyField('self', symmetrical=False, related_name='followers')
       #자기 자신을 참조한다. 역참조 시 followers 사용
   ```

   ```bash
   $ python manage.py makemigrations
   $ python manage.py migrate
   ```

2. 생성된 중개 테이블 확인

   ![image-20220419174519123](Model Relationship.assets/image-20220419174519123.png)

3. url, follow view 함수 작성

   ```python
   #accounts/urls.py
   
   urlpatterns = [
       path('<int:user_pk>/follow/', views.follow, name='follow'),
   ]
   
   #accounts/views.py
   @require_POST
   def follow(request, user_pk):
       if request.user.is_authenticated:
           person = get_object_or_404(get_user_model(), pk=user_pk)
           if person != request.user:
               if person.followers.filter(pk=request.user.pk).exists():
               # if request.user in person.followers.all():
                   person.followers.remove(request.user)
               else:
                   person.followers.add(request.user)
           return redirect('accounts:profile', person.username)
       return redirect('accounts:login')
   ```

4. profile 페이지에 팔로우와 언팔로우 버튼 작성

   ```django
   <!-- accounts/profile.html -->
   {% extends 'base.html' %}
   {% block content %}
   <h1>
       {{ person.username }}님의 프로필
   </h1>
   <div> 
     <div>
       <!-- 팔로잉 수/ 팔로워 수 출력 -->
       팔로잉 : {{ person.followings.all|length }} / 팔로워 : {{ person.followers.all|length }}
     </div>
     <!-- 자기 자신을 팔로우할 수 없음 -->
     {% if user != person %}
       <div>
         <form action="{% url 'accounts:follow' person.pk %}" method="POST">
           {% csrf_token %}
           {% if user in person.followers.all %}
             <input type="submit" value="Unfollow">
           {% else %}
             <input type="submit" value="Follow">
           {% endif %}
         </form>
       </div>
     {% endif %}
   </div>
   {% endblock %}
   ```

   - {% with %}를 사용하면 더 간결하게 표현할 수 있다.

     - with 태그 안에서만 변수에 저장되어 있다. (최적화와는 관련 없음)

     ```django
     {% with followers=person.followers.all followings=person.followings.all %}
         <div>
             팔로워 : {{ followers|length }} / 팔로우 : {{ followings|length }}
         </div>
         <div>
             {% if user != person %}
             <form action="{% url 'accounts:follow' person.pk %}" method="POST">
                 {% csrf_token %}
                 {% if user in followers %}
                 <input type="submit" value="Unfollo">
                 {% else %}
                 <input type="submit" value="Follow">
                 {% endif %}
             </form>
             {% endif %}
         </div>
     {% endwith %}
     ```

5. 팔로우 버튼 클릭 후 테이블 확인

   ![image-20220419174629600](Model Relationship.assets/image-20220419174629600.png)

