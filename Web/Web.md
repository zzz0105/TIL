# Web

## HTML

> Hyper Text Markup Language. 웹페이지를 작성(구조화)하기 위한 언어

* HyperText: 참조를 통해 사용자가 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트

* Markup Language: 태그 등을 이용하여 문서나 구조를 명시하는 언어

  * ex. HTML, markdown




### HTML의 기본 구조

#### html: 문서의 최상위(root) 요소
#### head: 문서 메타데이터(데이터를 설명해주는 데이터) 요소
  * 문서 제목, 인코딩, 스타일, 외부 파일 로딩 등

  * 일반적으로 브라우저에 나타나지 않는 내용

  * head 예시	

    | head      | 설명                                       |
    | --------- | ------------------------------------------ |
    | \<title>  | 브라우저 상단 타이틀                       |
    | \<meta>   | 문서 레벨 메타데이터 요소                  |
    | \<link>   | 외부 리소스 연결 요소(CSS파일, favicon 등) |
    | \<script> | 스크립트 요소(JavaScript 파일/코드)        |
    | \<style>  | CSS 직접 지정                              |

    * Open Graph Protocol
      * 메타 데이터를 표현하는 새로운 규악
        * HTML 문서의 메타 데이터를 통해 문서의 정보를 전달
        * 메타 정보에 해당하는 제목, 설명 등을 쓸 수 있도록 정의
#### body: 문서 본문 요소
  * 실제 화면 구성과 관련된 내용



#### DOM(Document Object Model) 트리
  * 텍스트 파일인 HTML 문서를 브라우저에서 렌더링하기 위한 구조
    * HTML 문서에 대한 모델을 구성함
    * HTML 문서 내의 각 요소에 접근/수정에 필요한 프로퍼티와 메서드를 제공함
  * 마크업 스타일 가이드 지키기. 2space
  * 조작) Element에서 HTML 태그 구조를 탐색하며 추가, 삭제, 이동, 편집 등이 가능



#### 요소(element)

```html
<h1>contents</h1>	//태그 h1 내용 contents
```

  * HTML 요소는 시작 태그와 종료 태그 그리고 태그 사이에 위치한 내용으로 구성
    * 태그(Element, 요소)는 컨텐츠(내용)를 감싸는 것으로 그 정보의 성격과 의미를 정의
  * 내용이 없는 태그들 => 닫는 태그가 없다
    * br, hr, img, input, link, meta
  * 요소는 중첩(nested)될 수 있음
    * 요소의 중첩을 통해 하나의 문서를 구조화 => DOM
    * 여는 태그와 닫는 태그의 쌍을 잘 확인해야함
      * 오류를 반환하는 것이 아닌 그냥 레이아웃이 깨진 상태로 출력되기 때문에, 디버기이 힘들어 질 수 있음



#### 속성(attribute)

```html
<a href="https://google.com"></a>	//속성명 href 속성값 https://google.com
```

  * 태그별로 사용할 수 있는 속성은 다르다.
  * 속성 지정 스타일 가이드: 공백 No, 쌍따옴표 사용
  * 속성을 통해 태그의 부가적인 정보를 설정할 수 있음
  * 요소는 속성을 가질 수 있으며, 경로나 크기와 같은 추가적인 정보를 제공
  * 요소의 시작 태그에 작성하며 보통 이름과 값이 하나의 쌍으로 존재
  * 태그와 상관없이 사용 가능한 속성(HTML Global Attribute)들도 있음



##### HTML Global Attribute 

* 모든 HTML 요소가 <u>공통으로 사용할 수 있는 대표적인 속성</u>(몇몇 요소에는 아무 효과가 없을 수 있음)
* **id**: 문서 전체에서 유일한 고유 식별자 지정
* **class**: 공백으로 구분된 해당 요소의 클래스의 목록(CSS, JS에서 요소를 선택하거나 접근)
* data-*: 페이지에 개인 사용자 정의 데이터를 저장하기 위해 사용
* style: inline 스타일. Element의 디자인을 입혀주는 역할(ex. color, font-size)
* **title**: 요소에 대한 추가 정보 지정
* tabindex: 요소의 탭 순서



#### 시맨틱 태그

