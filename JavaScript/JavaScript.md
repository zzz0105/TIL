# JavaScript

## Intro

> 브라우저(BOM)과 그 내부의 문서(DOM)를 조작하기 위해 ECMAScript(JS)를 학습

### 브라우저(browser)

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
    - ex) JavaScript로 document의 title을 바꿀 수 있다 
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

#### var

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

[참고] undefined 타입과 null 타입 비교

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

**for...in과 for...of 비교**

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
  - 배열은 인덱스를 키로 가지며 length 프로퍼티를 갖는 특수항 객체
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

#### forEach

```javascript
array.forEach((element, index, array) =>{
    //do something
})

const fruits = ['딸기', '수박', '참외', '메론']
fruits.forEach((fruit, index) => {
    console.log(fruit, index)
})
/*
딸기 0
수박 1
참외 2
메론 3
*/
```

- array.forEach(callback(element[, index[,array]]))
  - 배열의 각 요소에 대해 콜백 함수를 한 번씩 실행
  - 콜백 함수는 3가지 매개변수로 구성
    - element: 배열의 요소
    - index: 배열 요소의 인덱스
    - array: 배열 자체
  - **반환 값이 없는 메서드**

#### map

```javascript
array.map((element, index, array) =>{
    //do something
})

const numbers = [1, 2, 3, 4, 5]
const doubleNums = numbers.map((num) => {
    return num * 2
})
console.log(numbers.map(number => number * 2))	// [2, 4, 6, 8, 10]

const rectangles = [
    {'width': 30, 'height': 20}, 
    {'width': 10, 'height': 20}
]	//결과 [600, 200]
const area = rectangles.map((wh) => wh.width*wh.height)
console.log(area)
```

- array.map(callback(element[, index[, array]]))
  - 배열의 각 요소에 대해 콜백 함수를 한 번씩 실행
  - 콜백 **함수의 반환 값을 요소로 하는** 새로운 배열 반환
  - 기존 배열 전체를 다른 형태로 바꿀 때 유용

#### filter

```javascript
array.filter(element, index, array) => {
    //do something
}

const numbers = [1,2,3,4,5]
const oddNums = numbers.filter((num, index) =>{
    return num % 2
})
console.log(oddNums)	//1, 3, 5

console.log(students.map((x) => x.python + x.js))

students.map(function (element) {return element.python + element.js})
```

- array.filter(callback(element[, index[, array]]))
  - 배열의 각 요소에 대해 **콜백 함수를 한 번씩 실행**
  - 콜백 **함수의 반환 값이 참인 요소들만** 모아서 새로운 배열을 반환
  - 기존 배열의 요소들을 필터링할 때 유용

#### reduce

```javascript
array.reduce((acc, element, index, array) => {
    //do something
}, initialValue)

const numbers = [1, 2, 3]
const result = numbers.reduce((acc, num) => {
    return acc + num
}, 0)
console.log(result)	//6
```

- array.reduce(callback(acc, element, [index[, array]])[, initialValue])
  - 배열의 각 요소에 대해 콜백 함수를 한번씩 실행
  - 콜백 함수의 반환 값들을 **하나의 값에 누적 후 반환**
  - reduce 메서드의 주요 매개변수
    - acc
      - 이전 callback 함수의 반환 값이 누적되는 변수
    - initialValue(optional)
      - 최초 callback 함수 호출 시 acc에 할당되는 값, default 같은 배열의 첫 번째 값
  - [참고] 빈 배열의 경우 initialValue를 제공하지 않으면 에러 발생

#### find

```javascript
array.find((element, index, array)) {
    //do something
}

const users = [
    {name:'길동', age: 30},
    {name '철수',age: 18}
]
const result = users.find((user)) => {
   return avenger.name==='철수'
}
console.log(result)	//{name '철수',age: 18}
```

- array.find(callback(element[, index[, array]]))
  - 배열의 각 요소에 대해 콜백 함수를 한 번씩 실행
  - 콜백 함수의 반환 값이 참이면, 조건을 만족하는 첫번째 요소를 반환
  - 찾는 값이 배열에 없으면 undefined

#### some

```javascript
array.some((element, index, array)) => {
    //do something
})
const numbers = [1, 2, 3]
const hasEvenNumber = numbers.some((num) => {
    return num%2===0
}, 0)
console.log(hasEvenNumber)	//true
```

