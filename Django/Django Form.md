# Django Form

## Form Class

### Form

- 유효성 검증(사용자가 입력한 데이터를 검증) 도구
- 외부의 악의적 공격 및 데이터 손상에 대한 <u>중요한 방어 수단</u>
- Form과 관련된 유효성 검사를 단순화하고 자동화할 수 있는 기능을 제공. 더 안전하고 빠르게 수행하는 코드를 작성할 수 있게 한다
- Django는 form에 관련된 작업의 아래 세 부분을 처리해준다
  1. 렌더링을 위한 데이터 준비 및 재구성
  2. 데이터에 대한 HTML forms 생성
  3. 클라이언트로 부터 받은 데이터 수신 및 처리

### Form Class

- Django Form 관리 시스템의 핵심. Django의 빌트인 클래스.
- Form 내 field, field 배치, 디스플레이 widget, label, 초기값, 유효하지 않는 field에 관련된 에러메세지 결정.
- Django는 사용자의 데이터를 받을 때 해야 할 과중한 작업(데이터 유효성 검증, 필요 시 입력된 데이터 검증 결과 재출력, 유효한 데이터에 대해 요구되는 동작 수행 등)과 반복 코드를 줄여줌

#### Form 선언하기

```python
#articles/forms.py
from django import forms

class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    #사용자가 10자 초과 쓰는 것을 막음
    content = forms.CharField()
```

- Model을 선언하는 것과 유사하다.
- Forms 라이브러리에서 파생된 Form 클래스를 상속받는다.

#### Form 사용하기

```python
#articles/views.py
from .forms import ArticleForm

def new(request):
    form = ArticleForm()	#인스턴스 만들었다
    context = {
        'form':form,
    }
    return render(request, 'articles/new.html', context)
```

```django
<!-- new.html -->
{% extends 'base.html' %}

{% block content %}
	<h1 class="text-center">NEW</h1>
	<form action="{% url 'articles:create' %}" method="POST">
        {% csrf_token %}
        {{ form.as_p }}	
        	{% comment %}
        	forms.py에서 지정한 것 출력
        	그런데 input태그는 inline 속성
        	-> {{ form }}만 하면 줄바꿈이 되지 않은 채 출력됨 
        	-> as_p를 써서 <p>로 감싸 렌더링 -> 줄바꿈 가능!
        	{% endcomment %}
        
        <input type="submit">
	</form>
	<hr>
	<a href="{% url 'articles:index' %}">[back]</a>
{% endblock %}
```

- Form rendering options

  > < label > & < input > 쌍에 대한 3가지 출력 옵션

  - as_p()
    - 각 필드가 단락(< p > 태그)으로 감싸져서 렌더링 됨
  - as_ul()
    - 각 필드가 목록 항목(< li > 태그)으로 감싸져서 렌더링 됨
    - < ul > 태그는 직접 작성해야 함
  - as_table()
    - 각 필드가 테이블(< tr > 태그) 행으로 감싸져서 렌더링 됨
    - < table > 태그는 직접 작성해야 함

- Django의 HTML input 요소 표현 방법 2가지

  1. Form fields (ex. CharField_input의 text 속성)

     - input에 대한 유효성 검사 로직을 처리하며 템플릿에서 직접 사용됨
     - 그러나 모든 유형의 input type을 제공하지 않는다. (ex. textarea) -> Widgets 사용

  2. Widgets

     > Django의 HTML input element 표현

     - 웹 페이지의 HTML input 요소 렌더링
     - GET/POST 딕셔너리에서 데이터 추출
     - widgets은 <u>반드시 Form fields에 할당</u>됨
     - Form Fields와의 차이점(혼동하지 말기!)
       - Form FIelds: input의 유효성 검사를 처리
       - Widgets: 웹페이지에서 input element의 단순 raw한 렌더링 처리

     ```python
     #articles/forms.py
     from django import forms
     
     class ArticleForm(forms.Form):
         REGION_A = 'sl'	
         REGION_B = 'dj'
         REGION_C = 'gj'
         REGION_CHOICES=[
             (REGION_A, '서울'),	#(변수값, 사용자에게 출력되는 형태)
             (REGION_B, '대전'),
             (REGION_C, '광주'),
         ]
         #사용자가 '서울'클릭하면 sl이 우리에게 온다.
         
         title = forms.CharField(max_length=10)
         content = forms.CharField(widget=forms.Textarea)
         region = forms.ChoiceField(choices=REGIONS_CHOICES, widget=forms.Select())	#drop-down형태의 선택 입력
     ```

     