* HTML5에서 의미론적 요소를 담은 태그의 등장

  * 기존 영역을 의미하는 div 태그를 대체하여 사용

* 대표적인 태그 목록	

  | 태그    | 설명                                                     |
  | ------- | -------------------------------------------------------- |
  | header  | 문서 전체나 섹션의 헤더(머리말 부분)                     |
  | nav     | 내비게이션                                               |
  | aside   | 사이드에 위치한 공간, 메인 콘텐츠와 관련성이 적은 콘텐츠 |
  | section | 문서의 일반적인 구분, 컨텐츠의 그룹을 표현               |
  | article | 문서, 페이지, 사이트 안에서 독립적으로 구분되는 영역     |
  | footer  | 문서 전체나 섹션의 푸터(마지막 부분)                     |

* Non semantic 요소는 div, span 등이 있으며 h1, table 태그들도 시맨틱 태그로 볼 수 있음

* 개발자 및 사용자 뿐만 아니라 검색엔진 등에 의미 있는 정보의 그룹을 태그로 표현

* 단순히 구역을 나누는 것 뿐만 아니라 '의미'를 가지는 태그들을 활용하기 위한 노력

* 요소의 의미가 명확해지기 때문에 코드의 가독성을 높이고 유지보수를 쉽게 함

* 검색엔진최적화(SEO)를 위해서 메타태그, 시맨틱 태그 등을 통한 마크업을 효과적으로 활용 해야함



#### HTML with 개발자 도구

* elements: 해당 요소의 HTML 태그
* Ctrl + Shift + C로 원하는 요소를 선택할 수 있다
  * 복잡한 형태의 경우 Elements에서 HTML 구조를 추가 탐색



### HTML 문서 구조화

#### 텍스트 요소

| 태그                | 설명                                                         |
| ------------------- | ------------------------------------------------------------ |
| \<a>\</a>           | href 속성을 활용하여 다른 URL로 연결하는 하이퍼링크 생성     |
| \<b>\</b>           | 굵은 글씨 요소.                                              |
| \<strong>\</strong> | 중요한 강조하고자 하는 요소 (보통 굵은 글씨로 표현). 시맨틱 코드 |
| \<i>\</i>           | 기울임 글씨 요소                                             |
| \<em>\</em>         | 중요한 강조하고자 하는 요소 (보통 기울임 글씨로 표현). 시맨틱 코드 |
| \<br>               | 텍스트 내 줄 바꿈 생성                                       |
| \<img>              | src 속성을 활용하여 이미지 표현                              |
| \<span>\</span>     | 의미 없는 인라인 컨테이너                                    |



#### 그룹 컨텐츠

| 태그                        | 설명                                                         |
| --------------------------- | ------------------------------------------------------------ |
| \<p>\</p>                   | 하나의 문단(paragraph)                                       |
| \<hr>                       | 문단 레벨 요소에서의 주제의 분리를 의미하며 수평선으로 표현됨(A Horizontal Rule) |
| \<ol>\</ol>                 | 순서가 있는 리스트(ordered list)                             |
| \<ul>\</ul>                 | 순서가 없는 리스트(unordered list)                           |
| \<pre>\</pre>               | HTML에 작성한 내용을 그대로 표현. 보통 고정폭 글꼴이 사용되고 공백문자를 유지 |
| \<blockquote>\</blockquote> | 텍스트가 긴 인용문. 주로 들여쓰기를 한 것으로 표현됨         |
| \<div>\</div>               | 의미 없는 블록 레벨 컨테이너                                 |

#### table

* table의 각 영역을 명시하기 위해 \<thead>\<tbody>\<tfoot>요소를 활용
* \<tr>으로 가로 줄을 구성, 내부에는 \<th> 혹은 \<td>로 셀을 구성
* colspan, rowspan 속성을 활용하여 셀 병합
* \<caption>을 통해 표 설명 또는 제목을 나타냄
* table 태그 기본 구성

| 요소    | 구성  | 예시                       |
| ------- | ----- | -------------------------- |
| thead   | tr>th | \<tr>\<th>ID\</th>         |
| tbody   | tr>td | \<tr>\<td>1\</td>          |
| tfoot   | tr>td | \<tr>\<td>총계\</td>       |
| caption |       | \<caption>1학년\</caption> |



