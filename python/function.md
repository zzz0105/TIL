# 함수

## 왜 사용할까

* Decomposition: 기능을 분해하고 재사용 가능하게 만들기 위해
* Abstraction: 복잡한 내용을 모르더라도 사용할 수 있도록(블랙박스) 재사용성과 가독성, 생산성



## 함수기초

### 함수의 정의

* 함수(Function): 특정한 기능을 하는 코드의 조각. 매번 다시 작성하지 않고(코드 중복 방지) 필요 시에만 호출하여 간편히 사용. 
  * Error = (more code)**2
* 사용자 함수(Custom Function): 구현되어 있는 함수가 없는 경우 사용자가 직접 함수를 작성 가능

```python
def function_name(parameter):
    '''
    Documentation String(Doc-string)
    '''
    #code block. function body
    return returning_value
```



### 함수 기본 구조

#### 선언과 호출(define & call)

* def 키워드를 활용
* 들여쓰기를 통해 실행될 코드 블록(Function body) 작성함. Docstring은 선택적으로 작성.
* 함수는 parameter를 넘겨줄 수 있으며 동작 후에 return을 통해 결과값을 전달
* 함수 이름 -> 입력 이름 -> 로직-> 결과 순으로 생각하고 결정

* 함수는 함수명()으로 호출. 
  * parameter가 있는 경우, 함수명(값1, 값2, ...)로 호출

```python
#a를 n제곱하는 함수
def n_pow(a, n):
    result = a ** n
    return result
```



#### 입력(Input)

* Parameter: 함수를 실행할 때, 함수 내부에서 사용되는 식별자(이름). 함수 호출할 때 준 값을 받을 이름. ex. def foo(**a**):
* Argument: 함수를 호출할 때, 넣어주는 값. 함수에게 넣어주는 값 ex. foo(**a**)
  * 정의
    * 필수 Argument: 반드시 전달되어야 하는 argument
    * 선택 Argument(Default Argument): 값을 전달하지 않아도 되는 경우는 기본 값이 전달
      * 기본값을 지정하여 함수 호출 시 argument 값을 설정하지 않도록 함
      * 정의된 것보다 더 적은 개수의 argument들로 호출될 수 있다.
    * Positional Arguments Packing/Unpacking: 정해지지 않은 여러 개의 Argument 처리
      * *: 튜플
      * **: 딕셔너리
  * 호출
    * Positional Argument: 기본적으로 함수 호출 시 Argument는 위치에 따라 함수 내에 전달됨
    * Keyword Argument: 직접 변수의 이름으로 특정 Argument 전달. 
    

```python
def function(ham):		#parameter: ham
    return ham
function('spam')		#argument: spam

def add(x, y):
    return x + y
print(add(1, 2))		#Positional Argument. 내부에서 바인딩.x = 1 y = 2
print(add(y=2, x=1))	#Keyword Argument. 직접 x, y 값을 지정
print(add(x=1, 2))		#SyntaxError. 키워드로 지정하는 순간, 위치가 이미 의미x.
print(add(1, y=2))		#출력 가능. 

def add_z(x, y=0):		#Default Argument. 지정하지 않으면 y가 0으로 들어감.
    return x + y

def add_s(*args):		#팩을 사용하여 여러개 입력받음. args의 타입: 튜플
    for arg in args:
        print(arg)
        result = sum(arg)
    return result
        
def family(**kwargs):	#kwargs의 타입: 딕셔너리
    for key, value in kwargs:
        print(key, ':', value)
family(father = '고길동', monster = '둘리')	#father은 식별자. 따라서 ''안해야됨.
```

##### 함수를 만들 때 입출력 시 타입을 직접 지정할 수 있나? 

* 파이썬 = Dynamic type language.  a라는 변수에 string나 int등을 마음대로 넣을 수 있다. (static type language에는 java가 있다.)
* type-hinting(Python 3.5 버전 +)

