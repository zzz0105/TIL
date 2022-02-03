# 객체지향 프로그래밍

> 파이썬은 모든 것이 **객체(object)**
>

## 객체지향 프로그래밍(OOP)

### OOP 기초

#### 객체

* 객체란? 클래스에서 정의한 것을 토대로 메모리(실제 저장공간)에 할당된 것

* 객체지향프로그래밍: 컴퓨터 프로그램을 객체들의 모임으로 파악.

  ​									 대상의 정보와 동작 -> S+V

##### 객체의 특징

* 타입(type): 어떤 연산자(operator)와 조작(method)이 가능한가?
* 속성(attribute): 어떤 상태(데이터)를 가지는가?
* 조작법(method): 어떤 행위(함수)를 할 수 있는가?
* 객체 = 속성(Attribute) + 기능(Method)

#### 객체지향 프로그래밍이란?

> 프로그램을 여러 개의 독립된 객체들과 그 객체들 간의 상호작용으로 파악하는 프로그래밍 방법

* 절차지향 프로그래밍: 데이터와 함수로 인한 변화. 들어온거 리턴해주고 결과를 저장해서 쓸 수 밖에 없는 것. 데이터는 흘러다닐 수 밖에 없다. (직접적으로 할 수 있는 것은 없다)
* 객체지향 프로그래밍: 데이터와 기능(메소드) 분리. 추상화된 구조(인터페이스). 메소드를 활용하여 데이터가 스스로 변화할 수 있다.

```python
#절차지향
a = [1, 2, 3]
a = sorted(a)
a = reversed(a)
def append(l,value):
    return l + [value]
a = append(a, 4)

#객체지향
a = [1, 2, 3]
a.sort()
a.reverse()
a.append(4)
```

* 현실 세계를 프로그램 설계에 반영(추상화)

```python
class Person:
    def greeting(self):
        print('안녕하세요' + self.name + '입니다.')

J = Person()	#괄호는 호출의 의미
J.name='J'
j.phone='010123456'
J.greeting()	#안녕하세요 J 입니다
```

```python
#클래스 붕어빵 틀, 인스턴스는 붕어빵
class Rectangle:
    def area(self):
        return self.x * self.y
r1=Rectangle()
r1.x=100
r1.y=200
r1.area()
#사각형 = class / r1 = 인스턴스
#사각형의 정보(가로길이, 세로길이) = 속성 / 사각형의 행동(넓이를 구한다) = 메소드
```

##### 객체지향의 장점 
  * 프로그램을 유연하고 변경이 용이하게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용됨
  * 프로그래밍을 더 배우기 쉽게 하고 소프트웨어 개발과 보수를 간편하게 하며, 보다 직관적인 코드 분석이 가능
##### 기본 문법
  * 클래스 정의     class MyClass:
      * 클래스: 객체들의 분류
  * 인스턴스 생성 my_instance = MyClass()
      * 객체의 틀(클래스)을 가지고 객체(인스턴스)를 생성한다.
    * 객체는 특정 타입의 인스턴스(instance)
      * 인스턴스는 하나하나의 실체/사례
  * 메소드 호출    my_instance.my_method()   클래스 내부에 정의된 함수
      * 메소드: 특정 데이터 타입/클래스의 객체에 공통적으로 적용 가능한 행위(함수)
  * 속성                 my_instance.my_attribute    값
      * 속성: 특정 데이터 타입/클래스들의 객체들이 가지게 될 상태/데이터를 의미
* 객체의 틀(클래스)을 가지고 객체(인스턴스)를 생성한다.
* 객체는 특정 타입의 인스턴스(instance)
  * 인스턴스는 하나하나의 실체/사례

#### 객체 비교하기

##### ==

* 동등한(equal)
* 변수가 참조하는 객체가 동등한(**내용이 같은**) 경우 True
* 두 객체가 같아 보이지만 실제로 동일한 대상을 가리키고 있다고 확인해준 것은 아님

