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

- 1:N 관계 related manager

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
      comment =  Comment.objects.get(pk=1)
      comment.article				--<Article: title>
      comment.article.content		--'content'
      comment.article_id			--1
      ```

- ForiegnKey arguments - 'related_name'

  - 역참조 시 사용할 이름('model_set' manager)을 변경할 수 있는 옵션

    ```python
    # articles/models.py
    class Comment(models.Model):
        article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
    ```

  - 위와 같이 변경하면 <u>article.comment_set은 더이상 사용할 수 없고</u>, **article.comments**로 대체됨

  - **[주의]** 역참조 시 사용할 이름 수정 후, <u>migration</u> 과정 필요

​                                                                                              

### Comment Create

- CommentForm 작성

  ```python
  #articles/forms.py
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
      commnt_form = CommentForm()
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
      path('<int:pk>/comments/', views..comments_create, name='comments_create')
  ]
  
  #articles/views.py
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
  - save(commit=False)
    - Create, but don't save the new instance.
    - 아직 데이터베이스에 저장되지 않은 인스턴스를 반환
    - 저장하기 전에 객체에 대한 사용자 지정 처리를 수행할 때 유용하게 사용



### Comment Read

- 댓글 출력

  - 특정 article에 있는 모든 댓글을 가져온 후 context에 추가

    ```python
    #articles/views.py
    from .models import Article, Comment
    
    def detail(request, pk):
        article = get_object_or_404(Article, pk=pk)
        comment_form = CommentForm()
        comments = article.comment_set.all()
        context = {
            'article' : article,
            'comment_form' : comment_form,
            'commets' : comments
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
        {% for comment in comments %}
        	<li>{{ comment.content }}</li>
        {% endfor %}
    </ul>
    {% endfor %}
    ```

    

### Comment Delete

- 댓글 삭제 후 detail page에서 댓글 삭제 확인

  ```python
  #articles/urls.py
  app_name = 'articles'
  urlpatterns=[
      path('<int:article.pk>/comments/<int:comment_pk>/delete/', views.comments_delete, name='comments_delete')
  ]
  
  #articles/views.py
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

- 댓글이 없는 경우 대체 컨텐츠 출력(DTL의 for-empty 태크 활용)

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
      class Meta(UserCreationForm,.Meta):
          model = get_user_model()
          fields = UserCreationForm.Meta.fields + ('email,')
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