- array.some(callback(element[, index[, array]]))
  - 배열의 **요소 중 하나라도** 주어진 판별 함수를 통과하면 참.
  - 모든 요소가 통과하지 못하면 거짓 반환
  - [참고] 빈 배열은 항상 **거짓** 반환

#### every

```javascript
array.every((element, index, array)) => {
    //do something
})
const numbers = [1, 2, 3]
const isEveryNumberEven = numbers.some((num) => {
    return num%2===0
}, 0)
console.log(isEveryNumberEven)	//false
```

- array.every(callback(element[, index[, array]]))
  - 배열의 **모든 요소가** 주어진 판별 함수를 통과하면 참.
  - 하나의 요소라도 통과하지 못하면 거짓 반환
  - [참고] 빈 배열은 항상 **참** 반환

### [참고] 배열 순회 방법 비교

| 방식     | 특징                                                         | 비고                         |
| -------- | ------------------------------------------------------------ | ---------------------------- |
| for loop | 모든 브라우저 환경에서 지원<br />인덱스를 활용하여 배열의 요소에 접근<br />break, continue 사용 가능 |                              |
| for...of | 일부 오래된 브라우저 환경에서 지원x<br />인덱스 없이 배열의 요소에 바로 접근 가능<br />break, continue 사용 가능 |                              |
| forEach  | 대부분의 부라우저 환경에서 지원<br />break, continue 사용 불가능 | Airbnb style Guide 권장 방식 |



## 객체

### 객체의 정의와 특징

- 객체는 속성의 집합이며 중괄호 내부에 key와 vlue의 쌍으로 표현
- **key**는 **문자열 타입**만 가능
  - key이름에 띄어쓰기 등의  구분자가 있으면 따옴표로 묶어서 표현
- **value**는 **모든 타입(함수 포함)** 가능
- 객체 요소 접근은 점 또는 대괄호로 가능
  - key이름에 띄어쓰기 같은 구분자가 있으면 따옴표로 묶어서 표현

### 객체와 메서드

```javascript
const me = {
    firstName: '길동',
    lastName:  '홍',
    
    fullName: this.firstName + this.lastName
    
    getFullName: function(){
        return this.firstName + this.lastName
    }
}
```

- 메서드는 객체의 속성이 참조하는 함수
- 객체.메소드명()으로  호출 가능
- **메서드** 내부에서는 <u>this 키워드가 **객체**를 의미</u>함
  - fullName은 메서드가 아니까 때문에 정상출력 되지 않음(NaN)
  - getFullName은 메서드이기 때문에 해당 객체의 firstName과 lastName을 정상적으로 이어서 반환

### 객체 관련 ES6 문법 익히기

#### 속성명 축약

```javascript
const fruits = ['딸기', '수박', '참외', '메론']
const drinks = ['콜라', '사이다']

const shop = {
    fruits,
    drinks,
}
console.log(shop)
/*
fruits: ['딸기', '수박', '참외', '메론'],
drinks: ['콜라', '사이다']
*/
```

- 객체를 정의할 때 key와 할당하는 변수의 이름이 같으면 예시와 같이 축약 가능

#### 메서드명 축약

```javascript
const obj = {
    greeting() {
        console.log('안녕')
    }
}
obj,greeting()	//안녕
```

- 메서드 선언 시 function 키워드 생략 가능

#### 계산된 속성명 사용하기

```javascript
const key = 'fruits'
const value = ['딸기', '수박', '참외', '메론']

const likes = {
    [key]: value
}
console.log(likes)			//{fruits: Array(4)}
console.log(likes.fruits)	//["딸기", "수박", "참외", "메론"]
```

- 객체를 정의할 때 key의 이름을 표현식을 이용하여 동적으로 생성 가능

#### 구조 분해 할당

```javascript
const userInfo = {
    name: '길동',
    birthday: '04-26',
    phoneNumber: '012-3456-7890'
}

const name = userInfo.name
const birthday = userInfo.birthday
const phoneNumber = userInfo.phoneNumber

const {name} = userInfo
const {birthday} = userInfo
const {phoneNumber} = userInfo

const {name, birthday, phoneNumber} = userInfo
```

- 배열 또는 객체를 분해하여 속성을 변수에 쉽게 할당할 수 있는 문법

