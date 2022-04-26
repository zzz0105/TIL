# JavaScript

## Intro

### 브라우저(browser)

> 브라우저(BOM)과 그 내부의 문서(DOM)를 조작하기 위해 ECMAScript(JS)를 학습

- URL로 웹(WWW)을 탐색하며 서버와 통신하고, HTML 문서나 파일을 출력하는 GUI 기반의 소프트웨어
- 인터넷의 컨텐츠를 검색 및 열람하도록 함
- "웹 브라우저"라고도 함
- 주요 브라우저
  - Google, Chrome, Mozilla Firefox, Microsoft Edge, Opera, Safari

### JavaScript의 필요성

- 브라우저 화면을 '동적'으로 만들기 위함
- 브라우저를 조작할 수 있는 유일한 언어

### 브라우저에서 할 수 있는 일

- DOM(Document Object Model) 조작: 문서(HTML) 조작
  - HTML, XML과 같은 문서를 다루기 위한 프로그래밍 인터페이스
  - 문서를 구조화하고, 구조화된 구성 요소를 하나의 객체로 취급하여 다루는 논리적 트리 모델
  - 문서가 객체(object)로 구조화되어 있으며 key로 접근 가능
  - 단순한 속성 접근, 메서드 활용뿐만 아니라 프로그래밍 언어적 특성을 활용한 조작 가능
  - 주요 객체
    - window: DOM을 표현하는 창(브라우저 탭). 최상위 객체(작성 시 생략 가능)
    - document: 페이지 컨텐츠의 Entry Point 역할을 하며, \<head>, \<body> 등과 같은 수많은 다른 요소들을 포함
    - navigator, location, history, screen
  - DOM - 조작
    - JavaScript로 document의 title을 바꿀 수 있다 
  - DOM - 해석
    - 파싱(Parsing)
      - 구문 분석, 해석
      - 브라우저가 문자열을 해석하여 DOM Tree로 만드는 과정
- BOM(Browser Object Model) 조작: navigator, screen, location, frames, history, XHR
  - 자바스크립트가 브라우저와 소통하기 위한 모델
  - 브라우저의 창이나 프레임을 추상화해서 프로그래밍적으로 제어할 수 있도록 제공하는 수단
    - 버튼, URL 입력창, 타이틀 바 등 브라우저 윈드우 및 웹 페이지 일부분을 제어 가능
  - window 객체는 모든 브라우저로부터 지원받으며 브라우저의 창(window)을 지칭 
- JavaScript Core(ECMAScript): Data Structure(Object, Array), Conditionsal Expression, Iteration
  - 브라우저(BOM & Tree)를 조작하기 위한 명령어 약속(언어)
  - ECMA(ECMA International): 정보 통신에 대한 <u>표준을 제정하는 비영리 표준화 기구</u>
  - ECMAScript는 ECMA에서 ECMA-262 규격에 따라 정의한 언어
    - ECMA-262 : 범용적인 목적의 프로그래밍 언어에 대한 명세
  - ECMAScript6는 ECMA에서 제안하는 6번째 표준 명세를 말함
    - [참고] ECMASciprt6의 발표 연도에 따라 ECMAScript2015라고도 불림

### 세미콜론

- 자바스크립트는 **세미콜론을 선택적으로 사용 가능**
- 세미콜론이 없으면 ASI(자동 세미콜론 삽입 규칙)에 의해 <u>자동으로 세미콜론이 삽입됨</u>

### 코딩 스타일 가이드

- 코딩 스타일의 핵심은 **합의된 원칙과 일관성**
  - 절대적인 하나의 정답은 없으며, 상황에 맞게 원칙을 정하고 일관성 있게 사용하는 것이 중요
- 코딩 스타일은 코드의 **품질에 직결되는 중요한 요소**
  - 코드의 유지보수 또는 팀원과의 커뮤니케이션 등 개발 과정 전체에 영향을 끼침



## 변수와 식별자

### 식별자 정의와 특징