#### form

* 정보(데이터)를 서버에 제출하기 위한 영역

* 기본 속성
  * action: form을 처리할 서버의 URL
  * method: form을 제출할 때 사용할 HTTP 메서드(GET 혹은 POST)
  * enctype: method가 post인 경우 데이터의 유형
    * application/x-www-form-urlencoded: 기본값
    * multipart/form-data: 파일 전송시(input type이 file인 경우)
    * ~~text/plain: HTML5 디버깅용~~(잘 사용되지 않음)



### input

* 다양한 타입을 가지는 입력 데이터 유형과 위젯이 제공됨
* 대표적인 속성
  * name: form control에 적용되는 이름(이름/값 페어로 전송됨)
  * value: form control에 적용되는 값(이름/값 페어로 전송됨)
  * required, readonly, autofocus, autocomplete, disabled 등

#### input label

* label을 클릭하여 input 자체의 초점을 맞추거나 활성화 시킬 수 있음
  * 사용자는 선택할 수 있는 영역이 늘어나 웹/모바일(터치) 환경에서 편하게 사용할 수 있음
  * label과 input 입력의 관계가 시각적 뿐만 아니라 화면리더기에서도 label을 읽어 쉽게 내용을 확인할 수 있도록 함
  * \<input>에 id 속성을, \<label>에는 for 속성을 활용하여 상호 연관을 시킴

```html
<label for="agree">동의</label>
<input type="checkbox" name="agree"	id="agree">
```

#### input 유형 -  일반

* 일반적으로 입력을 받기 위하여 제공되며 타입별로 HTML 기본 검증 혹은 추가 속성을 활용할 수 있음
  * text: 일반 텍스트 입력
  * password: 입력 시 값이 보이지 않고 문자를 특수기호(*)로 표현
  * email: 이메일 형식이 아닌 경우 form 제출 불가
  * number: min, max, step 속성을 활용하여 숫자 범위 설정 가능
  * file: accept 속성을 활용하여 파일 타입 지정 가능

#### input 유형 - 항목 중 선택

* 일반적으로 label을 사용하여 내용을 작성하여 항목 중 선택할 수 있는 input을 제공
* 동일 항목에 대하여는 name을 지정하고 선택된 항목에 대한 value를 지정해야 함
  * checkbox: 다중 선택
  * radio: 단일 선택

#### input 유형 - 기타

* 다양한 종류의 input을 위한 picker를 제공
  * color: color picker
  * date: date picker
* hidden input을 활용하여 사용자 입력을 받지 않고 서버에 전송되어야 하는 값을 설정
  * hidden: 사용자에게 보이지 않는 input

#### input 유형 - 종합