#### 객체 전개 구분(Spread Operator)

```javascript
const obj  = {b:1, c:2}
const newObj = {a:0, ...obj,  d:3}

console.log(newObj)	//{a:0, b:1, c:2,  d:3}
```

- spread operator(...)를 사용하면 객체 내부에서 객체 전개 가능
- ES5까지는 Object.assign() 메서드를 사용

### JSON

> JavaScript Object Noation

- key-value 쌍의 형태로 데이터를 표기하는 언어 독립적 표준 포맷
- 자바스크립트의 객체와 유사하게 생겼으나 실제로는 문자열 타입
  
- 따라서 JS의 객체로써 조작하기 위해서는 구문 분석(parsing)이 필수
  
- 자바스크립트에서는 JSON을 조작하기 위한 두 가지 내장 메서드를 제공

  ```javascript
  const jsonData =  JSON.stringify({
      drink: 'soda',
      fruit: 'apple',
  })
  
  console.log(jsonData)			//"{"drink": "soda", "fruit": "apple"}"
  console.log(typeof jsonData)	//string
  
  const parsedData = JsoN.parse(jsonData)
  console.log(parsedData)			//{drink: "soda", fruit: "apple"}
  console.log(typeof parsedData)	//object
  ```

  - JSON.parse
    - JSON => 자바스크립트 객체
  - JSON.stringify()
    - 자바스크립트 객체 => JSON 



## this

```javascript
function getFullName(){
    return this.lastName + this.firstName
}
const me = {
    firstName = '길동',
    lastName = '홍',
    getFullName: getFullname,    
}
const you = {
    firstName = '짱구',
    lastName = '신',
    getFullName: getFullname,
}
me.getFullName()	//홍길동	this===me
you.getFullName()	//신짱구	this===you
getFullName()		//NaN		this===window
```

- 실행 문맥에 따라 다른 대상을 가리킨다
  - class 내부의 생성자 함수
    - this는 생성되는 객체를 가리킴(Python의 self와 같음)
  - 메서드(객체.메서드명()으로 호출 가능한 함수)
    - this는 해당 메서드가 소속된 객체를 가리킴
  - 위의 두가지 경우를 제외하면 모두 최상위 객체(window)를 가리킴

### function 키워드와 화살표 함수 차이

```javascript
//function 키워드
const obj = {
    PI: 3.14,
    radiuses: [1, 3, 5],
    printArea: function () {
        this.radiuses.forEach(function(r){
            console.log(this.PI * r * r)
        }.bind(this))
    },
}

//화살표 함수
const obj ={
    PI:3.14,
    radiuses = [1, 3, 5],
    printArea: function() {
        this.radiuses.forEach((r)->{
            console.log(this.PI * r * r)
        })
    },
}
```

- this.radiuses는 메서드(객체.메서드명()으로 호출 가능) 소속이기 때문에 정상적으로 접근 가능

- forEach의 콜백함수의 경우 메서드가 아님(객체.메서드명()으로 호출 불가능)

  -> 때문에 콜백함수의 내부의 this는 window가 되어 this.PI는 정상적으로 접근 불가능

  -> 이 콜백함수 내부에서 this.pi에 접근하기 위해서 <u>함수객체.bind(this) 메서드를 사용</u>

  => 이 <u>번거로운 과정을 없앤 것</u>이 **화살표 함수**


- 함수  내부에 this 키워드가 존재할 경우

  - 화살표 함수와 function 키워드로 선언한 함수가 다르게 동작

- 함수 내부에 this  키워드가 존재하지 않을 경우

  - 완전 동일하게 동작

  

## lodash

> A modern JavaScript utility library

- 모듈성, 성능 및 추가 기능을 제공하는 JavaScript 유틸리티 라이브러리
- array, object 등 자료구조를 다룰 때 사용하는 유용하고 간편한 유틸리티 함수들을 제공
  - ex) reverse, soryBy, range, random, cloneDeep ...