```python
def greeting(name: str) -> str:
    return 'Hello' + name
print(greeting('oo'))	 #Hello oo
print(greeting(123))	 #실행은 됨.(동작 막기x) IDE에서 코드를 작성할 때 힌트가 뜬다.
```

##### Default argument에서 값을 설정하고 싶은 식별자를 뒤에 쓰는 게 좋은건가?

```python
#앞에서 설정하면 구조적으로 호출할 수 없다. 기본값 = 선택적으로 호출할 때 값을 넘겨라
def foo(a=1, c):	#SyntaxError: non-default argument follows default argument
    pass
foo(3)		#받는 사람 입장에서 c=3이라고 생각할 수 없다. 
```

##### 할당이 어떻게 되는건지?

```python
def foo(a,b):
    return a, b
foo(1, 2)		#a=1 b=2
foo(b=2, a=1)	#b=2 a=1
foo(1, 2, 3)	#위치로 대응x -> Error
```



#### 문서화(Doc-string)

```python
def foo():
    '''
    이 함수는 foo입니다.
    docstring으로 함수나 클래스의 기능을 설명합니다.
    '''
```

* 함수나 클래스의 설명
  * Jupyter notebook에서 함수에 커서를 놓고 shift+tab
* Naming Convention
  * 좋은 함수와 parameter 이름을 짓는 방법.
    * 상수 이름은 영문 전체를 대문자
    * 클래스 및 예외의 이름은 각 단어의 첫 글자만 영문 대문자
    * 이외 나머지는 소문자 또는 밑줄로 구분한 소문자 사용 -> 함수
  * 스스로를 설명
    * 함수의 이름만으로 어떠한 역할을 하는 함수인지 파악 가능해야 함
      * 인덱스의 경우 i, j, idx를 많이 쓴다.
    * 어떤 기능을 수행하는지, 결과 값으로 무엇을 반환하는지 등
    * 리스트나 튜플 같은 경우는 복수로 써주면 좋다
  * 약어 사용을 지양
    * 보편적으로 사용하는 약어를 제외하고 가급적 약어 사용을 지양

#### 범위(Scope)

* 함수는 코드 내부에 local scope를 생성하며, 그 외의 공간인 global scope로 구분
  * global scope: 코드 어디에서든 참조할 수 있는 공간
  * local scope: 함수가 만든 scope. 함수 내부에서만 참조 가능
* variable
  * global variable: global scope에 정의된 변수
  * local variable: local scope에 정의된 변수

```python
def ham():
    a = 'spam'
    return a
print(a)		#NameError가 뜬다. a가 global variable이 아니기 때문인다.
#함수의 기본은 local scope.
#블랙박스의 결과를 받아보고 싶으면 반환 값을 변수에 저장해서 사용하는 것
#블랙박스 밖으로 결과를 주고 싶으면 return해야한다.
```

* 변수 수명주기(lifecycle)
    * built-in scope: 파이썬이 실행된 이후부터 영원히 유지
    * global scope: 모듈이 호출된 시점 이후 혹은 인터프리터가 끝날 떄(.py)까지 유지
    * local scope: 함수가 호출될 때 생성되고, 함수가 종료될 떄(return)까지 유지
    
* 이름 검색 규칙(Name Resolution)

    * 파이썬에서 사용되는 이름들은 이름공간(namespace)에 저장되어 있음.
    * 아래와 같은 순서로 이름을 찾아나감. LEGB Rule이라고 부름
        * Local scope: 함수
        * Enclosed scope: 특정 함수의 상위 함수. 함수 내부에 함수 정의 가능
        * Global scope: 함수 밖의 변수, Import 모듈
        * Built-in scope: 파이썬 안에 내정되어 있는 함수 또는 속성

    ```python
    a = 0
    b = 1
    def enclosed():
        a = 10
        c = 3
        def local(c):
            print(a, b, c)		
        local(300)				#올라가면서 값을 찾아나간다.a=10,b=1.c=300
        print(a,b,c)			#enclosed 영역. a=10 b=1 c=3
    enclosed()
    print(a, b)					#global의 0, 1을 출력
    ```

    ```python
    print(sum)					#<built-in function sum>
    print(sum(range(2)))		#1
    sum=5						
    print(sum)					#5
    print(sum(range(2)))		#TypeError. LEGB 순서로 찾기 때문에 빌트인 함수 sum을 불러올 수 없다.
    ```

    * 즉, 함수 내에서는 바깥 Scope의 변수에 접근 가능하나 수정은 할 수 없음