* \<input>요소의 동작은 type에 따라 달라지므로, 각각의 내용을 숙지할 것. [참고](https://developer.mozilla.org/ko/docs/Web/HTML/Element/input)



## CSS

> Cascading Style Sheets. 
>
> 스타일을 지정하기 위한 언어. (**선택**하고, 스타일을 지정한다.)

```css
h1 {					//선택자
    color: blue;		//선언
    font-size: 15px;	// 속성: 값
}
```

* CSS 구문은 **선택자**를 통해 스타일을 지정할 HTML 요소를 선택
* 중괄호 안에서는 속성과 값, 하나의 쌍으로 이루어진 선언을 진행
* 각 쌍은 선택한 요소의 속성, 속성에 부여할 값을 의미
  * 속성(Property): 어떤 스타일 기능을 변경할지 결정
  * 값(Value): 어떻게 스타일 기능을 변경할지 결정



### CSS 정의 방법

* 인라인(inline): 해당 태그에 직접 style 속성을 활용. 수정 시 불편.

  ```html
  <p style="color: blue; font-size: 40px;">HI</p>
  ```

* 내부참조(embadding)-\<style>:\<head>태그 내에 \<style>지정. 복잡하고 커진다.

* 외부참조(link file): 외부 CSS 파일을 \<head>내 \<link>를 통해 불러오기. 가장 많이 사용됨.

  ```html
  <link rel="stylesheet" href="style.css">
  ```

  

### CSS selectors

* 기본 선택자
  * 전체 선택자(*)
    요소 선택자(태그명. HTML 태그를 직접 선택)
    
  * **클래스** 선택자(**.**으로 시작. 해당 클래스가 적용된 항목을 선택)
    **아이디** 선택자(**#**으로 시작. 해당 아이디가 적용된 항목을 선택. 단일 id 사용 권장)
    속성 선택자
    
    ```html
    <head>
        <style>
            .color-primary {
                color: red;
            }
            .font-50 {
                font-size: 50px
            }
        </style>
    </head>
    <body>
        <p class="color-primary">빨강</p>
        <p class="color-primary" style="font-size:30px;">빨강 30px</p>
        <p class="color-primary font-50">빨강 50px</p>
    </body>
    ```
* 결합자(Combinators)
  * 자손 결합자, 자식 결합자
  * 일반 형제 결합자, 인접 형제 결합자
* 의사 클래스/요소(Pseudo Class)
  * 링크, 동적 의사 클래스
  * 구조적 의사 클래스, 기타 의사 클래스, 의사 엘리먼트, 속성 선택자

#### 우선순위

1. !important
2. 우선 순위

   inline>#id>.class>태그명>*전체, 속성, pseudo-class>요소, pseudo-element
3. CSS 파일 로딩 순서(나중에 선언된 것)

#### 상속

* CSS는 상속을 통해 부모 요소의 속성을 자식에게 상속한다.

* 상속 되는 것: Text 관련 요소(font, color,text-align), opacity, visibility 등

* 상속 되지 않는 것: Box model 관련 요소(width, height, margin, padding, border, box-sizing, display), position 관련 요소(position, top/right/bottm/left, z-index) 등 되는 것: style(Text 관련 요소, opacity) 등

  

### CSS 단위

#### 크기 단위 

* px(픽셀)
  * 픽셀의 크기 변하지 x => 고정 단위
* %
  * 백분율 단위. 가변적인 레이아웃에서 자주 사용
* em
  * (바로 위 부모 요소에 대한) 상속의 영향을 받음
  * 배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈를 가짐
* rem
  * (바로 위 부모 요소에 대한) 상속의 영향을 받지 않음
  * 최상위 요소(html)의 사이즈를 기준으로 배수 단위를 가짐
* viewport
  * 웹 페이지를 방문한 유저에게 바로 보이게 되는 웹 컨텐츠의 영역(디바이스 화면)
  * 디바이스의 viewport를 기준으로 상대적인 사이즈가 결정됨
  * vw, vh,vmin, vmax

#### 색상 단위

* 색상 키워드
  * 대소문자를 구분하지 않는다.
  * ex. red, crimson, black ...
* RGB 색상
  * 16진수 표기법 혹은 함수형 표기법을 사용해서 특정 색을 표현하는 방식
  * ex. #000   rgb(0,0,0)
* HSL 색상
  * 색상, 채도, 명도를 통해 특정 색을 표현하는 방식
  * hsl(120, 75%, 0)

+) a는 alpha(투명도)를 뜻한다.



### Selectors 심화 

* 자손 결합자: selector A 하위의 **모든** selector B 요소
* 자식 결합자: selector A **바로 아래의** selector B 요소
* 일반 형제 결합자: selector A의 형제 요소 중 뒤에 위치하는 selector B 요소를 **모두** 선택
* 인접 형제 결합자:selector A의 형제 요소 중 **바로 뒤**에 위치하는 selector B 요소를 선택

```css
//자손 결합자
div span{
    color: red;
}
//자식 결합자
div > span{
    color: red;
}
//일반 형제 결합자
p ~ span{
    color: red;
}
//인접 형제 결합자
p + span{
    color: red;
}
```



### Box model 

> 모든 HTML 요소는 네모 => 네모빔 맞은 멈뭄미
>
> 위에서부터 아래로, 왼쪽에서 오른쪽으로 쌓인다.(CSS 원칙1)

* 구성: 하나의 박스는 네 영역으로 이루어짐
  * content: 글이나 이미지 등 요소의 실제 내용
  * padding: 테두리 안쪽의 내부 여백. 요소에 적용된 배경색, 이미지는 padding까지 적용
  * border: 테두리 영역
  * margin: 테두리 바깥의 외부 여백. 배경색을 지정할 수 없다.
* 표기

```css
//모두 margin 10px씩
.margin-1{
    margin: 10px;
}
//상하 10px 좌우 20px
.margin-2{
    margin: 10px 20px;
}
//상 10px 좌우 20px 하 30px
.margin-3{
    margin: 10px 20px 30px;
}
//상 10px 우 20px 하 30px 좌 40px
.margin-4{
    margin: 10px 20px 30px 40px;
}
```

* box sizing
  * 기본적은 모든 요소의 box-sizing은 content-box(padding 제외 순수 contents 영역)
  * 일반적으로 영역을 볼 때 border까지의 너비를 원한다면, box-sizing을 border-box으로 설정



### *Display 

> css는 display에 따라 크기와 배치가 달라진다(CSS 원칙2)

#### display: block

* 줄바꿈이 일어나는 요소
* 화면 크기 전체의 가로 폭을 차지
  * 블록의 기본 너비는 가질 수 있는 너비의 100%
  * 너비를 가질 수 없다면 자동으로 margin 부여
* 블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있음
* 블록 레벨 요소) div / ul , ol , li / p / hr / form 등