## ModelForm

- Django Form을 사용하다 보면 Model에 정의한 필드를 유저로부터 입력 받기 위해 Form에서 <u>Model 필드를 재정의하는 행위가 중복</u>될 수 있음 => Model을 통해 Form Class를 만들 수 있는 ModelForm이라는 Helper 제공
- 모델 필드 속성에 맞는 html element를 만들어주고 이를 통해 받은 데이터를 view 함수에서 유효성 검사를 할 수 있도록 함

### Model Form Class

- Model을 통해 Form Class를 만들 수 있는 Helper
- 일반 Form Class와 완전히 같은 방식(객체 생성)으로 view에서 사용 가능

#### ModelForm 선언하기

```python
#articles/forms.py
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    class Meta:	#ArticleModelForm에 대한 data를 작성
        model = Article		#어떤 모델을 기반으로 만들어질 모델 폼인지 그 모델 이름 작성
        fields = '__all__'	#어떤 필드를 출력할 것인지. 사용자로부터 입력받은 전체 필드를 출력한다
        #exclude = {'title',}	#출력에서 제외. fields와 exclude 같이 쓰지 못함
```

- forms 라이브러리에서 파생된 ModelForm 클래스를 상속받음
- 정의한 클래스 안에 Meta 클래스를 선언하고, 어떤 모델을 기반으로 Form을 작성할 것인지에 대한 정보를 Meta 클래스에 지정
  - **주의**: 클래스 변수 fields와 exclude는 동시에 사용할 수 없음

##### Meta class

- Model의 정보를 작성하는 곳
- ModelForm을 사용할 경우 사용할 모델이 있어야 하는데 Meta Class가 이를 구성함
  - 해당 Model에 정의한 field 정보를 Form에 적용하기 위함

[참고]

- Inner Class(Nested Class)

  - 클래스 내에 선언된 다른 클래스
  - 관련 클래스를 함께 그룹화하여 가독성 및 프로그램 유지 관리를 지원(논리적으로 묶어서 표현)
  - <u>외부에서 내부 클래스에 접근할 수 없으므로</u> 코드의 복잡성을 줄일 수 있음

- *Meta 데이터

  - 데이터에 대한 데이터

    ex. 사진 촬영 - 사진 데이터 - 사진의 메타 데이터(촬영 시간, 렌즈, 조리개 값 등)

#### create view 수정

```python
#articles/views.py
def create(request):
    form = ArticleForm(request.POST)	#request의 POST 딕셔너리 데이터를 한방에 넣은 상태로 form 인스턴스 생성
    if form.is_valid():	#유효성 검증
        article = form.save()	#form.save()을 하면 생성된 객체가 나옴.
        return redirect('articles:detail', article.pk)
    return redirect('articles:new')
```

- is_valid() method

  - 유효성 검사를 실행하고, 데이터가 유효한지 여부를 boolean으로 반환
  - 데이터 유효성 검사를 보장하기 위한 많은 테스트에 대해 Django는 is_valid()를 제공

  [참고] 유효성 검사

  - 요청한 데이터가 특정 조건에 충족하는지 확인하는 작업
  - 데이터베이스 각 필드 조건에 올바르지 않은 데이터가 서버로 전송되거나 저장되지 않도록 하는 것 