* global문
  * 현재 코드 블록 전체에 적용되며, 나열된 식별자(이름)이 global variable임을 나타냄
    * global에 나열된 이름은 같은 코드 블록에서 global 앞에 등장할 수 었음
    * global에 나열된 이름은 parameter, for 루프 대상, 클래스/함수 정의 등으로 정의되지 않아야 한다.

```python
#함수 내부에서 글로벌 변수 변경하기
a = 10
def func():
    global a
    a = 3
print(a)	#10
func()
print(a)	#3
#global scope에서 global 변수 값이 변경. 
#global 키워드를 사용하지 않으면, Local scope에 a 변수가 생성(쓰기 전에 선언을 해야한다. 그렇지 않고 쓰면 SyntaxError)
```

* nonlocal
  * global을 제외하고 가장 가까운 (둘러 싸고 있는) scope의 변수를 연결하도록 함
    * nonlocal에 나열된 이름은 같은 코드 블록에서 nonlocal 앞에 등장할 수 없음
    * nonlocal에 나열된 이름은 parameter, for 루프 대상, 클래스/함수 정의 등으로 정의되지 않아야 함
  * global과는 달리 이미 존재하는 이름과의 연결만 가능함.

```python
x = 0
def func1():
    x = 1
    def func2():
        nonlocal x
        x = 2
    func2()
    print(x)			
func1()				#2
print(x)			#0
#enclosed scope(func1)의 변수 x의 변경
```

* 주의

  * *기본적으로 함수에서 선언된 변수는 Local scope에 생성되며, 함수 종료 시 사라짐

  * *해당 scope에 변수가 없는 경우 LEGB rule에 의해 이름을 검색함

    * *변수에 접근은 가능하지만, 해당 변수를 수정할 수는 없음
    * 값을 할당하는 경우 해당 scope의 이름공강간에 새롭게 생성되기 때문
    * 단, 함수 내에서 필요한 상위 scope 변수는 argument로 넘겨서 활용할 것(클로저 제외)
      * 클로저: 어떤 함수 내부에 중첩된 형태로써 외부 scope 변수에 접근 가능한 함수

  * 상위 sxope에 있는 변수를 수정하고 싶다면 global, nonlocal 키워드를 활용 가능

    -> 사용 시 함수 != 블랙박스. 블랙박스 깨버리는 것

    * 단, 코드가 복잡해지면서 변수의 변경을 추적하기 어렵고, 예기치 못한 오류가 발생
    * 가급적 사용하지 않는 것을 권장하며, 함수로 값을 바꾸고자 한다면 항상 argument로 넘기고 리턴 값을 사용하는 것을 추천

* 범위 확인하기
  * globals()와 locals()
    * namespace(global, local, builtin)를 딕셔너리(dict)로 정리
      * locals(): locals()가 실행되는 함수 내의 local namespace들을 정리
      * globals(): global, local, built-in 정보 모두 dict 형태로 정리 {'변수': 값}



#### 결과값(Output)

* 반드시 하나의 객체 반환!

* Void function

  * 명시적인 return 값이 없는 경우, 코드블록 마지막 줄에서 None을 반환하고 종료