```javascript
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
//위의 CDN import를 통해 _ 식별자 사용 가능
<script>
    _.sample([1,2,3,4])
	_.sampleS]ize(_.range(1, 46), 6)
	_.reverse([1,2,3,4])
	_.range(1,5,2)
	
	//깊은 복사 - lodash를 사용하지 않을 경우, 직접 함수를 만들어서 구현해야 함
	const original = {a : {b : 1}}
    const ref = original
    const copy = _.cloneDeep(original)
    console.log(original.a.b, ref.a.b, copy.a.b)	//1,1,1
	ref.a.b = 10
	console.log(original.a.b, ref.a.b, copy.a.b)	//10,10,1
	copy.a.b = 20
	console.log(original.a.b, ref.a.b, copy.a.b)	//10,10,20
</script>
```



## History of JavaScript

- 핵심 인물
  - 팀 버너스리
    - WWW, URL, HTTP, HTML 최초 설계자
    - 웹의 아버지
  - 브랜던 아이크
    - JavaScript 최초 설계자
    - 모질라 재단 공동 설립자
    - 코드네임 피닉스 프로젝트 진행
      - 파이어폭스의 전신
- JavaScript의 탄생
  - 1994년 당시 넷스케이프 커뮤니케이션스사의 Netscape Navigator(NN) 브라우저가 전 세계 점유율을 80% 이상 독점하며 브라우저의 표준 역할을 함
  - 당시 넷스케이프에 재직중이던 브랜던 아이크가 HTML을 동적으로 종작하기 위한 회사 내부 프로젝트를 진행  중 JS를 개발
    - JavaScript 이름 변천사
      - Mocha - LiveScript - JavaScript(1995)
  - 그러나 1995년 경쟁사 마이크로소프트에서 이를 채택하여 커스터마이징한 JScript를 만들고 이를 IE 1.0에 탑재 -> 1차 브라우저 전쟁의 시작

- History of JavaScript & Browser

  - 브라우저 전쟁
    - 1차 브라우저 전쟁
      - MS의 폭팔적 성장, IE3에서 자체적인 JScript를 지원, 호환성 문제로 크로스 브라우징 등의 이슈 발생
      - 이후 넷스케이프 후계자들은 모질라 재단 기반의 파이어폭스를 개발
    - 2차 브라우저 전쟁 : MS vs Google
      - 2008년 Google의 Chrome 브라우저 발표
      - 2011년 3년 만에 파이어폭스의 점유율을 돌파 후 2012년부터 전세계 점유율 1위 등록
      - 크롬의 승리 요인: 압도적인 속도, 강력한 개발자 도구 제공, 웹 표준
  - 파편화와 표준화의 투쟁
    - 제 1차 브라우저 전쟁 이후 수많은 브라우저에서 자체 자바스크립트 언어를 사용하게 됨
    - 결국 서로 다른 자바스크립트가 만들어지면서 크로스 브라우징 이슈가 발생하여 웹 표준의 필요성이 제기

- 브라우저 전쟁의 여파

  - Cross Browsing Issue
    - W3C에서 채택된 표준 웹 기술을 채용하여 각각의 브라우저마다 다르게 구현되는 기술을 비슷하게 만들되, 어느 한쪽에 치우치지 않도록 웹 페이지를 제작하는 방법론(동일성이 아닌 **동등성**)
    - 브라우저마다 렌더링에 사용하는 엔진이 다르기 때문
- 표준화(통합)을 위한 노력
    - 1996년부터 넷스케이프는 표준 제정의 필요성을 주장
      - ECMA 인터네셔널(정보와 통신 시스템을 위한 국제적 표준화 기구)에 표준 제정 요청
    - 1997년 ECMAScript1(ES1) 탄생
    - 제1차 브라우저 전쟁 이후 제기된 언어의 파편화를 해결하기 위해 각 브라우저 회사와 재단은 표준화에 더욱 적극적으로 힘을 모으기 시작
    - 2015년 ES2015(ES6) 탄생
      - "Next-gen of JS"
      - JavaScript의 고질적인 문제들을 해결
      - JavaScript의 다음 시대라고 불릴 정도로 많은 혁신과 변화를 맞이한 버전
      - 이때부터 버전 순서가 아닌 출시 연도를 붙이는 것이 공식 명칭이나 통상적으로 ES6라 부름
      - 현재는 표준 대부분이 ES6+로 넘어옴
  - Vanilla JavaScript
    - 크로스 브라우징, 간편한 활용 등을 위해 많은 라이브러리 등장(jQuery 등)
    - ES6 이후, 다양한 도구의 등장으로 순수 자바스크립트 활용의 증대
  
  