##### is

* 동일한(identical)
* 두 변수가 **동일한 객체**를 가리키는 경우 True

```python
#1
a=[1,2,3]
b=[1,2,3]
a is b #F
a == b #T

#2
a=[1,2,3]
b = a
a is b #T
a == b #T

# a가 None인지 보려면?
if a is None:
```



### 인스턴스

#### 인스턴스 변수

* 인스턴스 변수란?
  * 인스턴스가 개인적으로 가지고 있는 속성(attribute)
  * 각 인스턴스들의 고유한 변수
* 생성자 메소드에서 self.<name>으로 정의
* 인스턴스가 생성된 이후 <instance>.<name>으로 접근 및 할당

#### 인스턴스 메소드

* 인스턴스 변수를 사용하거나, 인스턴스 변수에 값을 설정하는 메소드
* 클래스 내부에 정의되는 메소드의 기본
* 호출 시, 첫번째 인자로 **인스턴스 자기자신(self)이 전달됨**

##### self

* 인스턴스 자기자신
* 파이썬에서 인스턴스 메소드는 호출 시 첫번째 인자로 인스턴스 자신이 전달되게 설계
  * 매개변수 이름으로 self를 첫번째 인자로 정의
  * 다른 단어로 써도 작동하지만, 파이썬의 **암묵적인 규칙**

```python
class Person:
    def test(self):	#인스턴스 메서드. Person.test(p1)
        return self

#오류
p1 = Person		#인스턴스 작성
p1.test()		#TypeError: test()takes 0 positional arguments but 1 given

#따라서,,,
p1 = Person()
p1.test()		#<__main__.Person at (주소)>
p1				#<__main__.Person at (주소)>
Person.test(p1)	#내부적으로는 이렇게 실험
```

* What is 'self'?
  * 먼저, test(self)는 '정의하는 시점에서 반드시 첫번째 인자를 받도록 할 것이고, 이때 받은 첫번째 인자가 self이다.'라는 뜻. 내부적으로는 첫번째 인자에 p1을 넣어주는 것이다.
    * 왜 첫번째 인자로 넘겨줄까?
      * 인스턴스를 만드는 메서드이다보니, 그 안에서 인스턴스가 가지고 있는 값들을 자유롭게 쓰기 위해서 자기 자신을 첫번째로 넘겨주는 것이다.
      * 함수 안에서 인스턴스에 대한 조작들을 해야하는데 조작을 하려면 함수 정의 상 함수 인자로 넘겨주어야 하는데 그걸 파이썬이 자동으로 해준다.



#### 생성자 메소드

* 인스턴스 객체가 생성될 때 자동으로 호출되는 메소드
* 인스턴스 변수들의 초기값을 설정
  * 인스턴스 설정
  * __ init __ 메소드 자동 호출

```python
#1
class Person:
    def __init__(self):
        print('응애!')
p1 = Person()	#응애!
p2 = Person()	#응애!

#2
class Person:	
    def __init__(self, name, age):	#인스턴스 변수를 받아서 정의하기 위해 사용된다.
        self.name = name
        self.age = age
p1 = Person()	#TypeError. 2개의 위치 인자 안써서 error
# Person() 인스턴스를 만들면 __init__메서드가 호출되는구나
p2 = Person('A', 100)
print(p2.name, p2.age)	#A 100

#3
class Person:	
    def __init__(self, name, age=1):	
        self.name = name
        self.age = age
p3 = Person('A')	
print(p3.name)			# A 1
p3 = Person('B', 500)
print(p3.name, p3.age)	#B 500
```



#### 소멸자 메소드

* 인스턴스 객체가 소멸(파괴)되기 직전에 호출되는 인스턴스 메소드

```python
class Person:
    def __init__(self):
        print('응애')
    def __del__(self):
        print('으악...')
p1 = Person()	#응애
del p1	#으악...
```