```python
#print는 return 값 없다. print는 출력을 위한 함수, return은 함수 안에서만 사용되는 키워드.코드 작성하기 위해 함수 반환. 블랙박스에 input 넣어서 output을 받는다.
'''REPL(Read-Eval-Print Loop) 환경(ex. 주피터 노트북)에서는 마지막으로 작성된 코드의 리턴값을 보여주므로 똑같이 동작하는 것으로 착각할 수 있다.'''
a = print('hello')
print(a)	#결과값: None
```

* Value returning function
  * 함수 실행 후, return문을 통해 값 변환
  * return을 하게 되면, 값 반환 후 함수가 바로 종료
  * 한 함수에서 return값 2개 반환한다고 코드를 작성하면?
    * 위에 하나만 return한다. return 만나면 코드 종료이기 때문에.
    * 두 개 이상의 값을 반환하려면 콤마를 사용해 return하면 된다. -> return x, y (튜플 하나로 반환)

```python
def rectangle(width, height):	#너비와 높이 입력
    size = width * height
    around = 2(width + height)
    return size, around			#하나의 튜플로 반환
```



## 함수 응용

### 내장 함수(Built-in Functions)

* 파이썬 인터프리터에는 항상 사용할 수 있는 많은 함수와 형(type)이 내장되어 있음

#### map

```python
map(function, iterable)
#예시) 띄어쓰기로 구분된 입력을 int형으로 한번에 바꾸기
#split()으로 입력을 찢어서 하나씩 리스트로 들어옴. (split()의 default값 = 공백)
#그리고 문자열 리스트를 int 리스트로 map으로 한방에 바꿔줌
n, m = map(int,input().split())
#튜플처럼 리스트도 하나씩 저장해준다.
print(n, m)
```

* 순회 가능한 데이터 구조(iterable)의 모든 요소에 함수(function)을 적용하고, 그 결과를 map object로 반환. (cf. enumerate도 enumerate object로 반환됨)
* 리스트 형 변환을 통해 결과를 직접 확인.
  * map의 결과는 리스트 [1,2,3]을 그대로 주는게 아니고 1  /  2  /  3 이렇게 하나씩 뽑아서 준다. 따라서 리스트로 형 변환해서 본다.



#### filter

```python
filter(function, iterable)
#
def odd(n):
    return n % 2
numbers = [1, 2, 3]
result = filter(odd, numbers)
```

* 순회 가능한 데이터구조(iterable)의 모든 요소에 함수(function) 적용하고, 그 결과가 True인 것들을 filter object로 반환
* 리스트 형변환을 통해 결과 직접 확인



#### zip

```python
zip(*iterables)
#
girls = ['a', 'b']
boys = ['c', 'd']
pair = zip(girls, boys)
list(pair)	#[('a', 'c'), ('b', 'd')]
```

* 복수의 iterable을 모아 튜플을 원소로 하는 zip object를 반환



#### lambda

```python
lambda [parameter] : 표현식
#삼각형 넓이를 구하는 공식
def triangle_area(b, h):
    return 0.5 * b * h
#이를 람다 함수를 이용해서 쓰면 다음과 같다.
triangle_area = lambda b, h : 0.5 * b *h
triangle_area(5, 6)

#4까지 홀수를 출력
print(list(filter(lambda n : n % 2, range(5))))
```

* 표현식을 계산한 결과값을 반환하는 함수. 이름이 없는 함수여서 익명함수라고도 불림
* return 문을 가질 수 없다. 간편 조건문 외 조건문이나 반복문을 가질 수 없음
* 함수를 정의해서 사용하는 것보다 간결하게 사용 가능.
  * 한 번만 쓸껀데? 하면 lambda 쓰면 좋다.
* def를 사용할 수 없는 곳에서도 사용 가능



### 재귀 함수(recursive function)

```python
#Factorial = n!
def factorial(n):
    if n == 0 or n ==1:
        return 1
    else:
        return n * factorial(n-1)
factorial(4)
# 반복문으로도 작성 가능
def fact(n):
    result = 1
    while n > 1:
        result *= n
        n -= 1
    return result
```