## DOM 조작

- [브라우저에서 할 수 있는 일, DOM과 BOM](#브라우저에서-할-수-있는-일)

- 개념
  - Document는 문서 한 장(HTML)에 해당하고 이를 조작
  - **DOM 조작 순서**
    1. 선택(Select)
    2. 변경(Manipulation)
- **DOM 관련 객체의 상속 구조**
  - EventTarget
    - Event Listener를 가질 수있는 객체가 구현하는 DOM 인터페이스
  - Node
    - 여러가지 DOM 타입들이 상속하는 인터페이스
  - Element
    - Document 안의 모든 객체가 상속하는 가장 범용적인 인터페이스
    - 부모인 Node와 그 부모인 EventTarget의 속성을 상속
  - Document
    - 브라우저가 불러온 웹 페이지를 나타냄
    - DOM 트리의 진입점(Entry point) 역할을 수행
  - HTMLElement
    - 모든 종류의 HTML 요소
    - 부모 element의 속성 상속

### DOM 선택

- DOM  선택 관련 메서드
  - document.**querySelector(selector)**
    - 제공한 선택자와 일치하는 element 하나 선택
    - 제공한 CSS selector를 만족한느 첫번째 element 객체를 반환(없다면 null)
  - document.**querySelectorAll(selector)**
    - 제공한 선택자와 일치하는 여러 element를 선택
    - 매칭할 하나 이상의 셀렉터를 포함하는 유효한 CSS selector를 인자(문자열)로 받음
    - 지정된 셀렉터에 일치하는 NodeList를 반환
  - getElementById(id)
  - getElementByTagName(name)
  - getElementByClassName(names)
  - querySelector(), querySelectorAll()을 사용하는 이유
    - id, class 그리고 tag 선택자 등을 모두 사용 가능하므로, 더 구체적이고 유연하게 선택 가능
    - 예시
      - document.querySelector('#id')
      - document.querySelectorAll('.class')
- 선택 메서드별  반환 타입
  - 단일 element
    - getElementById()
    - querySelector()
  - HTMLCollection
    - getElementByTagName()
    - getElementByClassName()
  - NodeList
    - querySelectAll()
- HTMLColloction과 NodeList
  - 둘 다 배열과 같이 각 항목에 접근하기 위한 index를 제공(유사 배열)
  - HTMLCollction: name, id, index 속성으로 각 항목에 접근 가능
  - NodeList
    - index로만 각 항목에 접근 가능
    - 단, HTMLCollction과 달리 배열에서 사용하는 forEach 메서드 및 다양한 메서드 사용 가능
  - 둘 다 Live Collection으로 DOM의 변경사항을 실시간으로 반영하지만, querySelectAll()에 의해 반환되는 NodeList는 Static Collection으로 실시간으로 반영되지 않음
- **Collection**
  - Live Collection
    - 문서가 바뀔 때 실시간으로 업데이트 됨
    - DOM의 변경사항을 실시간으로 collection에 반영
    - ex) HTMLCollection, NodeList
  - Static Collection(non-live)
    - DOM이 변경되어도 collection 내용에는 영향을 주지 않음
    - querySelectorAll()의 반환 NodeList만 static collection

### DOM 변경

- DOM 변경 관련 메서드

  - document.createElement()

    - 작성한 태그 명의 HTML 요소를 생성하여 반환

  - Element.append()

    - 특정 부모 Node의 자식 NodeList 중 마지막 자식 다음에 Node 객체나 DOMString을 삽입
    - 여러 개의 Node 객체, DOMString을 추가할 수 있음
    - 반환 값이 없음

  - Node.appendChild()

    - 한 Node를 특정 부모 Node의 자식 NodeList 중 마지막 자식으로 삽입(Node만 추가 가능)
    - 한번에 오직 하나의 Node만 추가할 수 있음
    - 만약 주어진 Node가 이미 문서에 존재하는 다을ㄴ Node를 참조한다면 새로운 위치로 이동

  - ParentNode.append() vs Node.appendChild()

    | ParentNode.append()               | Node.appendChild()           |
    | --------------------------------- | ---------------------------- |
    | DOM String 객체 추가 가능         | Node 객체만 허용             |
    | 반환 값 없음                      | 추가된 Node 객체 반환        |
    | 여러 Node 객체와 문자열 추가 가능 | 하나의 Node 객체만 추가 가능 |