#### 매직 메소드

* Double underscore(__)가 있는 메소드는 특수한 동작을 위해 만들어진 메소드로, 스페셜 메소드 혹은 매직 메소드라고 불림
* 특정 상황에 자동으로 불리는 메소드

```python
#1
class Person:
    def __init__(self, name, age, height):
        self.name=name
        self.age=age
        self.height=height
    def __gt__(self, other):	#greater than. 작은건 lesser than
        print(f'{self.name}: {self.age}살 / {other.name}:{other.age}살')
        return self.age > other.age
    def __len__(self):
        return self.height
p1 = Person('A', 100, 190)
p2 = Person('B', 10, 185)
p1 > p2	#A: 100살 / B: 10살		True
len(p1)	#190
p1			#<__main__.Person object in 주소1>
print(p1)	#<__main__.Person object in 주소1>
#2
class Person:
    def __init__(self, name, age, height):
        self.name=name
        self.age=age
        self.height=height
    def __str__(self):'<{self.name}>: {self.age}살'
        return f
    def __gt__(self, other):	#greater than. 작은건 lesser than
        print(f'{self.name}: {self.age}살 / {other.name}:{other.age}살')
        return self.age > other.age
    def __len__(self):
        return self.height
p1 = Person('C', 900, 200)
print(p1)	#<C>: 900살
```

##### 매직 메소드 예시

* 객체의 특수 조작 행위를 지정(함수, 연산자 등)

* __ str __: 해당 객체의 출력 상태를 지정

  * 프린트 함수를 호출할 때, 자동으로 호출
  * 어떤 인스턴스를 출력하면 __ str __의 return 값이 출력

* __ ge __: 부등호 연산자(>=, great equa)

  

### 클래스

#### 클래스 변수

* 한 클래스의 모든 인스턴스라도 똑같은 값을 가지고 있는 속성
  * 객체 = 속성+메소드
  * 클래스 = 변수 +메소드
  * 인스턴스 = 변수+메소드
* 클래스 이름 대신 인스턴스 이름을 쓰면 인스턴스 변수
* 클래스 속성(attribute): 한 클래스의 모든 인스턴스라도 똑같은 값을 가지고 있는 속성
  * 클래스 선언 내부에서 정의.  <classname> <name>으로 접근 및 할당

```python
class Circle:
    P1 = 3.14	#모든 서클에 해당하는 내용 -> 클래스 변수로. 인스턴스들이 다 쓸 수 있다.
    def __init__(self, r):
        self.r = r
    def area(self):
        return Circle.pi * self.r * self.r
Circle.pi#3.14
c1 = Circle(2)
c1.area	#12.56
c1.pi #3.14
```



### 메소드

#### 클래스 메소드

* 클래스가 사용할 메소드
* @classmethod 데코레이터를 사용하여 정의
  * 데코레이터: 함수를 어떤 함수로 꾸며서 새로운 기능을 부여
* 호출 시, 첫번째 인자로 클래스(cls)가 전달됨
* 클래스를 의미하는 cls 매개 변수를 통해 클래스를 조작

```python
class MyClass:
    @classmethod		
    def class_method(cls):#클래스가 조작할 애
        return cls
MyClass.class_method()	#__main__.MyClass
MyClass					#__main__.MyClass
#
class MyClass:#클래스 이름은 보통 대문자로 쓴다.
    var = 'Class 변수'
    @classmethod		
    def class_method(cls):#클래스가 조작할 애. 함수 메서드, 변수는 _를 활용해서 쓴다.
        print(cls.var)
        return cls
MyClass.class_method()	#Class 변수	__main__.MyClass
MyClass	
```



#### 스태틱 메소드

* 인스턴스 변수, 클래스 변수를 전혀 다루지 않는 메소드
  * 객체 상태나 클래스 상태를 수정할 수 없음