#### display: inline

* 줄 바꿈이 일어나지 않는 행의 일부 요소
* content 너비만큼 가로 폭을 차지한다
* width, height, margin-top, margin-bottom을 지정할 수 없다.
* 상하 여백은 line-height로 지정한다.
* 인라인 레벨 요소) span / a / img / input, label / b, em, i, strong 등

#### display: inline-block

* block과 inline 레벨 요소의 특징을 모두 가짐
* inline과 같이 한 줄에 표시가 가능하며, block처럼 width, height, margin 속성 지정 가능

#### display: none

* 해당 요소를 화면에 **표시하지 않고**, 공간조차 **부여되지 않음**
* 이와 비슷한 visibility: hien은 해당 요소가 **공간은 차지**하나 화면에 **표시만 하지 않음**



### *Position

> 문서 상에서 요소 위치를 지정
>
> position으로 위치의 기준을 변경(CSS 원칙3)

#### static

* 모든 태그의 기본 값(기준 위치)
* 일반적인 요소의 배치 순서에 따른다.
* 부모 요소 내에서 배치될 때에는 부모 요소의 위치를 기준으로 배치됨

#### relative: 상대 위치

* **자기 자신**의 static 위치를 기준으로 이동(normal flow 유지)
* 레이아웃에서 요소가 차지하는 공간은 static일 때와 같다.(offset)

#### absolute: 절대 위치

* 요소를 일반적인 문서 흐름에서 제거 후 레이아웃에 공간을 차지하지 않음(normal flow에서 벗어남)
  * 다음 블록 요소가 좌측상단으로 붙는다.
  * 특정 영역 위에 존재할 때 사용
* static이 아닌 가장 가까이 있는 **부모/조상 요소를 기준**으로 이동(없는 경우 body)

#### fixed: 고정 위치

* 요소를 일반적인 문서 흐름에서 제거 후 레이아웃에 공간을 차지하지 않음(normal flow에서 벗어남)
* 부모 요소와 관계없이 **viewport(브라우저) 기준**으로 이동.(스크롤 시에도 항상 같은 곳에 위치)



### CSS Layout

#### Float

* 박스를 왼쪽 혹은 오른쪽으로 이동시켜 텍스트를 포함 인라인 요소들이 주변을 wrapping하도록 함. => Normal Flow 벗어남
  * Flexbox, Grid 등장과 함께 사용도 낮아짐
* 활용- Normal Flow에서 벗어난 레이아웃 구성
  * 원하는 요소들을 Float로 지정하여 배치 => Normal Flow에서 벗어나 떠있는 상태
  * 부모 요소에 반드시 Clearing Float를 하여 이후 요소부터 Normal Flow를 가지도록 지정
* 속성
  * 기본값: none 
  * 요소를 왼쪽/오른쪽으로 띄움: Float Left/Right 

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            .box{
                width: 10rem;	//160px
                height:10rem;
                border: 1px solid black;
                background color: crimson;
            }
            
            .left{
                float left;
            }
            
            .clearfix:after{
                content: ""	//뒤에 나올 글씨
                display: block;
                clear both;
            }
        </style>
    </head>
    <body>
        <div class-"clearfix">	//float해도 float 안쓴것처럼.클리어링
            <div class="box1 left">box1</div>
        </div>
        <div class="box2">box2</div>
        <p>
            Lorem Ipsum dolor ~//Lorem 300하면 가짜로 긴 글(dummy text) 생성
        </p>
    </body>