* 자기 자신을 호출하는 함수
* 무한한 호출을 목표로 하는 것이 아니며, 알고리즘 설계 및 구현에서 유용하게 활용
  * 알고리즘 중 재귀 함수로 로직을 표현하기 쉬운 경우가 있음(ex. 점화식)
  * 변수의 사용이 줄어들며, 코드의 가독성이 높아짐
* *1개 이상의 base case(종료되는 상황)가 존재하고, 수렴하도록 작성
* 주의사항
  * 재귀함수는 **base case**에 도달할 때까지 함수를 호출함
  * 메모리 스택이 넘치게 되면(stack overflow) 프로그램이 동작하지 않게 됨
  * 파이썬에서는 최대 재귀 깊이(maximun recursion depth)가 1000번으로, 호출 횟수가 이를 넘어가게 되면 Recursion Error 발생
* 반복문과 재귀 함수 비교
  * 알고리즘 자체가 재귀적인 표현이 자연스러운 경우 재귀함수를 사용함.
  * 재귀 호출은 변수 사용을 줄여줄 수 있음
  * 재귀 호출은 입력 값이 커질수록 연산 속도가 오래 걸림



## 모듈과 패키지

```python
import module							#pprint.pprint로 쓴다
from module import var, function, Class	#pprint로 쓸 수 있다.
from module import *	# 전부 import

from package import module
from package.module import var, function, Class
```

* 모듈
  * 다양한 기능을 하나의 파일로 만든 소스코드
  * 특정 기능을 하는 코드를 파이썬 파일(.py) 단위로 작성한 것
* 패키지
  * 다양한 파일을 하나의 폴더로 만들어 관리
  * 특정 기능과 관련된 여러 모듈의 집합
  * 패키지 안에는 또 다른 서브 패키지를 포함

* 라이브러리
  * 다양한 패키지를 하나의 묶음으로 만듬

### 파이썬 표준 라이브러리(PSL)