* 속성을 다루지 않고 단지 기능(행동)만을 하는 메소드를 정의할 때 사용
  * ex. 유틸리티, 작동을 할 때 사용
* 일반 함수처럼 동작하지만 클래스의 이름공간에 귀속됨.
  * 주로 해당 클래스로 한정하는 용도로 사용

```python
#1
class MyClass:
    
    @staticmethod
    def static_method(static):
        return static
MyClass.static_method()	#TypeError. 하나의 positional argument인 static 안씀(자동으로 넘어가지x)

#2
class MyClass:
    @staticmethod
    def static_method():
        return 'static'
MyClass.static_method()	#'static' 출력
```



```python
class MyClass:
    def instance_method(self):	#인스턴스 메서드
        return self
    
    @staticmethod
    def static_method():		#스태틱 메서드
        return ''
    
    @classmethod
    def class_method(cls):		#클래스 메서드
        print(cls.var)
        return cls
```

* 함수는 기본적으로 로컬 스코프 => 내부에서 활용하고 싶다면 파라미터로 받도록 정의.
* 인스턴스 메서드는 인스턴스를 조작하고 싶을 때. 함수 내부에 인스턴스를 던져주도록 설계되었다. 메서드를 정의할 때 self로 받도록 되어있다.
* 클래스 메서드는 클래스를 조작하고 싶을 때. 함수 내부에 클래스를 던져주도록 설계되어있다. 메서드를 정의할 때 cls로 받도록 되어있다. 
* 스태틱 메서드는 클래스나 인스턴스를 조작할 생각은 없는데 함수를 쓰고 싶을 때.



### 인스턴스와 클래스 간의 이름 공간(namespace)

* 클래스를 정의하면, 클래스와 해당하는 이름 공간 생성(안에 클래스 변수가 들어있다)
* 인스턴스를 만들면, 그 순간 init함수가 실행, 인스턴스 객체가 생성되고 이름 공간 생성
* 인스턴스에서 특정 속성에 접근하면, 인스턴스-클래스 순으로 탐색



```python
class Person():
    population = 0
    
    def __init__(self):
        Person.population += 1
        
    @classmethod
    def add_population(cls):
        cls.population += 1
    
    @staticmethod
    def get_phone_number(phone_number):
        return phone_number[:2]+ ')' + phone_number[:2]
    
    @staticmethod
    def math_pi():
        return 3.14
    
Person.get_phone_number('123456789')	#12)3456789
Person.math_pi()	#3.14
```



## 객체지향의 핵심개념

### 추상화

> 현실 세계를 프로그램 설계에 반영

```python
class Student:
    def __init__(self,name, age, gpa):
        self.name = name
        self.age = age
        self.gpa = gpa
    def talk(self):
        print(f'반갑습니다. {self.name}입니다')
    def study(self):
        self.gpa += 0.1
class Professor:
    def __init__(self, name, age, department):
        self.name = name
        self.age = age
        self.department = department
    def talk(self):
        print(f'반갑습니다. {self.name}입니다')
    def teach(self):
        self.age += 1
```

어떤 것을 만들고 싶을 때 만들어놓고 사람들이 쓸 수 있도록. 행동들을 각자 정의하는 것. 사용자는 밖에서 추상화된 class를 쓴다. 

### 상속

> 두 클래스 사이 부모 - 자식 관계를 정립하는 것

* 클래스는 상속이 가능하며, 모든 파이썬 클래스는 object를 상속받는다.
  * ex. class ChildClass(ParentClass):
* 부모클래스의 속성과 메소드가 자식 클래스에 상속되므로, 코드 재사용성이 높아짐.
* 하위 클래스는 상위 클래스에 정의된 속성, 행동, 관계 및 제약 조건을 모두 상속 받음.
  * 메소드 오버라이딩을 통해 자식 클래스에서 재정의 가능하다.