</html>
```

* 이후 요소에 대하여 Float 속성이 적용되지 않도록 Clearing이 필수적
  * ::after: 선택한 요소이 맨 마지막 자식으로 가상 요소를 하나 생성
  * 부모요소에게 clear 속성 부여. 주로 clear: both;를 자주 쓴다.

#### Flexbox

* 행과 열 형태로 아이템들을 배치하는 1차원 레이아웃 모델

  * 수동 값 부여 없이 아이템의 너비와 높이 혹은 간격을 동일하게 배치, 수직 정렬
* 축: main axis(메인 축), cross axis(교차 축-메인 축과 수직)

  * flex-direction: row
    * main axis가 가로. 시작점이 왼쪽(시작점을 오른쪽으로 두려면 row-reverse)
  * flex-direction: column
    * main axis가 세로. 시작점이 위쪽(시작점을 아래쪽으로 두려면 column-reverse)

##### 구성요소

* Flex Container(부모 요소)
  * flexbox 레이아웃을 형성하는 가장 기본적인 모델
  * Flex Item들이 놓여있는 영역
  * 속성을 display: flex; 혹은 inline-flex를 넣어주면 된다
* Flex Item(자식요소)
  * 컨테이너에 속해 있는 컨텐츠(박스)

##### 속성

* 배치 설정
    * flex-direction
        * Main axis의 방향을 설정. 시작점부터 1이다.
      * row, row-reverse, column, column-reverse
    * flex-wrap
      * 아이템이 컨테이너 영역을 벗어나지 않도록 설정(wrap-넘치면 다음줄로/nowrap-기본값. 한줄 배치)
    * flex-flow
      * flex-direction과 flex-wrap에 대한 설정값을 차례로 작성.
      * ex. flex-flow: row nowrap;
* 공간 나누기
  * justify-content
    * Main axis를 기준으로 공간 배분
    * flex-start/flex-end/center/space-between/space-around/space-evenly
  * align-content
    * Cross axis를 기준으로 공간 배분
    * flex-start/flex-end/center/space-between/space-around, space-evenly
* 정렬
  * align-items: 모든 아이템을 Cross axis를 기준으로 정렬
    * stretch/flex-start/flex-end/center/baseline
  * align-self: **개별 아이템**을 Cross axis를 기준으로 정렬
    * stretch/flex-start/flex-end/center
* 기타 속성
  * flex-grow: 남은 영역을 아이템에 분배
  * order: 배치 순서

##### grid



#### Bootstrap

> 세상에서 가장 유명한 프론트엔드 오픈소스

##### CDN

> Content Delivery(Distribution) Network

* 컨텐츠를 더 효율적으로 전달하기 위해 여러 노드에 가진 네트워크에 데이터를 제공하는 시스템
  * 개별 end-user의 가까운 서버를 통해 빠르게 전달 가능(지리적 이점)
  * 외부 서버를 활용함으로써 본인 서버의 부하가 적어짐

##### spacing

* .mt-1: margin top 0.25rem(= 4px)

* .mx-0: margin left right(x축) 0

* .py-2: padding top bottom 0.5rem(=8px)
  * (left=start, right=end)



##### Responsive web

> 별도의 기술 이름이 아닌 웹 디자인에 대한 접근 방식, 반응형 레이아웃 작성에 도움이 되는 사례들의 모음 등을 기술하는데 사용되는 용어



#### Grid system(web design)

>  요소들의 디자인과 배치에 도움을 주는 시스템

* 기본 요소
  * Column: 실제 컨텐츠를 포함하는 부분
  * Gutter: 칼럼과 칼럼 사이의 공간(사이 간격)
  * Container: Column들을 담고 있는 공간

##### Bootsrap grid System

* flexbox로 제작. container, rows, column으로 컨텐츠를 배치하고 정렬
* ***12개의 column, 6개의 grid breakpoints**