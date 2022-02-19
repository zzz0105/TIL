# 문자열

## 문자의 표현

### ASCII 코드

* 네트워크가 발전하며 서로 정보를 주고 받을 때 다르게 해석하는 문제 발생 => 표준안 만들자!
* 1967년 ASCII 코드 탄생 **7bit**  인코딩 -> 128개의 문자.(33개 출력이 안되는 제어문자와 95개의 출력 가능 문자로 이루어져 있다)



### 확장 ASCII 코드

* **8bit**
* 표준 문자, 악센트문자, 도형 문자, 특수 문자, 특수기호로 이루어짐
* 서로 다른 프로그램이나 컴퓨터 간 교환X. 해독할 수 있도록 설계되어 있어야만 올바르게 해독 가능



### 유니코드

* 자국 문자 표현하기 위한 코드 체계(한글의 코드 체계는 조합형과 완성형이 있다.)를 만들기 시작 -> 그 나라의 코드 체계를 가지고 있지 않다면 잘못 해석 => **다국어 처리를 위한 표준**. 유니코드!

* character set으로 분류. (2와 4는 유니코드를 저장하는 변수의 크기)

  * UCS(Universal Character Set)-2
  * UCS(Universal Character Set)-4

* 그러나 바이트 순서에 대해 표준화가 되지 않아 UCS-2인지 4인지 인식하고 다르게 구현해야하는 문제. => 외부 코딩 필요

  (여러 byte 가지고 큰 값을 저장한다.)

  * Big-endian
    * 낮은 자리를 늦은 주소에 저장한다.
  * Little-endian
    * 낮은 자리를 빠른 주소에 저장한다.

* 유니코드 인코딩(UTF: Unicode Transtformation Format)

  * UTF-8: Web / min: 8bit, max: 32bit(1byte * 4)
  * UTF-16: Windows, Java / min: 16bit, max: 32bit(2byte * 2) 
  * UTF-32: Unix / min: 32bit, max: 32bit(4byte * 1)

* 파이썬의 인코딩

  * 2.x: ASCII -> 첫줄에 명시

    #-*-coding:utf-8-*-

  * 3.x: 유니코드 UTF-8 -> 생략 가능

  * 다른 인코딩 방식을 원한다면 원하는 인코딩 방식 지정

  

## 문자열

* 문자열은 fixed와 variable length로 나뉜다. 

* variable length는 length controlled(java 언어에서의 문자열)과 delimited(c언어에서의 문자열)로 나뉜다.

* java

  * metadata 외에도 4가지 필드들이 포함되어 있다
    * class pointer, Flags, Locks, size
  * 문자열을 저장 및 처리해주는 클래스를 제공한다. string class 사용.
  * 문자열 연산의 경우 연산자와 메소드 형태가 있다.

* C

  * 문자 배열 형태. 끝을 표시하는 널'\0' 문자
  * 연산을 함수 형태로 제공

* Python 

  * char type이 없다. 텍스트 데이터 취급 방법 통일.
  * +는 연결, *는 반복
  * 인덱싱, 슬라이싱 메소드를 제공한다
  * 요소값 변경 불가

  | 언어   | 인코딩        | '홍길동'의 길이              |
  | ------ | ------------- | ---------------------------- |
  | C      | ASCII         | 6<br />2byte씩 나눠 저장해서 |
  | Java   | UTF-16        | 3                            |
  | Python | Unicode UTF-8 | 3                            |

  

### 문자열 뒤집기

1. 자기 문자열에서 뒤집기. 변수 1개 더 필요. 문자열/2번 실행
2. 빈 문자열 만들고 뒤에서부터 읽기

* Python의 경우 slice notation 사용
  * A.reverse()의 경우 A가 리스트인 경우에만 동작



### 문자열 비교

* ==
  * __ eq __() 호출
  * 내용 같으면 True
* is
  * 참조를 비교한다.

```python
s1 = 'abc'
s2 = s1[:2]+'c'
s3 = s1[:3]
print(s1 is s2)	#False
print(s1 is s3)	#True
```

* <, >
  * 맨 앞부터 아스키 코드 대소를 비교한다
    * 'abc' > 'ab'