- 변경 관련 속성(property)

  - Node.innerText
    - Node 객체와 그 자손의 텍스트 컨텐츠(DOMString)를 표현(해당 요소 내부의 raw text)(사람이 읽을 수 있는 요소만 남김)
    - 즉, 줄 바꿈을 인식하고 숨겨진 내용을 무시하는 등 최종적으로 스타일링이 적용된 모습으로 표현
  - Element.innerHTML
    - 요소(element) 내에 포함된 HTML 마크업을 반환
    - [참고] XSS 공격에 취약하므로 사용 시 주의
      - XSS(Cros-site Scripting)
        - 공격자가 입력요소를 사용하여(\<input>) 웹 사이트 클라이언트 측 코드에 악성 스크립트를 삽입해 공격하는 방법
        - 피해자(사용자)의 브라우저가 악성 스크립트를 실행하며 공격자가 엑세스 제어를 우회하고 사용자를 가장할 수 있도록 함

### DOM 삭제

- 삭제 관련 메서드
  - ChildNode.remove()
    - Node가 속한 트리에서 해당 Node를 제거
  - Node.removeChild()
    - DOM에서 자식 Node를 제거하고 제거된 Node를 반환
    - Node는 인자로 들어가는 자식 Node의 부모 Node

### DOM 속성

-  속성 관련 메서드

  - Element.setAttribute(name, value)

    - 지정된 요소의 값을 설정
    - 속성이 이미 존재하면 값을 갱신,  존재하지 않으면 지정된 이름과 값으로 새 속성을 추가

  - Element.getAttribute(attributeName)

    - 해당 요소의 지정된 값(문자열)을 반환
    - 인자(attributeName)는 값을 얻고자 하는 속성의 이름

    

## Event Listener

### Event

- 개념

  - <u>네트워크 활동이나 사용자와의 상호작용</u> 같은 **사건의 발생**을 알리기 위한 객체
  - 이벤트 발생
    - 마우스를 클릭하거나 키보드를 누르는 등 사용자 행동으로 발생할 수 있음
    - 특정 메서드를 호출(Element.click())하여 프로그래밍적으로도 만들어낼 수 있음

- Event 기반 인터페이스

  - AnimationEvent, ClipboardEvent, DragEvent 등
  - UIEvent
    - 간단한 사용자 인터페이스 이벤트
    - Event의 상속을 받음
    - MouseEvent, KeyboardEvent, InputEvent, FocusEvent 등의 부모 객체 역할을 함

- Event의 역할

  - ~하면 ~한다	ex) 클릭하면 경고창을 띄운다

    => 특정 이벤트가 발생하면 할 일을 **등록**한다

- Event handler

  - EventTarget**.addEventListener()**

    - 지정한 이벤트가 대상에 전달될 **때마다** 호출할 **함수를 설정**	(함수===일(동작)의 명세)
    - 이벤트를 지원하는 모든 객체(Element, Document, Window 등)를 대상으로 지정 가능
    - DOM 관력 객체의 상속 구조에서, EventTarget이 가장 최상단에 위치 => 모든 요소에 이벤트를 달아줄 수 있다

  - target**.addEventListener(type, listener**[, options]**)**

    > 대상(EventTarget)에 특정 이벤트(type)가 발생하면, 할 일을 등록하자(listener)

    - type: 반응할 이벤트 유형(대소문자 구분 문자열)
    - listener: 지정된 타입의 이벤트가 발생했을 때 알림을 받는 객체
      EventListener 인터페이스 혹은 JS function 객체(<u>콜백 함수</u>)여야 함

- Event 취소: enent.preventDefault()

  - 현재 이벤트의 기본 동작을 중단
  - HTML 요소의 기본 동작을 작동하지 않게 막음
    - ex) a 태그의 기본 동작은 클릭 시 링크로 이동 / form 태그의 기본 동작은 form 데이터  전송
  - 이벤트를 취소할 수 잇는 경우, 이벤트의 전파를 막지 않고 그 이벤트를 취소
  - 취소할 수 없는 이벤트도 존재
    - 이벤트의 취소 가능 여부는 event.cancelable을 사용해 확인할 수 있음