* 계층 구조를 가지고 갈 수 있다.
* 상속관계에서의 이름 공간은 인스턴스, 자식 클래스, 부모 클래스 순으로 탐색

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def talk(self):
        print(f'반갑습니다. {self.name}입니다.')
#메서드 재사용. Person클라스를 Professor와 Student가 상속받음. 
class Professor(Person):
    def __init__(self, name, age, department):
        self.name = name
        self.age = age
        self.department = department
class Student(Person):
    def __init__(self,name, age, gpa):
        self.name = name
        self.age = age
        self.gpa = gpa
    def talk(self):
        print(f'안녕하십니까. {self.name}입니다.')
p1 = Professor('교수', 49, 'A학과')
s1 = Student('학생', 20, 3.5)
#부모인 Person 클래스의 talk 메서드 활용
p1.talk()	#반갑습니다. 교수입니다.
s1.talk()	#안녕하십니까. 학생입니다.
```



#### 상속 관련 함수와 메소드

* issubclass(class, classinfo)
  * class가 classinfo의 subclass면 True
  * classinfo는 클래스 객체의 튜플일 수 있으며, classinfo의 모든 항목을 검사

```python
issubclass(bool, int)						#T
issubclass(float, int)						#F
issubclass(Professor, Person)				#T
issubclass(Professor, (Person, Student))	#T
```

* bool은 0이나 1이고 int는 정수형이니까 내부적으로 subclass로 볼 수 있다,

* float는 실수체계(정수+소수). 따라서 int보다는 큰 범위이니까 False

  +) int, float, str, list 모두 클래스이다. 또한 예외 계층 구조도 클래스. (상속 구조를 가지고 있음)

  

* isinstance(object, classinfo)

  * classinfo의 instance거나 subclass인 경우 True

```python
class Person():
    pass
class Professor(Person):
    pass
class Student(Person):
    pass
p1 = Person()
s1 = Student()
pro1 = Professor()
isinstance(p1, Person)	#T
isinstance(s1, Person)	#T
isinstance(p1, Student)	#F
```



* super()
  * 자식클래스에서 부모클래스를 사용하고 싶은 경우에 사용
  * 부모 클래스의 요소를 호출할 수 있음.

```python
class Person:
    def __init(self, name, age):
        self.name = name
        self.age = age
    def talk(self):
        print(f'반갑습니다. {self.name}입니다.')