- The save() method

  - Form에 바인딩 된 데이터에서 데이터 베이스 **객체를 만들고 저장**
  - ModelForm의 하위(sub) 클래스(ArticleForm)는 기존 모델 인스턴스를 키워드 인자 instance로 받아 들일 수 있음
    - 이것이 제공되면 save()는 해당 인스턴스를 수정(UPDATE)
    - 제공되지 않은 경우 save()는 지정된 모델의 새 인스턴스를 만듦(CREATE)
  - Form의 유효성이 확인되지 않은 경우(hasn't been validated) save()를 호출하면 form.errors를 확인하여 에러 확인 가능

  ```python
  form = ArticleForm(request.POST)
  #CREATE- instance 없음
  new_article = form.save()
  #UPDATE - instance 있음
  article = Article.objects.get(pk=1)
  form = ArticleForm(request.POST, instance=article)
  form.save()
  ```

  - [참고] HTTP method

    - GET: 조회/검색할 때
    - POST: DB에 조작을 가하는 행위일 때

  - new와 create를 합칠 수 있다.

    - 둘 다 CRUD 중 C를 위한 함수. 그런데 request의 method가 달라서 나눠져있던 것
      - new.html -> create.html
      - action 값이 없어도 동작.
        - html form tag의 특징. action값이 없으면 현재 url로 요청을 보낸다.
    - 추가적으로, edit과 과거의 new함수도 사실상 하는 일이 같음.(조회. GET 요청) update는 과거의 create 함수와 하는 일이 같음.(수정. POST) => 하나로 만들 수 있다.

    ```python
    #views.py
    def create(request):
        if request.method == 'POST':	#POST일때만 DB조작하기 때문에 POST만 확인
            #기존 create 함수
            form = ArticleForm(request.POST)	
        	if form.is_valid():	#유효성검사
            	article = form.save()	
            	return redirect('articles:detail', article.pk)
    
        else:#POST가 아닌 다른 모든 메서드일 때
            #기존 new 함수
            form = ArticleForm()
        context={	#유효성검사 통과 못했을 때도 고려
            'form':form,	
        }#form 2가지 상태(:유효성검사 통과 못했을 때-에러메세지 들고 온다. ul태그로 출력됨-,인스턴스-빈 폼-)
        return render(request,'articles/new.html', context)
    
    def update(request, pk):
        article = Article.objects.get(pk=pk)
        if request.method == 'POST':	#기존 update.create와 다른 점: 조회와 *instance*
            form = ArticleForm(request.POST, instance=article)	
        	if form.is_valid():	#유효성검사
            	article = form.save()
            	return redirect('articles:detail', article.pk)
        else:	#기존 edit
            form = ArticleForm(instance=article)
        context = {
            'article': article,
            'form': form,
        }
        return render(request, 'articles/update.html', context)
    
    def delete(request, pk):
        article = Article.objects.get(pk=pk)
        if request.method== 'POST':
            article.delete()
            return redirect('articles:index')
        return redirect('articles:detail', article.pk)
    ```

#### forms.py 파일 위치

- Form class는 forms.py뿐만 아니라 다른 어느 위치에 두어도 상관 없음
- 하지만 되도록 **app폴더/forms.py**에 작성하는 것이 일반적인 구조

#### Form & ModelForm 비교

- Form
  - 어떤 Model에 저장해야 하는지 알 수 없으므로 유효성 검사 이후 cleaned_data 딕셔너리를 생성
  - cleaned_data  딕셔너리에서 데이터를 가져온 후 .save() 호출해야 함(매핑을 해주고 .save()해줘야 한다.)
  - Model에 연관되지 않은 데이터를 받을 때 사용
- ModelForm
  - Django가 해당 model에서 양식에 필요한 대부분의 정보를 이미 정의
  - 어떤 레코드를 만들어야 할지 알고 있으므로 바로 .save() 호출 가능

#### Widgets 활용하기

- Django의 HTML <u>input element 표현</u>(유효성 검사x)

- HTML 렌더링을 처리

- 2가지 작성 방식을 가짐

  - 첫번째 방식_Django에서 권장하지 않는다

    ```python
    #articles/forms.py
    class ArticleForm(forms.ModelForm):
        class Meta:
            model = Article
            fields = '__all__'
            widgets = {
                'title': forms.TextInput(attrs={
                    'class':'my-title',
                    'placeholder': 'Enter the title',
                    'maxlength': 10,
                    }
                )
            }
    ```

  - 두번째 방식_권장

    ```python
    class ArticleForm(forms.ModelForm):
        title = forms.CharField(
            widget=forms.TextInput(
            	attrs={		#속성값을 넣기 위함
                    'class':'my-title', 'second-class',	#부트스트랩 클래스 여기에 써야함
                    'placeholder': 'Enter the title',
                }
            )
        )
        content = forms.CharField(
            widget=forms.Textarea(
            	attrs={		
                    'class':'my-title', 
            }
            )     
        )
        class Meta:
        model = Article
            fields = '__all__'
    ```

- 에러메세지 바꾸는 방법

```python
content = forms.CharField(
    widget=forms.Textarea(
    	attrs={
            'class' : 'my-content',            
        }
    ),
    error_messages={
        'required' : 'Please enter your content!!'
    }
)
```



## Rendering fields manually

### 수동으로 Form 작성하는 2가지 방법

1. Rendering fields manually

   ```django
   <!--articles/create.html -->
   <h1>Create</h1>
   <hr>
   
   <form action="" method="POST">
       {% csrf_token %}
       <div>
           {{ form.title.errors }}
           {{ form.title.label_tag }}
           {{ form.title }}
       </div>
       <div>
           {{ form.content.errors }}
           {{ form.content.label_tag }}
           {{ form.content }}
       </div>
       <input type="submit">
   </form>
   ```

2. Looping over the form's fields({% for %})

   ```django
   <!--articles/create.html -->
   <form action="{% url 'articles:create' %}" method="POST">
       {% csrf_token %}
       {% for field in form %}
           {{ field.errors }}
           {{ field.label_tag }}
           {{ field }}
       {% endfor %}
       <input type="submit">
   </form>
   ```

### Bootstrap과 함께 사용하기

1. Bootstrap class with widgets

   - Bootstrap Form을 사용해 적용한다
   - 핵심 클래스: form-control

   ```python
   #articles/forms.py
   class ArticleForm(forms.ModelForm):
       title = forms.CharField(
           widget=forms.TextInput(
           	attrs={		
                   'class':'my-title form-control',	
                   'placeholder': 'Enter the title',
               }
           )
       )
       content = forms.CharField(
           widget=forms.Textarea(
           	attrs={		
                   'class':'my-title form-control', 
               }
           ),
           error_messages={
           'required' : 'Please enter your content!!'
       	}        
       )
       class Meta:
           model = Article
           fields = '__all__'
   ```

   ```django
   <!-- 에러메세지 색상 바꾸기 -->
   <!--articles/create.html -->
   <form action="{% url 'articles:create' %}" method="POST">
       {% csrf_token %}
       {% for field in form %}
       	{% if field.errors %}	
       		{% for error in field.errors %}
       			<div class="alert alert-danger">{{ error }}</div>
       		{% endfor %}
       	{% endif %}
           {{ field.label_tag }}
           {{ field }}
       {% endfor %}
       <input type="submit">
   </form>
   ```

2. Django Bootstrap 5 Library

   - django-bootstrap v5

     - form class에 bootstrap을 적용시켜주는 라이브러리
     - 한번에 끝낼 수 있지만 커스텀이 어려워짐(자율성 떨어짐)

     ```bash
     $ pip install django-bootstrap-v5
     ```

     ```python
     #settings.py
     INSTALLED_APPS=[
         ...
         'bootstrap5',
         ...
     ]
     ```

   ```django
   <!-- update.html -->
   {% extends 'base.html' %}	<!-- base.html에 bootstrap cdn 추가해야됨 -->
   {% load bootstrap5 %}
   
   {% block content %}
   	<h1>UPDATE</h1>
   	<hr>
   	<form action="{% url 'articles:update' article.pk %}" method="POST">
           {% csrf_token %}
           {% bootstrap_form form %}
           <input type="submit">
   	</form>
   	<hr>
   	<a href="{% url 'articles:detail' article.pk %}">[back]</a>
   {% endblock %}
   ```



## Handling HTTP requests

> HTTP 요청에 따라 적절한 예외처리 혹은 데코레이터를 사용해 서버를 보호하고 클라이언트에게 정확한 상황을 제공하는 것은 중요함

### Django에서 HTTP 요청을 처리하는 방법

1. Django shortcut functions

   - django.shortcuts 패키지는 개발에 도움이 될 수 있는 여러 함수와 클래스를 제공

   - shortcuts function 종류

     - render(request, template_name, context=None, content_type=None, status=None, using=None)

       - templates에 data(dictionary `'템플릿에서 사용할 변수이름': 파이썬 변수` 형태의 context)를 넣어서 보내고 싶을 때 이용

     - redirect(to, permanent=False, *args, **kwargs)

       - templates나 url(to)로 이동하고 싶을 때 사용. data는 넘길 수 없다.

     - get_object_or_404()

       ```python
       from django.shortcuts import get_object_or_404
       
       def update(request, pk):
           article = Article.objects.get_object_or_404(pk=pk)
       ```

       - objects에서 get()을 호출했으나 해당 객체가 없을 경우 DoesNotExist 예외 대신 Http 404를 raise.
         - get(): 조건에 맞는 데이터가 없을 경우 예외 발생.
           - 코드 실행 단계에서 발생한 예외 및 에러에 대해서 브라우저는 http status code 500으로 인식
       - **상황에 따라 적절한 예외처리**를 하고 **클라이언트에게 올바른 에러 상황을 전달하는 것**은 개발의 중요한 요소 중 하나이다.

     - get_list_or_404()

2. View decorators

   ```python
   from django.views.decorators.http import require_http_methods, require_POST, require_safe
   
   @require_http_methods('GET', 'POST')
   def create(request):
       pass
   
   @require_POST
   def delete(request, pk):	#URL로 delete 요청 시 405 http status code
       pass
   
   @require_safe
   def index(request):
       pass
   ```

   - django는 다양한 HTTP 기능을 지원하기 위해 view 함수에 적용할 수 있는 여러 데코레이터를 제공
     - Decorator: 원본 함수를 수정하지 않으면서 추가 기능만을 구현할 때 사용
   - Allowed HTTP methods
     - 요청 메서드에 따라 view 함수에 대한 엑세스를 제한
     - 요청이 조건을 충족시키지 못하면 HttpResponseNotAllowed을 return(405 Method Not Allowed)
     - 종류
       - @require_http_methods('GET', 'POST'): view 함수가 특정한 method 요청에 대해서만 허용하도록 하는 데코레이터
       - @require_POST: view 함수가 POST method 요청만 승인하도록 하는 데코레이터
       - @require_safe: view 함수가 GET 및 HEAD method만 허용하도록  요구하는 데코레이터. (django는 @require_GET 대신 @require_safe를 사용하는 것을 권장)



## Media files

> 미디어 파일. 사용자가 웹에서 업로드하는 정적 파일(user-upload). 유저가 업로드한 모든 정적 파일

### Model field

#### ImageField()

- 이미지 업로드에 사용하는 모델 필드
- FileField를 상속받는 서브 클래스이기 때문에 FileField의 모든 속성 및 메서드를 사용 가능하며, 더해서 사용자에 의해 업로드 된 객체가 유효한 이미지인지 검사
-  ImageField 인스턴스는 최대 길이가 100자인 문자열로 DB에 생성되며, max_length 인자를 사용하여 최대 길이를 변경 할 수 있음

**[주의]** 사용하려면 반드시 Pillow 라이브러리 필요함

##### Arguments

- upload_to='images/': 실제 이미지가 저장되는 경로를 지정

  - 업로드 디렉토리와 파일 이름을 설정하는 2가지 방법

    - 문자열 값이나 경로 지정

      ```python
      #models.py
      class MyModel(models.Model):
          upload = models.FileField(upload_to='uploads/')
          upload = models.FileField(upload_to='uploads/%Y/%m/%d/')
      ```

      - 파이썬의 strftime() 형식이 포함될 수 있으며, 이는 파일 업로드 날짜/시간으로 대체 됨
        time.strftime(format[ , t]):날짜 및 시간 객체를 문자열 표현으로 변환하는 데 사용. 하나 이상의 형식화된 코드 입력을 받아 문자열 표현을 반환

    - 함수 호출

      ```python
      #models.py
      def articles_image_path(instance, filename):
          return f'image_{instance.pk}/{filename}'
      class Article(models.Model):
          image = models.ImageField(upload_to=articles_image_path)
      ```

      - 필수 인자
        - instance: FileField가 정의된 모델의 인스턴스. 대부분 이 객체는 아직 데이터베이스에 저장되지 않았으므로 PK 값이 아직 없을 수 있음
        - filename: 기존 파일에 제공된 파일  이름

- blank=True: 이미지 필드에 빈 값(빈  문자열)이 허용되도록 설정(이미지를 선택적으로 업로드할 수 있도록)

#### FileField()

- 파일 업로드에 사용하는 모델 필드
- 선택인자
  - upload_to
  - ~~storage~~

#### Model field option

- blank

  - 기본 값: False
  - True인 경우 필드를 비워둘 수 있음. **DB에 빈 문자열로 저장**
  - **Validation-related**
  - 유효성 검사에서 사용됨(is_valid)
    - 모델 필드에 blank=True를 작성하면 <u>form 유효성 검사에서 빈 값</u>을 입력할 수 있음

- null

  - 기본 값: False

  - True인 경우 django는 빈 값에 대해 **DB에 NULL로 저장**
  - **Database-related**
    - 문자열 기반 및 비문자열 기반 필드 모두에 대해  **null은 DB에만 영향**을 미침
  - 주의 사항
    - CharField, TextField와 같은 <u>문자열 기반 필드에는 사용하는 것을 피해야 함</u>
      - 문자열 기반 필드에 True로 설정 시 '데이터 없음(no data)'에 "빈 문자열(1)"과 "NULL(2)"의 2가지 가능한 값이 있음을 의미하게 됨.
      - 대부분의 경우 "데이터 없음"에 대해 두 개의 가능한 값을 갖는 것은 중복되는 것이며, Django는 NULL이 아닌 빈 문자열을 사용하는 것이 규칙

#### ImageField(or FileField)를 사용하기 위한 몇 가지 단계

1. settings.py에 **MEDIA_ROOT, MEDIA_URL** 설정
2. **upload_to** 속성을 정의하여  업로드된 파일에 사용할 **MEDIA_ROOT**의 하위 경로를 지정
3. 업로드된 파일의 경로는 django가 제공하는 **'url' 속성**을 통해 얻을 수 있음

```django
<img src="{{ article.image.url }}" alt='{{ article.image }}'
```

- MEDIA_ROOT

  ```python
  #settings.py
  MEDIA_ROOT = BASE_DIR / 'media'
  ```

  - 사용자가 업로드한 파일(미디어 파일)들을 보관할 디렉토리의 절대 경로
  - django는 서능을 위해 업로드 파일은 데이터베이스에 저장하지 않음
    - 실제 데이터베이스에 저장되는 것은 **파일의 경로**

  **[주의]** MEDIA_ROOT는 STATIC_ROOT와 반드시 다른 경로로 지정해야 함

- MEDIA_URL

  ```python
  #settings.py
  MEDIA_URL = '/media/'
  ```

  - MEDIA_ROOT에서 제공되는 미디어를 처리하는 URL
  - 업로드된 파일의 주소(URL)를 만들어주는 역할
    - 웹 서버 사용자가 사용하는 public URL
  - <u>비어있지 않은 값</u>으로 설정한다면 반드시 **slash(/)**로 끝나야함

  **[주의]** MEDIA_URL은 STATIC_URL과 반드시 다른 경로로 지정해야 함

#### 개발 단계에서 사용자가 업로드한 파일 제공하기

```python
#project/urls.py
from django.conf import settings
from django.conf.urls.static import static

urlpatterns=[
    path('admin/', admin.site.urls),
    path('appname/', include('appname.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
'''
사용자가 업로드 한 파일이 프로젝트에 업로드 되더라도, 실제로 사용자에게 제공하기 위해서는 업로드 된 파일의 URL이 필요
'''
```

- settings.MEDIA_URL: 업로드된 파일의 URL
- settings.MEDIA_ROOT: MEDIA_URL을 통해 참조하는 파일의 실제 위치

```bash
$ pip install Pillow
$ python manage.py makemigrations
$ python manage.py migrate
$ pip freeze > requirements.txt
```