* 파이썬에 기본적으로 설치된 모듈과 내장 함수
  * [`파이썬 자습서`](https://docs.python.org/ko/3.9/tutorial/index.html)

### 파이썬 패키지 관리자(pip)

* PyPI(Python Package Index)에 저장된 외부 패키지들을 설치하도록 도와주는 채키지 관리 시스템
* 다양한 파이썬 프로젝트에서 사용됨. ex. PyTorch

#### 명령어

* 패키지 설치
  * 최신 버전/특정 버전/최소 버전을 명시하여 설치할 수 있음
  * 이미 설치되어 있는 경우 이미 설치되어 있음을 알리고 아무것도 하지 않음
* 패키지 삭제
  * pip는 패키지를 업그레이드 하는 경우 과거 버전을 자동으로 지워줌
* 패키지 목록 및 특정 패키지 정보
* 패키지 freeze
  * 설치된 패키지의 비슷한 목록을 만들지만, pip install에서 활용되는 형식으로 출력
  * 해당 목록을 requirements.txt(관습)으로 만들어 관리함.
* 패키지 관리하기
  * 명령어들을 통해 패키지 목록을 관리[1]하고 설치할 수 있음[2]
  * 일반적으로 패키지를 기록하는 파일의 이름은 requirements.txt로 정의함

```bash
#패키지 설치
$ pip install SomePackage
$ pip install SomePackage==1.0.5
$ pip install 'SomePackage>=1.0.4'	# $ 사인은 bash, cmd 환경에서 사용되는 명령어

#패키지 삭제
$ pip uninstall SomePackage

#패키지 목록. 눈으로 보는 것
$ pip list

#특정 패키지 정보
$ pip show SomePackage

#패키지 freeze. 지금 설치되어있는 패키지들의 버전을 매핑. 같이 프로젝트를 하는 사람에게 공유
$ pip freeze

#패키지 관리하기
$ pip freeze > requirements.txt		#[1]공유하는 법
$ pip install -r requirements.txt	#[2]requirements.txt로 한방에 정리하는 법
```



### 사용자 모듈과 패키지

#### 모듈 만들기 

* check.py에 짝수를 판별하는 함수(even)와 홀수를 판별하는 함수(odd)를 만들고 check 모듈을 활용해보시오.
* 모듈을 활용하기 위해서는 import 문을 통해 가져옴

```python
#check.py
NAME = 'lion'
def odd(n):
    return n % 2	#(n%2==1) 이렇게 써도 됨
def even(n):
    return ~(n % 2)	#(n%2==0) 이렇게 써도 됨

#활용1
import check
print(check.NAME)	#lion
print(check.odd(2))	#False

#활용2
from check import NAME
print(NAME)			#lion

#활용3
from check import *
print(NAME)			#lion
print(odd(1))		#True
```

*  이미 만들어진 모듈과 이름이 같도록 모듈을 만들 수 있다. (변수 이름을 메서드 이름과 똑같이 만들어서 쓰는 것과 동일) 그러나 이름을 찾는 순서는 결국 LEGB rule이므로 만드는 순간 built-in 함수 못쓴다. 자체모듈보다 내가 만든 함수 먼저 찾는다.



#### 패키지

* 패키지는 여러 모듈/하위 패키지로 구조화
  
  * 활용 예시: package.module
* 모든 폴더에는 _ _ init _ _.py를 만들어 패키지로 인식
  
  * Python 3.3부터는 파일이 없어도 되지만, 하위 버전 호환 및 프레임워크 등에서의 동작을 위해 파일을 생성하는 것을 권장
  
  

#### 패키지 만들기

* 수학과 통계 기능이 들어간 패키지를 아래와 같이 구성

  * math의 tools: 자연 상수 e, 원주율 pi 값, 최대값을 구하는 my_max 함수

  * statics의 tools: 평균을 구하는 mean 함수

  * 폴더 구조(폴더에 _ _ init _ _.py 만들어 구분한다)

    ```bash
    my_package/
    	_ _ init _ _.py
    	math/
    		_ _ init _ _.py
    		tools.py
    	statistics/
    		_ _ init _ _.py
    		tools.py
    ```

    

```python
#math.py
PI = 3.14152
E = 2.71

def add(a, b):
    return a + b
def minus(a, b):
    return a - b


#01.py로 활용
from my_package.math import math
print(math.PI)			#출력: 3.141592
```







## 가상 환경

* 파이썬 표준 라이브러리가 아닌 외부 패키지와 모듈을 사용하는 경우 모두 pip를 통해 설치를 해야함
* 복수의 프로젝트를 하는 경우 버전이 상이할 수 있음
  * 과거 외주 프로젝트 - django 버전 2.x
  * 신규 회사 프로젝트 - django 버전 3.x
* 이러한 경우 가상환경을 만들어 프로젝트 별로 독립적인 패키지를 관리할 수 있다.

#### venv

* 가상 환경을 만들고 관리하는데 사용되는 모듈(Python 버전 3.5부터)
* 특정 디렉토리에 가상 환경을 만들고, 고유한 파이썬 패키지 집합을 가질 수 있음
  * 특정 폴더에 가상 환경이(패키지 집합 폴더 등) 있고
  * 실행환경(ex. bash)에서 가상환경을 활성화시켜
  * 해당 폴더에 있는 패키지를 관리/사용함

#### 가상환경 생성

* 가상환경을 생성하면, 해당 디렉토리에 별도의 파이썬 패키지가 설치됨

```bash
#가상환경 생성
$ python -m venv <폴더명>

#가상환경 활성화. 사용하면 뒤에 (venv) 따라다님. venv 폴더별로 고유한 프로젝트가 설치됨
$ source venv/Scripts/activate
```

#### 가상환경 활성화/비활성화

* 명령어를 통해 가상환경을 활성화

  * <venv>는 가상환경을 포함하는 디렉토리의 경로

  * 가상환경 비활성화는 $ deactivate 명령어를 사용