class Student(Person):
    def __init(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id
Student('A', 20, '2022')	#<__main__.Student at 주소>
```



* ##### 상속 관련 함수와 메소드

  * mro 메소드(Method Resolution Order)

    * 해당 인스턴스의 클래스가 어떤 부모 클래스를 가지는지 확인하는 메소드.

    * 풀어나가는 순서.

    * 기존의 인스턴스 -> 클래스 순으로 이름 공간을 탐색하는 과정에서 상속 관계에 있으면 인스턴스 -> 자식 클래스 -> 부모 클래스로 확장

      



#### 상속, 클래스 메서드

```python
#1
class Person:
    population = 0
    
    @staticmethod
    def add_person():
        Person.population += 1
        
Person.add_population()
print(Person.population)	#3

class Student(Person):
    population = 0
    
Student.add_population()
print(Student.population)	#0 
#상속받은 형태가 static method고 이 안에 Person을 그대로 넣었기 떄문에 인구증가가 되지 않음

#2
class Person:
    population = 0
    
    @classmethod
    def add_person(cls):	#호출할 때 cls로 받겠다. 쓰기 위해서는 입력으로 넘겨야함
        cls.population += 1
        
class Student(Person):
    population = 0
    
Person.add_population()	
print(Person.population)	#1    
Student.add_population()
print(Student.population)	#1
```



#### 다중 상속

* 두개 이상의 클래스를 상속 받는 경우
* 상속 받은 모든 클래스의 요소를 활용 가능함
* 중복된 속성이나 메서드가 있는 경우 상속 순서에 의해 결정됨

```python
class Person:
    def __init__(self, name):
        self.name = name
    def greetin(self):
        return f'안녕, {self.name}'
class Mom(Person):
    gene = 'XX'
    def swim(self):
        return '엄마 수영'
class Dad(Person):
    gene = 'XY'
    def walk(self):
        return '아빠 걷기'
class FirstChild(Dad, Mom):
    def swim(self):
        return '첫째 수영'
    def cry(self):
        return '첫째 응애'
baby1 = FirstChild('아기')
baby1.cry()		#'첫째 응애'
baby1.swim()	#'첫째 수영'
baby1.walk()	#'아빠 걷기'
baby1.gene		#'XY' 다중상속에서는 앞의 클래스의 것을 가져오게 되어있다.
```



### 다형성

* Polymorphism: 여러 모양을 뜻하는 그리스어
* 동일한 메소드가 클래스에 따라 다르게 행동할 수 있음을 의미
* 즉, 서로 다른 클래스에 속해있는 객체들이 <u>동일한 메세지에 대해 다른 방식으로 응답될 수 있음</u>



##### 메소드 오버라이딩

* 상속 받은 메소드를 재정의
  * 클래스 상속 시, 부모 클래스에서 정의한 메소드를 자식 클래스에서 변경
  * 부모 클래스의 메소드 이용과 기본 기능은 그대로 사용하지만, 특정 기능을 바꾸고 싶을 때 사용
  * 상속받은 클래스에서 같은 이름의 메소드로 덮어씀
  * 부모 클래스의 메소드를 실행시키고 싶은 경우 super를 사용

```python
class Person:
    def __init__(self, name):
        self.name = name
    def talk(self):
        print('반갑습니다')
        
class Professor(Person):
    def talk(self):
        print('교수입니다')
        
class Student(Person):
    super().talk()
    print('학생입니다')
    
p1 = Professor('김')
p1.talk()	#교수입니다
s1 = Student('이')
s1.talk()	#반갑습니다		학생입니다.
```



### 캡슐화

* 객체의 일부 구현 내용에 대해 외부로부터의 직접적인 액세스를 차단
  * 예시: 주민등록번호
* 파이썬에서 암묵적으로 존재하지만, 언어적으로는 존재하지 않음

```python
class Person:
    def get_name(self):
        return self.name
    def set_name(self):
        self._name = name	#Protected 
p2 = Person()
p2.set_name('A')
p2.get_name()	#'A'
```



##### 접근제어자 종류

* Public Access Modifier
  * 언더바 없이 시작하는 메소드나 속성
  * 어디서나 호출이 가능, 하위 클래스 override 허용
  * 일반적으로 작성되는 메소드와 속성의 대다수 차지
* Protected Access Modifier
  * 언더바 1개로 시작하는 메소드나 속성
  * 암묵적 규칙에 이해 부모 클래스 내부와 자식 클래스에서만 호출 가능
  * 하위 클래스 override 허용
* Private Access Modifier
  * 언더바 2개로 시작하는 메소드나 속성
  * 본 클래스 내부에서만 사용이 가능
  * 하위클래스 상속 및 호출 불가능(오류)
  * 외부 호출 불가능(오류)



##### getter 메소드와 setter 메소드

* 변수에 접근할 수 있는 메소드를 별도로 생성
  * getter 메소드: 변수의 값을 읽는 메소드
    * @property 데코레이터 사용
  * setter 메소드: 변수의 값을 설정하는 성격의 메소드
    * @변수.setter 사용

```python
class Person:
    def __init__(self, age):
        self._age = age
    @property
    def age(self):
        return self._age
    @age.setter
    def age(self, new_age):
        if new_age <= 19:
            raise ValueError('Young')
            return
        self._age = new_age
        
p1 = Person(20)
print(p1.age)	#20
p1.age = 33
print(p1.age)	#33
p1.age = 19
print(p1.age)	#ValueError: Young
```

