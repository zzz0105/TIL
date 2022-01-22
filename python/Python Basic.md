# Python Basic

> 'Life is short, You need Python'

## 프로그래밍 언어: 3형식

* 얘네만 알면 알고리즘 가능!

1. 저장

2. 조건(if)

3. 반복(while)

+) SW개발 시 함수랑 클래스 지식 필요

**대/소문자, 띄어쓰기, 스펠링 꼭 지키기!**



### 1. 저장

> 자료구조: 효율적인 접근 및 수정을 가능케 하는 자료의 조직, 관리, 저장



#### 변수

>  박스에 값을 저장(할당)하는 것. 숫자, 글자(따옴표), 참/거짓을 저장할 수 있다.

```python
greeting = 'Guten Tag'	# 변수에 저장해서 한 방에 바꿀 수 있다

print(greeting)
print(greeting)
print(greeting)
```

```python
a = 'hello'
print(type(a))		#a의 타입을 알 수 있다.*타입 확인하는 습관!
print(a * 3)		#결과: hellohellohello

num = '3'			#3은 숫자, '3'은 글자
print(num * 3)		#결과: 333 / num에 저장된 3은 문자이기 때문에 다음과 같은 결과가 나옴
print(True, False)	#True, False 앞에 대문자 주의!
```



#### 리스트 

> 박스가 순서대로 여러 개가 붙어있다.

```python
dust = [58, 40, 70]
print(dust[1])		#40 출력. 첫 번째는 [0]
```

```python
lunch_box = ['소고기', '돼지고기', '양고기']
dinner_box = ['샐러드', '포케']
meal_box = [lunch_box, dinner_box]	#리스트 안의 리스트
print(meal_box)	#[['소고기', '돼지고기', '양고기'], ['샐러드', '포케']]
```

cf. list: 가변 시퀀스. 어떤 숫자든 들어갈 수 있다.

​	 range: 숫자의 불변 시퀀스.



#### 딕셔너리

> 견출지를 붙여보자. 변수와 값이 매핑된 것. Key: Value

```python
dust = {'영등포구': 40, '강남구': 50}	#문자열로 안쓰면 NameError 뜬다.
print['영등포구']	#40 출력. 40으로 영등포구를 찾을수는 없다.
```

```python
phone_book = {'pizza': '1234-4567', 'burger': '4458-7785'}	
	#번호에 ''씌우지 않으면 계산된 결과 나옴
print(phone_book)			#결과: 
print(phone_book['pizza'])	#결과: 1234-4567
```



cf. No such file or directory: 실행하고 싶은 파일의 위치에서 code로 오픈 열면 해결!

​	 ctrl+n: 새로운 파일 만들기 ctrl+s: 저장하기 ctrl+/: 긁어서 한 번에 주석처리하기

​	 저장하고 실행할 것!

​	  '>>>'이 앞에 있으면 exit()할 것. 앞에는 항상 '$'가 있어야 한다.

​	 **코드는 위에서 아래로, 오른쪽에서 왼쪽으로 할당. 안에서부터 밖으로 읽어나가면 좋다.**

​	 흐름 제어: 조건, 반복, ~~함수~~



### 2. 조건

```python
dust = 100
#shift + tab하면 tab 한 번 지워짐
#:, 들여쓰기(tab==띄어쓰기 4번/달라지면 오류남) 매우 중요! indentation 기반
#들여쓰기 일치하면 하나의 블럭으로 인식한다.
#우선순위 잘 모르겠으면 ()를 사용한다.
if dust > 150:		
    print('매우나쁨')		
elif dust > 80:			 #(80 < dust <= 150) == (80 < dust and dust <= 150)
    print('나쁨')				#순차적으로 검증하기 때문에 dust <=150은 쓸 필요 없다.
elif dust > 30:
    print('보통')
else:
    print('좋음')
```



### 3. 반복

#### while문

* 조건이 참일 때 계속 반복. 해당 조건이 False가 되면, 종료

* 조건이 True인 동안 반복적으로 실행되기에 종료조건이 반드시 필요

```python
greeting = 'Guten Tag!'
i=0
while i < 10:
    print(greeting)
    i+=1
```



#### for문

* 정해진 박스 내에서의 반복 시 사용. '통에서 가지고 있는 모든 것을 꺼낸다.'
* 정해진 범위를 반복하기에 종료 조건이 필요 없음 

```python
greeting = 'Guten Tag!'
for i in range(10):	#print(list(range(10)))은 [0, 1, 2, ... ,9]
    #i = ___
    print(greeting)	#Guten Tag!
```

```python
lunch_box = ['버거킹', '파파존스', '맥도날드']
for menu in lunch_box:		# 런치박스의 내용을 하나씩 menu에 넣어준다.
    #menu = ___
    print(menu)				#결과: 버거킹\n파파존스\n맥도날드
for i in range(len(lunch_box)):		# 런치박스의 길이만큼 숫자들을 나열시키고 하나씩 i에 인덱스를 넣어줌. 인덱스에 하나씩 접근
    print(lunch_box[i])	#결과: 버거킹\n파파존스\n맥도날드
```



### 4. 함수

> 어떤 작업을 반복하기 위해 사용. 로직을 어딘가에 담아서 계속 활용하고 싶을 때 사용

cf. CS는 추상화(abstraction)의 과정이다. 

```python
def add(a, b):		#def 함수이름(인자, 인자):
    return a + b	#a +b를 반환한다.
```

```python
def dust_quality(dust):	
    if dust > 150:		
    	print('매우나쁨')		
	elif dust > 80:			 
    	print('나쁨')				
	elif dust > 30:
    	print('보통')
	else:
    	print('좋음')
        
dust_quality(100)	#나쁨 출력
```

* 개발자 유우머: Error = (more code)^2 -> 따라서 적게 코드 쓰려고 함수 쓴다~



* Built-in function(내장함수)
  * print('hi'): 출력
  * abs(-3): 절댓값
  * len('hi'): 길이



* Module: 자주 쓰는 함수

```python
import random	#모듈 불러오기. 안쓰면 random에서 NameError 나온다.
#파일이름과 import함수가 같은 경우 내가 만든게 우선이긴 하나 오류가 뜰 것이다.
lunch_box = ['돼지고기', '소고기', '양꼬치', '회']
	# 점심 메뉴 리스트를 만들고 (최소 3개 아상)
today_menu = random.choice(lunch_box)	#하나를 랜덤으로 선택하여 저장
print(today_menu)
```

```python
import random		#random 모듈 불러오기
nums = range(1, 46)	#random(숫자 통, 개수)/리스트 이름 지을 때 복수형 쓰면 좋음
					#range(n, m)은 n 이상 m 미만
lotto = random.sample(nums, 6)	#1개를 뽑아도 리스트가 나온다.
sorted_lotto = sorted(lotto)	#뽑은 숫자를 오름차순으로 정렬한다.
print(sorted_lotto)
```

```python
def lotto_number_maker(n):						# n번 반복 
    for i in range(n):	
        print(random.sample(range(1, 46), 6))	# 로또 번호를 추출
lotto_number_maker(5)
```



* non Built-in function



cf. 변수: type    함수: input output (type)