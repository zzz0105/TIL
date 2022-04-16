# Markdown & JSON

## Markdown

* 제목: #으로 작성. h1~h6까지 표현 가능. # 개수에 따라 크기가 다르다.
* 순서가 없는 목록(unordered list): *, -
* 순서가 있는 목록(ordered list): 1., 2., ...
* 하이라이팅: `
* 들여쓰기: tab. (들여쓰기 취소는 shift + tab)
* 코드 블록: ```python
* 링크: [~~] (주소)로 쓰면 된다.
* 인용문: >
* 표는 직접 삽입하는 것이 더 편하다.
* 이미지는 드래그앤드롭. 이미지 복사 시 .assets 경로로 복사하는 설정해두면 좋다.
* *기울임*  **굵게**  ~~취소선~~ ---수평선



## JSON(JavaScript Object Notation)

* 자바스크립트 객체 표기법. 웹 어플리케이션에서 데이터를 전송할 때 사용

* 문자 기반(텍스트) 데이터 포맷. 쉽게 활용 가능
* 활용
  * 객체(리스트, 딕셔너리 등)를 JSON으로 변환 - json.dumps
  * JSON을 객체(리스트, 딕셔너리 등)로 변환 - json.load
  * Pprint : 임의의 파이썬 데이터 구조 예쁘게 인쇄
  * 리스트 순회
    * 이름만 출력하고 싶으면? for문 사용하여 키로 접근한다.
    * 가격만 출력하고 싶으면? 없는 값 찾으면 key error 나옴. dict.get(key, defailt-value없을 때 나올 값-) 사용



 ### 데이터 활용을 위한 파일 입력 활용법

```python
f = open('workfile', 'w')			#파일 객체 활용

with open('workfile') as f:			#with 키워드 활용(일반적)
    read_data = f.read
f.closed

open(file, mode='r', encoding=None)	#기본값 설정.파일명, 텍스트모드, 인코딩방식 순.
									#인코딩 방식은 일반적으로 utf-8 사용한다.
```

+) 알고리즘/문제풀이에서는 리스트, 조건문, 반복문을 많이 쓴다.

​	 실무에서는 딕셔너리와 리스트를 많이 사용한다.



### 요청과 응답 그리고 API

* 웹 스크래핑(=웹 크롤링)
  * 웹 주소에서 query에 검색어를 넣으면 검색창에 검색어를 넣은 것과 같은 것을 볼 수 있다.
  * 파이썬을 통해 주소로 요청을 보내고, 응답 결과를 파이썬으로 조작
    * response (200) = 성공적으로 가져옴
    * 404 / 500 = 오류

```python
import requests
URL = 'https://~'    #URL
response = requests.get(URL).json()	#요청. 딕셔너리 타입
print(response.get('~'))
```

* API(Application Programming Interface)
  * 컴퓨터나 컴퓨터 프로그램 사이의 연결
  * 사용하는 방법은 API 사양/명세에 쓰여있다.(꼼꼼히 볼 것) 