- 식별자(identifier)는 변수를 구분할 수 있는 변수명을 말함
- 식별자는 반드시 문자, 달러($) 또는 밑줄(_)로 시작
- 대소문자를 구분하며, 클라스명 외에는 모두 소문자로 시작
- 예약어(for, if, function 등) 사용 불가능

### 식별자 작성 스타일

- 카멜 케이스(**camelCase**, lower-camel-case): 변수, 객체, 함수에 사용
  - 두번째 단어의 첫 글자부터 대문자
- 파스칼 케이스(**PascalCase**, upper-camel-case): 클래스, 생성자에 사용
  - 모든 단어의 첫번째 글자를 대문자로 작성
- 대문자 스네이스케이스(**SNAKE_CASE**): 상수(개발자의 의도와 상관없이 변경될 가능성이 없는 값을 의미)에 사용
  - 모든 단어 대문자 작성 & 단어 사이에 언더스코어 삽입

### 변수 선언 키워드

#### let

- 재할당 할 예정인 변수 선언 시 사용
- 변수 재선언 불가능
- [블록 스코프](#블록-스코프)

#### const

- 재할당 할 예정이 없는 변수 선언 시 사용
- 변수 재선언 불가능
- [블록 스코프](#블록-스코프)

##### 블록 스코프

```javascript
let x = 1
if (x == 1){
    let x = 2
    console.log(x)	//2
}
console.log(x)		//1
```

- if, for, 함수 등의 **중괄호 내부**를 가리킴
- 블록 스코프를 가지는 변수는 **블록 바깥에서 접근 불가능**

[참고] 선언, 할당, 초기화

```javascript
let foo				//선언
console.log(foo)	//undefined

foo = 11			//할당
console.log(foo)	//11

let bar = 0			//선언 + 할당
console.log(bar)	//0

let num = 10		//할당
num = 50			//재할당
console.log(num)	//50
let num = 70		//재선언 -> 불가
```

- 선언: **변수를 생성**하는 행위 또는 시점
- 할당: **선언된 변수에 값을 저장**하는 행위 또는 시점
- 초기화: **선언된 변수에 <u>처음으로</u> 값을 저장**하는 행위 또는 시점

[참고] var

```javascript
var number = 10		//선언 및 초기값 할당
var number = 50		//재할당

console.log(number)	//50
```

- **var로 선언한 변수는 재선언 및 재할당 모두 가능**

- ES6 이전에 변수를 선언할 때 사용되던 키워드

- **호이스팅되는 특성**으로 인해 예기치 못한 문제 발생 가능

  - 따라서 ES6 이후부터는 var 대신 <u>const와 let을 사용하는 것을 권장</u>

  - **호이스팅**

    ```javascript
    console.log(username)	//undefined
    var username = '홍길동'
    
    console.log(email)		//Uncaught ReferenceError
    let email = 'gildong@naver.com'
    
    console.log(age)		//Uncaught ReferenceError
    const age =  50
    ```

    - 변수를 **선언 이전에 참조할 수 있는 현상**
    - **변수 선언 이전의 위치에서 접근 시 undefined를 반환**

- 함수 스코프

  ```javascript
  function foo(){
      var  x = 5
      console.log(x)	//5
  }
  
  console.log(x)	//ReferenceError: x is not defined
  ```

  - **함수의 중괄호 내부**를 가리킴
  - 함수 스코프를 가지는 변수는 **함수 바깥에서 접근 불가능**

| 키워드 | 재선언 | 재할당 | 스코프          | 비고         |
| ------ | ------ | ------ | --------------- | ------------ |
| let    | X      | O      | 블록 스코프     | ES6부터 도입 |
| const  | X      | X      | 블록 스코프     | ES6부터 도입 |
| var    | O      | O      | **함수 스코프** | 사용X        |



## 데이터 타입

### 데이터 타입 종류

- 자바스크립트의 모든 값은 특정한 데이터 타입을 가짐

- 크게 원시 타입과 참조타입으로 분류됨

  | 원시 타입                                  | 참조 타입                                  |
  | ------------------------------------------ | ------------------------------------------ |
  | **객체가 아닌** 기본 타입                  | **객체** 타입의 자료형                     |
  | 변수에 **해당 타입의 값이 담김**           | 변수에 해당 **객체의 참조 값이 담김**      |
  | 다른 변수에 복사할 때 **실제 값이 복사됨** | 다른 변수에 복사할 때 **참조 값이 복사됨** |

#### 원시 타입

##### 숫자 타입

- **정수, 실수 구분 없는 하나의 숫자 타입**
- **부동소수점 형식**을 따름
- [참고] NaN(Not-A-Number)
  - **계산 불가능**한 경우 **반환**되는 값
    - ex. 'Angel'/1004 => NaN

##### 문자열 타입

```javascript
const firstName = 'Gildong'
const lastName  = 'Hong'
const fullName = `${firstName} ${lastName}`

console.log(fullName)	//Gildong Hong
```

- **텍스트 데이터**를 나타내는 타입
- 16비트 유니코드 문자의 집합
- **작은따옴표** 또는 큰 따옴표 <u>모두 가능</u>
- **템플릿 리터럴**
  - ES6부터 지원
  - 따옴표 대신 backtick(``)으로 표현
  - ${ expression } 형태로 표현식 삽입 가능

##### undefined

- 변수의 **값이 없음**을 나타내는 데이터 타입
- 변수 선언 이후 **직접 값을 할당하지 않으면**, **자동으로** <u>undefined가 할당됨</u>

##### null

- 변수의 **값이 없음을 의도적으로 표현**할 때 사용하는 데이터 타입
- [참고] null 타입과 typeof 연산자
  - **typeof** 연산자: **자료형 평가를 위한 연산자**
  - **null 타입은 원시 타입에 속하지만, typeof 연산자의 결과는 객체로 표현됨**

##### [참고] undefined 타입과 null 타입 비교

| undefined                                                    | null                                      |
| ------------------------------------------------------------ | ----------------------------------------- |
| **빈 값**을 **표현**하기 위한 데이터 타입                    | **빈 값**을 **표현**하기 위한 데이터 타입 |
| **변수 선언 시 아무 것도 할당하지 않으면, <br />자바스크립트가 자동으로 할당** | **개발자가 의도적으로 필요한 경우 할당**  |
| typeof 연산자의 결과는 **undefined**                         | typeof 연산자의 결과는 **object**         |

##### Boolean 타입

- **논리적 참 또는 거짓**을 나타내는 타입

- true 또는 false로 표현

- 조건문 또는 반복문에서 유용하게 사용

  - [참고] 조건문 또는 반복문에서 boolean이 아닌 데이터 타입은 **자동 형변환 규칙**에 따라 true 또는 false로 변환됨

    - 자동 형변환 규칙

      | 데이터 타입 | 거짓       | 참               |
      | ----------- | ---------- | ---------------- |
      | Undefined   | 항상 거짓  | X                |
      | Null        | 항상 거짓  | X                |
      | Number      | 0, -0, NaN | 나머지 모든 경우 |
      | String      | 빈 문자열  | 나머지 모든 경우 |
      | Object      | X          | 항상 참          |

      조건문 또는 반복문에서 표현식의 결과가 참/거짓으로 판별되는 경우 발생

#### 참조 타입(Reference type)

- [함수](#함수), [배열](#배열), [객체](#객체)



## 연산자

### 할당 연산자

```javascript
let x = 0

x++
console.log(x)	//1

x += 1
console.log(x)	//2
```

- 오른쪽에 있는 피연산자의 평가 결과를 왼쪽 피연산자에 할당하는 연산자
- 다양한 연산에 대한 단축 연산자 지원
- [참고] Increment 및 Decrement 연산자
  - Increment(++): 피연산자의 값을 1 증가시키는 연산자
  - Decrement(--): 연산자의 값을 1 감소시키는 연산자
  - ++, -- 보다 += 또는 -=와 같이 더 분명한 표현으로 적을 것을 권장

### 비교 연산자

```javascript
const numA = 2
const numB = 3
console.log(numA < numB)	//true
```

- 피연산자들(숫자, 문자, Boolean 등)을 비교하고 결과값을 boolean으로 반환하는 연산자
- 문자열은 유니코드 값을 사용하며 표준 사전 순서를 기반으로 비교
  - ex. 알파벳끼리 비교할 경우
    - 알파벳 순서상 후순위가 더 크다
    - 소문자가 대문자보다 더 크다

### 동등 비교 연산자(==)

```javascript
const a = 100
const b = '100'
console.log(a==b)	//true

const c = 1
const d = true
console.log(c==d)	//true

//자동 타입 변환 예시
console.log(a + b)	//100100
console.log(c + d)	//2
```

- 두 피연산자가 같은 값으로 평가되는지 비교 후 **boolean 값을 반환**
- 비교할 때 <u>암묵적 타입 변환</u>을 통해 타입을 일치시킨 후 같은 값인지 비교
- 두 피연산자가 <u>모두 객체</u>일 경우 **메모리의 같은 객체를 바라보는지 판별**
- 예상치 못한 결과가 발생할 수 있으므로 **특별한 경우를 제외하고 사용하지 않음**

### 일치 비교 연산자(===)

```javascript
const a = 100
const b = '100'
console.log(a==b)	//false

const c = 1
const d = true
console.log(c==d)	//false
```

- 두 피연산자가 같은 값으로 평가되는지 비교 후 boolean 값을 반환
- **엄격한 비교**가 이뤄지며 <u>암묵적 타입 변환이 발생하지 않음</u>
  - 엄격한 비교: 두 비교 대상의 **타입과 값 모두 같은지 비교**하는 방식
- 두 피연산자가 <u>모두 객체</u>일 경우 **메모리의 같은 객체를 바라보는지 판별**

### 논리 연산자

```javascript
console.log(1 && 0)		//0
console.log(4 && 7)		//7
console.log('' && 3)	//''
console.log(4 || 7)		//4
console.log('' || 3)	//3
console.log(!'hi')		//false
```

- 세 가지 논리 연산자로 구성
  - **and** 연산은 '**&&**' 연산자를 이용
  - **or** 연산은 '**||**' 연산자를 이용
  - **not** 연산은 '**!**' 연산자를 이용
- 단축 평가 지원
  - 예시
    - false && true => false
    - true || false => true

### 삼항 연산자

```javascript
console.log(true? 1 : 2)	//1
console.log(false? 1 : 2)	//2
```

- 세 개의 피연산자를 사용하여 **조건에 따라 값을 반환**하는 연산자
- 가장 왼쪽의 **조건식이 참**이면 **콜론(:) 앞의 값**을 사용하고 그렇지 않으면 콜론(:) 뒤의 값을 사용
- 삼항 연산자의 결과 값이기 때문에 **변수에 할당 가능**
- [참고] 한 줄에 표기하는 것을 권장한다



## 조건/반복

### 조건문의 종류와 특징

#### 'if' statement

```javascript
if (condition){
    //do something
} else if (condition){
    //do something
} else {
    //do something
}
```

- 조건 표현식의 결과값을 **Boolean 타입으로 변환 후 참/거짓을 판단**
- 조건은 **소괄호** 안에 작성
- 실행할 코드는 **중괄호** 안에 작성
- 블록 스코프 생성

#### 'switch' statement

```javascript
switch(expression){
    case 'first value':{
        //do something
        break
    }
    case 'second value':{
        //do something
        break
    }
    [default:{
     	//do something
     }]
}
```

- 조건 표현식의 결과값이 **어느 값(case)에 해당하는지 판별**
  - 표현식의 결과값과 case 문의 오른쪽 값을 비교
- [참고] 주로 특정 변수의 값에 따라 조건을 분기할 때 활용
  - 조건이 많아질 경우 if 문보다 가독성이 나을 수 있음
- break 및 default 문은 선택적으로 사용 가능
- break 문이 없는 경우 **break 문을 만나거나 default 문을 실행할 때까지 다음 조건문을 실행**
- 블록 스코프 생성

### 반복문의 종류와 특징

#### while

```javascript
while (condition){
    //do something
}
```

- 조건문이 참인 동안 반복 시행
- 조건은 소괄호 안에 작성
- 실행할 코드는 중괄호 안에 작성
- 블록 스코프 생성

#### for

- 세미콜론으로 구분되는 세 부분으로 구성

```javascript
for (initialization; condition; expression){
    //do something
}
```

- initialization: 최초 반복문 진입 시 1회만 실행되는 부분
- condition: 매 반복 시행 전 평가되는 부분
- expression: 매 반복 시행 이후 평가되는 부분
- 블록 스코프 생성

#### for ... in

```javascript
for (variable in object) {
    //do something
}
```

- 주로 **객체인 속성들을 순회**할 때 사용

  - key-value로 이루어진 자료구조([객체](#객체) 참고)

    - value는 []과 .으로 접근 가능

      ```javascript
      const words ={
          apple = 'yummy',
          sky = 'blue'
      }
      for (let word in words) {
          console.log(words.sky)		//blue
          console.log(words[word])
          /*
          yummy
          blue
          */
      }
      ```

- <u>배열도 순회 가능하지만 인덱스 순으로 순회한다는 보장이 없으므로</u> **권장하지 않음**

- 실행할 코드는 **중괄호** 안에 작성

- 블록 스코프 생성

#### for ... of

```javascript
for (variable of iterables) {
    //do something
}
```

- **반복 가능한 객체를 순회하며 값을 꺼낼 때 사용**.
  - 반복 가능한 객체의 종류: Array, Map, Set, String 등
  - object의 경우 for...of를 쓰면 TypeError 발생(iterable하지 않으므로)
- 실행할 코드는 **중괄호** 안에 작성
- 블록 스코프 생성

#### for...in과 for...of 비교

```javascript
const fruits = ['딸기', '수박', '참외']

for (let fruit in fruits){
    console.log(fruit)
}
/* 배열의 key인 인덱스가 나옴
0
1
2
*/

for (let fruit of fruits){
    console.log(fruit)
}
/*
딸기
수박
참외
*/
```

### 조건문과 반복문 정리

| 키워드     | 종류   | 연관 키워드           | 스코프      |
| ---------- | ------ | --------------------- | ----------- |
| if         | 조건문 | -                     | 블록 스코프 |
| switch     | 조건문 | case, break, default  | 블록 스코프 |
| while      | 반복문 | break, continue       | 블록 스코프 |
| for        | 반복문 | break, continue       | 블록 스코프 |
| for ... in | 반복문 | 객체 순회             | 블록 스코프 |
| for ... of | 반복문 | 배열 등 iterable 순회 | 블록 스코프 |



## 함수

- 참조 타입 중 하나로써 **function 타입**에 속함
- JavaScript에서 함수를 정의하는 방법은 주로 2가지로 구분
  - [함수 선언식](#함수-선언식)
  - [함수 표현식](#함수-표현식)
- [참고] JavaScript의 함수는 **일급 객체**에 해당
  - 일급 객체: 다음의 조건들을 만족하는 객체를 의미함
    - 변수에 할당 가능
    - 함수의 매개변수로 전달 가능
    - 함수의 반환 값으로 사용 가능

### 함수 선언식

```javascript
function name(args) {
    //do something
}

function add(num1,  num2){
    return num1+num2
}
add(1, 2)
```

- 함수의 이름과 함께 정의하는 방식
- 익명함수로 
- 3가지 부분으로 구성
  - 함수의 이름(name)
  - 매개변수(args)
  - body(중괄호 내부)

### 함수 표현식

```javascript
const name = function (args) {	//이름이 없다
    //do something
}	

const add = function(num1, num2) {
    return num1 + num2
}
add(1, 2)
```

- 함수를 표현식 내에서 정의하는 방식
  - [참고] 표현식: 어떤 하나의 값으로 결정되는 코드의 단위
- 함수의 이름을 생략하고 익명 함수로 정의  가능
  - 익명 함수: 이름이 없는 함수. python의 lambda와 비슷
  - 익명함수는 **함수 표현식에서만** 가능
- 3가지 부분으로 구성
  - 함수의 이름(<u>생략 가능</u>)
  - **매개변수(args)**
  - **body(중괄호 내부)**
-   Airbnb Style Guide 권장 방식

### 기본 인자

- 인자 작성 시 '=' 문자 뒤 기본 인자 선언 가능

  ```javascript
  const greeting = function (name = 'Anonymous'){
      return `Hello ${name}`
  }
  greeting()	//Hello Anonymous
  ```

### 매개변수와 인자의 개수 불일치 허용

```javascript
//매개변수보다 인자의 개수가 많을 경우
const noArgs = function () {
    return 0
}
noArgs(1,2,3)	//0

const twoArgs = function(arg1, arg2) {
    return [arg1, arg2]
}
twoArgs(1,2,3)	//[1,2]

//매개변수보다 인자의 개수가 적을 경우
const threeArgs = function(arg1, arg2, arg3) {
    return [arg1, arg2, arg3]
}
threeArgs()		//[undefined, undefined, undefined]
threeArgs(1)	//[1, undefined, undefined]
```

#### Rest Parameter

```javascript
const restOpt = function(arg1, arg2, ...restArgs) {
    return [arg1, arg2, restArgs]
}
restOpt(1,2,3,4,5)	//[1,2,[3,4,5]]
restOpt(1,2)		//[1,2,[]]
```

- **rest parmeter(...)**를 사용하면 함수가 정해지지 않은 수의 매개변수를 **배열**로 받음(python의 *args와 유사)
  - 만약 rest operator로 처리한 매개변수가 인자로 넘어오지 않을 경우에는, 빈 배열로 처

#### *Spread operator

```javascript
const spreadOpr= function(arg1, arg2, arg3) {
    return arg1 + arg2 + arg3
}

const numbers = [1,2,3]
spreadOpr(...numbers)	//6
```

- **spread operator(...)**를 사용하면 <u>배열 인자를 전개하여 전달 가능</u>

### 함수 선언식과 표현식 비교 정리

- 공통점: 데이터 타입, 함수 구성 요소(이름, 매개변수, body)
- 차이점
  - 함수 선언식: 익명 함수 불가능	/	호이스팅 O
  - 함수 표현식: 익명 함수 가능       /     호이스팅 X

#### 함수의 타입

- 선언식 함수와 표현식 함수 모두 타입은 **function**으로 동일

#### 호이스팅 

##### 함수 선언식

```javascript
add(2, 7)	//9

function add (num1, num2) {
    return num1+num2
}	//코드는 위에서 아래로 실행. var에서는 호이스팅으로 선언부가 모두 위로 올라감. NameError 발생하지 않는다.
```

- 함수  선언식으로 선언한 함수는 var로 정의한 변수처럼 hoisting 발생
- 함수 호출이후에 선언해도 동작

##### 함수 표현식

```javascript
sub(7, 2)	//Uncaught ReferenceError: Cannot access 'sub' before initialization

const sub = function (num1, num2) {
    return num1  -  num2
}
```

- 함수 표현식으로 선언한 함수는 **함수 정의 전에 호출 시 에러 발생**
- 함수 표현식으로 정의된 함수는 변수로 평가되어 **변수의 scope 규칙**을 따름

```javascript
console.log(sub)	//undefined
sub(7, 2)			//Uncaught TypeError : sub is not a function
var sub = function (num1, num2) {
    return num1  -  num2
}
```

- 함수 표현식을 var 키워드로 작성한 경우, 변수가 선언 전 **undefined로 초기화되어 다른 에러가 발생**
- var 대신 **const** 쓰는 것을 권장

### Arrow Function

- 함수를 **비교적 간결하게 정의**할 수 있는 문법
- **function 키워드 생략 가능**
- 함수의 매개변수가 단 하나 뿐이라면, '( )'도 생략 가능
- 함수 몸통이 표현식 하나라면 '{ }'과 return도 생략 가능
- 기존 function 키워드 사용 방식과의 차이점은 [this 키워드](#this)까지 본 후 정리

```javascript
const arrow1  = function (name) {
    return `hello, ${name}`
}
//function 키워드 삭제
const arrow2 = (name) => {return `hello, ${name}`}

//매개변수가 한 개인 경우에만 ( )생략 가능
const arrow3 = name => {return `hello, ${name}`}

//함수의 body가 return을 포함하여 1개일 경우, { }와 return 삭제 가능
const arrow4 = name => `hello, ${name}`

//예시
const add = (a, b) => a+b
```

[참고] IIFE(즉시 실행 함수 표현, Immediately Invoked Function Expression)

```javascript
(function () {
    //do something
    })()
```

- 전역 스코프(Global scope)를 오염시키지 않기 위해 사용



## 문자열

### 문자열 관련 주요 메서드 목록

| 메서드   | 설명                                      | 비고                                         |
| -------- | ----------------------------------------- | -------------------------------------------- |
| includes | 특정 문자열의 존재여부를 참/거짓으로 반환 |                                              |
| split    | 문자열을 토큰 기준으로 나눈 배열 반환     | 인자가 없으면 기존 문자열을 배열에 담아 반환 |
| replace  | 해당 문자열을 대상 문자열로 교체하여 반환 | replaceAll                                   |
| trim     | 문자열의 좌우 공백 제거하여 반환          | trimStart, trimEnd                           |

#### includes

```javascript
const str = 'a santa'
str,includes('santa')	//true
str.includes('asan')	//false
```

- string.includes(value)
  - 문자열에 value가 존재하는지 판별 후 참 또는 거짓 반환

#### split

```javascript
const str = 'a santa'

str.split()		//['a santa']
str.split('')	//['a', ' ', 's','a','n','t','a']
str.split(' ')	//['a', 'santa']
```

- string.split(value)
  - value가 없을 경우, 기존 문자열을 배열에 담아 반환
  - value가 빈 문자열일 경우, 각 문자로 나눈 배열을 반환
  - value가 기타 문자열일 경우, 해당 문자열로 나눈 배열을 반환

#### replace

```javascript
const str = 'a santa'

str.replace(' ', '-')		//'a-santa'
str,replaceAll('a', 'q')	//'q-sqntq'
```

- string.replace(from,to)
  - 문자열에 from 값이 존재할 경우, **1개만** to 값으로 교체하여 반환

- string.replaceAll(from, to)
  - 무자열에 from 값이 존재할 경우, **모두** to 값으로 교체하여 반환

#### trim

```javascript
const str = '  a santa  '

str.trim()		//'a santa'
str,trimStart()	//'a santa  '
str.trimEnd()	//'  a santa'
```

- string.trim()
  - 문자열 시작과 끝의 모든 공백문자(스페이스, 탭, 엔터 등)를 제거한 문자열 반환

- string.trimStart()
  - 문자열 시작의 공백문자(스페이스, 탭, 엔터 등)를 제거한 문자열 반환

- string.trimEnd()
  - 문자열 끝의 공백문자(스페이스, 탭, 엔터 등)를 제거한 문자열 반환



## 배열

### 배열의 정의와 특징

- 키와 속성들을 담고 있는 참조 타입의  **객체(object)**
- 순서를 보장하는 특징이 있음
- 주로 대괄호를 이용하여 생성하고, 0을 포함한 양의 정수 인덱스로 특정 값에 접근 가능
  - 파이썬과 달리 -1을 사용하여 마지막 요소에 접근할 수 없다
- 배열의 길이는 array.length 형태로 접근 가능

### 배열 관련 주요 메서드 목록 - 기본

| 메서드          | 설명                                                 | 비고                     |
| --------------- | ---------------------------------------------------- | ------------------------ |
| reverse         | **원본 배열**의 요소들의 순서를 반대로 정렬          |                          |
| push & pop      | 배열의 **가장 뒤**에 요소를 **추가 또는 제거**       |                          |
| unshift & shift | 배열의 **가장 앞**에 요소를 **추가 또는 제거**       |                          |
| includes        | 배열에 특정 값이 존재하는지 판별 후 **참/거짓 반환** |                          |
| indexOf         | 배열에 특정 값이 존재하는지 판별 후 **인덱스 반환**  | 요소가 없을 경우 -1 반환 |
| join            | 배열의 **모든 요소를 구분자를 이용하여 연결**        | 구분자 생략 시 쉼표 기준 |

#### reverse

```javascript
const numbers = [1, 2, 3, 4, 5]
numbers.reverse()
console.log(numbers)	//[5, 4, 3, 2, 1]
```

- array.reverse() 
  - 원본 배열의 요소들의 순서를 반대로 정렬

#### push & pop

```javascript
const numbers = [1, 2, 3, 4, 5]

numbers.push(6)
console.log(numbers)	//[1, 2, 3, 4, 5, 6]

numbers.pop()
console.log(numbers)	//[1, 2, 3, 4, 5]
```

- array.push()
  - 배열의 가장 뒤에 요소 추가

- array.pop ()
  - 배열의 마지막 요소 제거

#### unshift & shift

```javascript
const numbers = [1, 2, 3, 4, 5]

numbers.unshift(0)
console.log(numbers)	//[0, 1, 2, 3, 4, 5]

numbers.shift()
console.log(numbers)	//[1, 2, 3, 4, 5]
```

- array.unshift() 
  - 배열의 가장 앞에 요소 추가

- array.shift() 
  - 배열의 첫번째 요소 제거

#### includes

```javascript
const numbers = [1, 2, 3, 4, 5]
console.log(numbers.includes(1))	//true
console.log(numbers.includes(7))	//false
```

- array.includes(value) 
  - 배열에 특정 값이 존재하는지 판별 후 참 또는 거짓 반환

#### indexOf

``````javascript
const numbers = [1, 2, 3, 4, 5]

console.log(numbers.indexOf(3))	//2
console.log(numbers.indexOf(7))	//-1
``````

- array.indexOf(value) 
  - 배열의 특정 값이 존재하는지 확인 후 가장 첫번째로 찾은 요소의 인덱스 반환
  - 만약 해당 값이 없을 경우 **-1** 반환

#### join

```javascript
const numbers = [1, 2, 3, 4, 5]

    console.log(numbers.join())	//1,2,3,4,5
console.log(numbers.join(''))	//12345
console.log(numbers.join(' '))	//1 2 3 4 5
console.log(numbers.join('-'))	//1-2-3-4-5
```

- array.join([separator])
  - 배열의 모든 요소를 문자열로 연결하여 반환. 구분자는 선택적으로 지정 가능하며 생략 시 **쉼표를 기본값**으로 사용

### spread operator

```javascript
const array = [1, 2, 3, 4, 5]
const newArray = [0, ...array, 6]

console.log(newArray)	//[0, 1, 2, 3, 4, 5, 6]
```

- **spread operator(...)**를 사용하면 배열 내부에서 배열 전개 가능
- S5까지는 Array.concat() 메서드를 사용
- 얕은 복사에 활용 가능

### *배열 관련 주요 메서드 목록 - 심화

- 메서드 호출 시 인자로 **callback함수**를 받는 것이 특징
  - **callback함수**: 어떤 함수의 내부에서 실행될 목적으로 인자로 넘겨받는 함수
  - ex) django views,py에 정의한 <함수이름>이 urls.py의 path함수에 전달되는 callback 함수

| 메서드  | 설명                                                         | 비고             |
| ------- | ------------------------------------------------------------ | ---------------- |
| forEach | 배열의 각 요소에 대해 콜백 함수를 한 번씩 실행               | **반환 값 없음** |
| map     | 콜백함수의 **반환 값을 요소**로 하는 **새로운 배열 반환**    |                  |
| filter  | 콜백 함수의 반환 값이 **참인 요소들만** 모아서 **새로운 배열을 반환** |                  |
| reduce  | 콜백 함수의 반환 값들을 **하나의 값(acc)에 누적 후 반환**    |                  |
| find    | 콜백 함수의 **반환 값이 참이면 해당 요소를 반환**            |                  |
| some    | 배열의 **요소 중 하나라도 판별 함수를 통과**하면 참을 반환   |                  |
| every   | 배열의 **모든 요소가 판별 함수를 통과**하면 참을 반환        |                  |

